
## 1. Validação de Endereços no Domínio (DDD)

### 1.1. Objeto de Valor (Value Object) para o CEP

O CEP não possui identidade própria, mas possui regras estritas de formatação. Ele foi encapsulado em um _Value Object_ para garantir sua integridade antes de qualquer processamento ou persistência.

Exemplo do que pode ser feito:
```c#
namespace AcessoClin.Domain.ValueObjects;

using System;
using System.Text.RegularExpressions;

public class Cep
{
    public string Valor { get; private set; }

    private Cep() { }

    public Cep(string valor)
    {
        if (string.IsNullOrWhiteSpace(valor))
        {
            throw new ArgumentException("O CEP não pode ser nulo ou vazio.");
        }

        // Remove pontuações padrão
        string cepLimpo = valor.Replace("-", "").Replace(".", "").Trim();

        // Valida se o formato final possui exatamente 8 caracteres numéricos
        if (!Regex.IsMatch(cepLimpo, @"^\d{8}$"))
        {
            throw new ArgumentException("O CEP informado é inválido. Deve conter exatamente 8 dígitos numéricos.");
        }

        Valor = cepLimpo;
    }
}
```

### 1.2. Cláusulas de Guarda (Guard Clauses) para Textos

Para atributos puramente textuais (Logradouro, Bairro, Cidade), não basta validar a nulidade. O sistema utiliza cláusulas de guarda na própria entidade para definir limites de tamanho (`Length`), evitando a persistência de textos demasiadamente longos ou curtos.

### 1.3. Fluxo de Orquestração no Backend

A validação de que um CEP reflete uma cidade real não ocorre na entidade, mas sim na **Camada de Serviço**. O fluxo estabelecido é:
1. **Recepção:** O `UsuarioController` ou `ClinicaController` recebe o DTO com os dados.
2. **Delegação:** O Controller repassa essas informações para o serviço principal (ex: `UsuarioService`).
3. **Validação:** O serviço principal aciona, internamente, o `EnderecoService` para aplicar as validações externas do CEP e instanciar a entidade.

---
## 2. Categorização de Exames e Consultas

A otimização de consultas no banco de dados exige que a categoria seja lida diretamente na tabela principal de exames/consultas, evitando a sobrecarga de relacionamentos (_JOINs_). O direcionamento para a implementação é:

- **Uso de Enumerações (Enum):** Altamente recomendado para macrocategorias bem estabelecidas e invariáveis no mercado de saúde (ex: Exames Laboratoriais, Exames de Imagem). Proporciona alta performance de busca e baixa manutenção.
    
- **Uso de Tabela Relacional:** Deve ser aplicado apenas se a regra de negócio exigir que as categorias sejam dinâmicas, altamente granulares e alteráveis via painel de administração.
    

---
## 3. Gestão de Geolocalização

A regra de geolocalização diverge entre o paciente e a clínica, visando performance e precisão dos dados espaciais.

### 3.1. Paciente vs. Clínica

- **O Paciente (Em Tempo Real):** A localização do cliente **não deve ser gravada** no banco de dados. O GPS do dispositivo móvel captura a coordenada no momento do uso e o Frontend a envia no _Payload_ (corpo da requisição) unicamente para o cálculo do raio de busca.
    
- **A Clínica (Estática):** A coordenada da clínica deve ser persistida na tabela `Enderecos` utilizando o tipo espacial nativo do PostGIS, permitindo a indexação na árvore espacial.
    
### 3.2. Geocodificação Automatizada (Backend)

Para garantir precisão e evitar que o administrador da clínica digite coordenadas complexas no momento do cadastro, o sistema utiliza o processo de Geocodificação:
1. O Frontend envia os dados humanos (CEP, Logradouro, Número, Bairro, Cidade).
2. O Backend valida matematicamente o CEP.
3. O Backend realiza, de forma silenciosa, uma requisição HTTP para uma API de Geocodificação (como Google Maps ou Nominatim).
4. A API devolve as coordenadas exatas daquele logradouro.
5. O Serviço instancia a entidade `Endereco`, gerando o objeto espacial `Point` do `NetTopologySuite`, e o persiste no banco.

### 3.3. A Entidade Endereco com Suporte Espacial

A classe consolida a validação de texto e a persistência do ponto espacial (`SRID 4326`).


```c#
namespace AcessoClin.Models;

using AcessoClin.Domain.ValueObjects;
using NetTopologySuite.Geometries;
using System;

public class Endereco
{
    public int Id { get; private set; }
    public Cep Cep { get; private set; }
    public string Logradouro { get; private set; }
    public string Numero { get; private set; }
    public string Bairro { get; private set; }
    public string Cidade { get; private set; }
    
    // Propriedade espacial nativa para o PostGIS
    public Point Localizacao { get; private set; }

    private Endereco() { }

    public Endereco(Cep cep, string logradouro, string numero, string bairro, string cidade, double longitude, double latitude)
    {
        ValidarTextos(logradouro, numero, bairro, cidade);

        Cep = cep;
        Logradouro = logradouro.Trim();
        Numero = numero.Trim();
        Bairro = bairro.Trim();
        Cidade = cidade.Trim();

        // O SRID 4326 define o sistema de coordenadas WGS84 (padrão global de GPS)
        Localizacao = new Point(longitude, latitude) { SRID = 4326 };
    }

    private void ValidarTextos(string logradouro, string numero, string bairro, string cidade)
    {
        if (string.IsNullOrWhiteSpace(logradouro) || logradouro.Length < 3)
            throw new ArgumentException("Logradouro inválido.");

        if (string.IsNullOrWhiteSpace(numero))
            throw new ArgumentException("Número inválido.");

        if (string.IsNullOrWhiteSpace(bairro) || bairro.Length < 2)
            throw new ArgumentException("Bairro inválido.");

        if (string.IsNullOrWhiteSpace(cidade) || cidade.Length < 2)
            throw new ArgumentException("Cidade inválida.");
    }
}
```

---

## 4. Fluxo de Validação de Interface (Frontend)

A integridade dos dados espaciais e textuais começa com um controle rigoroso na interface de usuário, focando na padronização via Correios (ViaCEP).

### 4.1. UX e Liberação Progressiva de Campos

A implementação no frontend deve adotar o modelo de bloqueio e preenchimento automático:

1. Inicialmente, apenas o campo **CEP** fica habilitado para digitação. Os demais campos textuais permanecem bloqueados ou ocultos.
    
2. Após a digitação dos 8 dígitos, o Frontend realiza uma requisição HTTP `GET` para o ViaCEP.
    
3. O Frontend preenche Logradouro, Bairro, Cidade e Estado com a resposta da API.
    
4. O campo **Número** (e Complemento) é habilitado para que o usuário finalize o cadastro.
    
### 4.2. Exceção de Municípios de CEP Único

Cidades do interior frequentemente utilizam um CEP único para todo o município. Nestes casos, o retorno do ViaCEP trará Cidade e Estado, mas Logradouro e Bairro estarão vazios.

- **Ação do Frontend:** A interface deve identificar o logradouro nulo no JSON e, **exclusivamente nestes casos**, desbloquear os campos de Logradouro e Bairro para digitação manual pelo usuário.
    

### 4.3. A Regra de Dupla Validação

É imperativo destacar que o tratamento e o preenchimento automático no Frontend destinam-se exclusivamente à facilidade de uso (UX) e limpeza primária dos dados. **Esta camada não substitui as validações do Backend.** O Backend continuará executando a verificação do Value Object (`Cep`), os Guard Clauses da entidade e acionando a Geocodificação de forma independente.


---

Para modelar a entidade `Endereco` utilizando o Entity Framework Core com suporte a geolocalização via PostGIS, é necessário integrar a biblioteca **NetTopologySuite (NTS)**. Esta biblioteca é o padrão da indústria para manipulação de dados geométricos e geográficos no ecossistema .NET.

Para que o provedor do PostgreSQL reconheça tipos espaciais, você deve instalar o seguinte pacote NuGet no seu projeto de infraestrutura:
- `Npgsql.EntityFrameworkCore.PostgreSQL.NetTopologySuite`

Nesta modelagem, a latitude e a longitude são encapsuladas na propriedade `Localizacao`. Observe o uso de modificadores de acesso privados para garantir o encapsulamento, conforme os princípios do Domain-Driven Design.


```c#
using NetTopologySuite.Geometries;
using AcessoClin.Domain.ValueObjects;

namespace AcessoClin.Models
{
    public class Endereco
    {
        public int Id { get; private set; }
        public Cep Cep { get; private set; }
        public string Logradouro { get; private set; }
        public string Numero { get; private set; }
        public string Bairro { get; private set; }
        public string Cidade { get; private set; }

        /// <summary>
        /// Representa o ponto geográfico (Longitude e Latitude).
        /// O tipo Point provém do NetTopologySuite.
        /// </summary>
        public Point Localizacao { get; private set; }

        // Construtor exigido pelo Entity Framework
        private Endereco()
        {
        }

        public Endereco(Cep cep, string logradouro, string numero, string bairro, string cidade, double longitude, double latitude)
        {
            ValidarTextos(logradouro, numero, bairro, cidade);

            Cep = cep;
            Logradouro = logradouro.Trim();
            Numero = numero.Trim();
            Bairro = bairro.Trim();
            Cidade = cidade.Trim();

            // Instancia o ponto geográfico definindo o SRID para 4326 (WGS 84)
            // Ordem dos parâmetros: Longitude (X), Latitude (Y)
            Localizacao = new Point(longitude, latitude) { SRID = 4326 };
        }

        private void ValidarTextos(string logradouro, string numero, string bairro, string cidade)
        {
            if (string.IsNullOrWhiteSpace(logradouro))
                throw new ArgumentException("O logradouro é obrigatório.");

            if (string.IsNullOrWhiteSpace(numero))
                throw new ArgumentException("O número é obrigatório.");

            if (string.IsNullOrWhiteSpace(bairro))
                throw new ArgumentException("O bairro é obrigatório.");

            if (string.IsNullOrWhiteSpace(cidade))
                throw new ArgumentException("A cidade é obrigatória.");
        }
    }
}
```

A implementação de filtros por raio geográfico varia drasticamente em complexidade e performance dependendo da arquitetura escolhida. A execução desse cálculo exige a compreensão de que a Terra é um esferoide, o que invalida cálculos matemáticos de distância plana (como o Teorema de Pitágoras) para aplicações de geolocalização precisas.

### Abordagem 1: Arquitetura Otimizada (PostGIS e NetTopologySuite)

```c#
using Microsoft.EntityFrameworkCore;
using NetTopologySuite.Geometries;

public async Task<IEnumerable<Clinica>> BuscarClinicasPorRaioAsync(double longitudeUsuario, double latitudeUsuario, double raioEmQuilometros)
{
    // 1. Conversão do raio para metros (unidade base do PostGIS para SRID 4326)
    double raioEmMetros = raioEmQuilometros * 1000;

    // 2. Instanciação do ponto geográfico do usuário
    var pontoUsuario = new Point(longitudeUsuario, latitudeUsuario) { SRID = 4326 };

    // 3. Consulta utilizando o método espacial IsWithinDistance
    var clinicasNoRaio = await _context.Clinicas
        .Include(c => c.Endereco)
        .Where(c => c.Endereco.Localizacao.IsWithinDistance(pontoUsuario, raioEmMetros))
        .ToListAsync();

    return clinicasNoRaio;
}
```

- **IsWithinDistance:** Este método do NetTopologySuite não é executado na memória do servidor C#. O Entity Framework Core o traduz diretamente para a função `ST_DWithin` do PostGIS.    
- **ST_DWithin:** É uma função nativa do banco de dados que executa o cálculo de distância. O seu principal diferencial é a capacidade de identificar automaticamente a existência do Índice GIST. Em vez de ler toda a tabela, a função cruza os dados do índice espacial para descartar localizações distantes antes de aplicar a matemática, operando com complexidade assintótica algorítmica logarítmica, o que garante tempo de resposta na ordem dos milissegundos mesmo com milhões de registros.


### Abordagem 2: Arquitetura Simplificada (Latitude e Longitude)
Se o banco de dados possuísse apenas duas colunas numéricas padrão (`Latitude` do tipo `double` e `Longitude` do tipo `double`), o Entity Framework Core não possuiria um método nativo como o `IsWithinDistance` para calcular a curvatura da Terra no LINQ.
Para executar esse filtro diretamente no banco de dados (evitando carregar todos os registros para a memória do C#), a aplicação precisaria injetar instruções em SQL bruto utilizando a **Fórmula de Haversine**.
```c#
using Microsoft.EntityFrameworkCore;

public async Task<IEnumerable<Clinica>> BuscarClinicasPorRaioSimplificadoAsync(double longitudeUsuario, double latitudeUsuario, double raioEmQuilometros)
{
    // A consulta em SQL Bruto implementa a Fórmula de Haversine (cálculo de distância esférica)
    // O valor 6371 representa o raio médio da Terra em quilômetros.
    string sql = $@"
        SELECT c.* FROM clinicas c
        INNER JOIN enderecos e ON c.IdEnd = e.Id
        WHERE (
            6371 * acos(
                cos(radians({latitudeUsuario})) * cos(radians(e.Latitude)) * cos(radians(e.Longitude) - radians({longitudeUsuario})) + 
                sin(radians({latitudeUsuario})) * sin(radians(e.Latitude))
            )
        ) <= {raioEmQuilometros}";

    // Execução da consulta através do Entity Framework Core
    var clinicasNoRaio = await _context.Clinicas
        .FromSqlRaw(sql)
        .Include(c => c.Endereco)
        .ToListAsync();

    return clinicasNoRaio;
}
```
- **Full Table Scan (Varredura Completa):** O problema central desta abordagem é a impossibilidade de indexação. Como as colunas contêm apenas números primitivos isolados, o PostgreSQL é forçado a realizar a operação matemática complexa de Haversine linha por linha em toda a tabela de `Enderecos` antes de poder avaliar a cláusula `WHERE` (se é menor ou igual ao raio). Este processo consome elevados ciclos de CPU e a performance degrada proporcionalmente ao crescimento do volume de dados cadastrados.