

### 1. Validação endereços

Value Objects são utilizados para encapsular regras de negócio de atributos que não possuem identidade própria. O CEP é o candidato ideal para se tornar um Value Object.

Para atributos puramente textuais e sem formatação estrita (como Logradouro e Bairro), a prática formal é utilizar Cláusulas de Guarda dentro da própria entidade.

```c#
namespace AcessoClin.Domain.ValueObjects;

using System;
using System.Text.RegularExpressions;

public class Cep
{
    public string Valor { get; private set; }

    private Cep()
    {
    }

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

Para os campos textuais (`Logradouro`, `Bairro`, `Cidade`), a validação não deve se limitar à nulidade. É necessário definir **limites de tamanho (Length)** para evitar que o banco de dados seja sobrecarregado com textos imensos.

```c#
namespace AcessoClin.Models;

using AcessoClin.Domain.ValueObjects;
using System;

public class Endereco
{
    public int Id { get; private set; }
    public Cep Cep { get; private set; }
    public string Logradouro { get; private set; }
    public string Numero { get; private set; }
    public string Bairro { get; private set; }
    public string Cidade { get; private set; }

    private Endereco()
    {
    }

    public Endereco(Cep cep, string logradouro, string numero, string bairro, string cidade)
    {
        ValidarTextos(logradouro, numero, bairro, cidade);

        Cep = cep;
        Logradouro = logradouro.Trim();
        Numero = numero.Trim();
        Bairro = bairro.Trim();
        Cidade = cidade.Trim();
    }

    public void Update(Cep cep, string logradouro, string numero, string bairro, string cidade)
    {
        ValidarTextos(logradouro, numero, bairro, cidade);

        Cep = cep;
        Logradouro = logradouro.Trim();
        Numero = numero.Trim();
        Bairro = bairro.Trim();
        Cidade = cidade.Trim();
    }

    private void ValidarTextos(string logradouro, string numero, string bairro, string cidade)
    {
        // Validações de Logradouro
        if (string.IsNullOrWhiteSpace(logradouro) || logradouro.Length < 3 || logradouro.Length > 150)
        {
            throw new ArgumentException("O logradouro deve conter entre 3 e 150 caracteres.");
        }

        // Validações de Número (Permite "S/N" ou números grandes)
        if (string.IsNullOrWhiteSpace(numero) || numero.Length < 1 || numero.Length > 20)
        {
            throw new ArgumentException("O número deve conter entre 1 e 20 caracteres.");
        }

        // Validações de Bairro
        if (string.IsNullOrWhiteSpace(bairro) || bairro.Length < 2 || bairro.Length > 100)
        {
            throw new ArgumentException("O bairro deve conter entre 2 e 100 caracteres.");
        }

        // Validações de Cidade
        if (string.IsNullOrWhiteSpace(cidade) || cidade.Length < 2 || cidade.Length > 100)
        {
            throw new ArgumentException("A cidade deve conter entre 2 e 100 caracteres.");
        }
    }
}
```

Para resolver a exigência de que o CEP **tem que referenciar alguma cidade**, isso deve ser orquestrado na camada de Serviço, antes da criação da Entidade `Endereco`.

O fluxo técnico deve ocorrer na seguinte ordem:
1. **Recepção:** O `UsuarioController/ClinicaController` recebe o DTO contendo os dados pessoais e os dados de endereço.
2. **Delegação:** O Controller repassa essas informações unicamente para o `UsuarioService`.
3. **Validação e Orquestração:** O `UsuarioService` percebe que precisa processar um endereço. É neste momento que ele aciona, internamente, as validações de CEP contidas em EndereçoService.

---

### 2. Tipo exame/consulta direto na tabela

No contexto de sistemas de saúde, os exames geralmente possuem macrocategorias muito bem estabelecidas e invariáveis (ex: Exames Laboratoriais, Exames de Imagem, Exames Cardiólógicos).

Se a sua regra de negócio estipula que a classificação será em alto nível (macrocategorias genéricas), a implementação via **Enum** é altamente recomendada devido à baixa manutenção e alta performance de busca.

Se a sua regra de negócio exige que o catálogo seja altamente granular e atualizado constantemente com novas nomenclaturas do mercado de saúde, a criação de uma Tabela é obrigatória.


---

### 3. Armazenamento geolocalização

- **O Paciente (Em Tempo Real):**  a localização do cliente não precisa (e não deve) ser gravada no banco de dados para a busca. Quando ele abre o aplicativo, o GPS do celular captura a coordenada atual dele. O Frontend envia essa coordenada no _Payload_ (corpo da requisição) da busca.
    
- **A Clínica (Estática no Banco):** A clínica não se move. A coordenada dela precisa estar gravada na tabela de `Enderecos` para que o PostGIS consiga indexá-la na árvore espacial. No entanto, o responsável pela clínica **não digitará** essa coordenada no momento do cadastro.

Para ter a informação de forma automática e precisa, o seu sistema precisará utilizar um processo chamado **Geocodificação**. Trata-se da conversão de um endereço em formato de texto (Rua, Número, Cidade, Estado) em coordenadas geográficas (Latitude e Longitude).Existem serviços externos (APIs) dedicados exclusivamente a isso, como a _Google Maps Geocoding API_, _Mapbox_, ou o _Nominatim_ (OpenStreetMap, que é gratuito).

1. **Entrada de Dados:** O administrador da clínica preenche apenas dados humanos no Frontend: CEP, Logradouro, Número, Bairro e Cidade.    
2. **Validação Inicial:** O seu backend valida o CEP (como discutimos na regra do Value Object).
3. **Chamada à API de Geocodificação:** O seu backend, silenciosamente, pega essa string formatada (Ex: _"Rua Epitácio Pessoa, 123, Centro, Quixadá, CE"_) e faz uma requisição HTTP para a API do Google Maps ou OpenStreetMap.
4. **Resposta Precisa:** A API externa devolve um JSON contendo a Latitude e a Longitude exatas daquela porta.
5. **Instanciação e Persistência:** Com os dados textuais e as coordenadas automáticas em mãos, o seu Serviço instancia a entidade `Endereco`, criando o objeto `Point` do NetTopologySuite, e salva no banco de dados.


### 4. Por que manter o Ponto Geográfico na Entidade Endereço?

Mesmo que a captura seja automática no backend, a propriedade `Localizacao` (o `Point` do PostGIS) deve continuar dentro da classe `Endereco`, e não na classe `Clinica`.

A justificativa arquitetural para isso é a **Coesão**:

- A coordenada geográfica é uma propriedade intrínseca de um local físico, não de um CNPJ ou de uma instituição de saúde.
    
- Se, no futuro, a clínica se mudar de prédio, o endereço inteiro será substituído. Ao atrelar a coordenada ao `Endereco`, você garante que a Latitude e Longitude antigas sejam descartadas junto com o nome da rua antiga, impedindo que o sistema fique com dados inconsistentes (uma rua nova apontando para a coordenada do prédio velho).
    

### Conclusão Técnica

A sua visão de capturar automaticamente está corretíssima. A solução técnica não exige mudar a modelagem das entidades (que já está correta com o `Point` no `Endereco`), mas sim **enriquecer a camada de serviço** com uma integração de Geocodificação.

Ao fazer isso, você garante a melhor precisão possível (fornecida por provedores de mapas globais) sem onerar o responsável pela clínica com tarefas técnicas no momento do cadastro.

```
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

    // Construtor exigido pelo Entity Framework
    private Endereco() { }

    // Construtor rico: Recebe os textos do usuário + as coordenadas da API
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

