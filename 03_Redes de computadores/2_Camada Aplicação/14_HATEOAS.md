
#Concluded 

---
### **1. HATEOAS**

O acrônimo HATEOAS vem de Hypermedia As the Engine Of Application State. Ao ser implementado, a API passa a fornecer links que indicarão aos clientes como navegar através dos seus recursos.

Com isso, o cliente não precisa ter um conhecimento profundo da API, basta conhecer a URL inicial e partir dos links fornecidos poderá acessar todos os recursos.

Por exemplo
```json
{
    "cursos": [
        {
            "id": 1,
            "nome": "C# (C Sharp)",
            "aulas": [
                {
                    "id": 1,
                    "titulo": "Título da aula 1"
                },
                {
                    "id": 2,
                    "titulo": "Título da aula 2"
                }
            ]
        },
        {
            "id": 2,
            "nome": "PHP",
            "aulas": [
                {
                    "id": 1,
                    "titulo": "Título da aula 1"
                }
            ]
        }
    ]
}
```

Se esta API implementasse o padrão HATEOAS, no lugar de listar as aulas, cada curso teria um recurso próprio que retornaria suas aulas. Evitando assim que elas fiquem expostas do corpo da requisição. 
```json
{
    "cursos": [
        {
            "id": 1,
            "nome": "C# (C Sharp)",
            "aulas": "api.treinaweb.com.br/cursos/1/aulas"
        },
        {
            "id": 2,
            "nome": "PHP",
            "aulas": "api.treinaweb.com.br/cursos/2/aulas"
        }
    ]
}
```

---
### **2. JSON HAL**

JSON HAL é uma especificação comumente utilizada, que define dois MIME Types:
```
application/hal+xml
application/hal+json
```

>[!INFO]
>
**Mas o que é MIME type?**
MIME Type diz qual é o tipo do arquivo que está sendo transmitido.
>- `Content-Type:text/html`
>- `Content-Type:image/png`
>- `Content-Type:application/pdf`
>- `Content-Type:application/json`
>- `application/hal+json` (Dados em JSON seguindo a regra HAL)

Ao ser enviados na solicitação o type `hal+json`, a API REST deve retornar uma propriedade links, contendo as informações:

- **URI**: A URI do recurso, representada pelo atributo `href`;
- **Relação:** Descreve como a URI se relaciona com o recurso atual, representado pelo atributo `rel`;
- **Tipo:** Tipo de verbo que deve ser utilizado para acessar a URI. 

```json
{
    "cursos": [
        {
            "id": 1,
            "nome": "C# (C Sharp)",
            "links": [
                {
                    "type": "GET",
                    "rel": "self",
                    "uri": "api.treinaweb.com.br/cursos/1"
                },
                {
                    "type": "GET",
                    "rel": "curso_aulas",
                    "uri": "api.treinaweb.com.br/cursos/1/aulas"
                },
                {
                    "type": "PUT",
                    "rel": "curso_atualizacao",
                    "uri": "api.treinaweb.com.br/cursos/1"
                },
                {
                    "type": "DELETE",
                    "rel": "curso_exclusao",
                    "uri": "api.treinaweb.com.br/cursos/1"
                }
            ]
        }
    ]
}
```

**Então a resposta depende do MIME enviado?**

Sim, Isso se chama **Negociação de Conteúdo**. No protocolo HTTP, quando o cliente faz uma requisição, ele envia um cabeçalho chamado **`Accept`**. 

- **Exemplo 1**: "Ei, servidor, me manda os dados. Eu só entendo JSON simples."
	- Requisição: `Accept: application/json`
	- Resposta: Manda o JSON apenas com id e nome, sem os links, 

#### Cenário B: Cliente quer HATEOAS (Links)

O cliente diz: _"Ei, servidor, eu sou um cliente inteligente que usa HATEOAS. Me manda no formato HAL."_

- **Requisição (Header):** `Accept: application/hal+json`
    
- **Resposta do Servidor:** O servidor detecta esse MIME específico e monta a resposta **com** o objeto `_links` (ou `links` no seu exemplo), permitindo a navegação dinâmica.
    

**Resumo:** O servidor _pode_ ser configurado para entregar formatos diferentes para a mesma URL, dependendo do que você pedir no `Accept`.

---

### 3. Uma observação sobre o padrão HAL

O exemplo que você colou acima ilustra perfeitamente o **conceito** de HATEOAS, mas vale um pequeno aviso técnico: a especificação oficial do **JSON HAL** tem uma estrutura ligeiramente diferente (e mais padronizada) do que a lista do seu exemplo.

Geralmente, no HAL padrão:

1. Usa-se `_links` (com underscore) em vez de `links`.
    
2. Usa-se um **objeto (mapa)** e não uma lista (array), onde a chave é o `rel`.
    

**Exemplo HAL Padrão (RFC draft):**

JSON

```
{
    "id": 1,
    "nome": "C# (C Sharp)",
    "_links": {
        "self": { "href": "/cursos/1" },
        "curso_aulas": { "href": "/cursos/1/aulas" }
    }
}
```

O exemplo que você trouxe é válido como HATEOAS, mas pode ser uma implementação customizada da TreinaWeb, e não necessariamente o padrão estrito "HAL". O importante é que o conceito é o mesmo: **o servidor entrega os próximos passos possíveis.**