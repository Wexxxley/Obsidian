
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