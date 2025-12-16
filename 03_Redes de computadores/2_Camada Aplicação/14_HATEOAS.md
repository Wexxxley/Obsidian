

---
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

JSON HAL é uma especificação comumente utilizada, que define dois MIME Types:
```
application/hal+xml
application/hal+json
```

Que ao serem enviados na solicitação, a API REST deve retornar uma propriedade links, contendo as informações:

- **URI**: A URI do recurso, representada pelo atributo `href`;
- **Tipo de relação:** Descreve como a URI se relaciona com o recurso atual, representado pelo atributo `rel`;
- **Tipo:** Descreve o tipo de conteúdo obtido ou do tipo de verbo que deve ser utilizado para acessar a URI. 

Desta forma, na prática, uma API REST que implemente HATEOAS retornar uma resposta como a abaixo:
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
        },
        {
            "id": 2,
            "nome": "PHP",
            "links": [
                {
                    "type": "GET",
                    "rel": "self",
                    "uri": "api.treinaweb.com.br/cursos/2"
                },
                {
                    "type": "GET",
                    "rel": "curso_aulas",
                    "uri": "api.treinaweb.com.br/cursos/2/aulas"
                },
                {
                    "type": "PUT",
                    "rel": "curso_atualizacao",
                    "uri": "api.treinaweb.com.br/cursos/2"
                },
                {
                    "type": "DELETE",
                    "rel": "curso_exclusao",
                    "uri": "api.treinaweb.com.br/cursos/2"
                }
            ]
        },
        {
            "id": 3,
            "nome": "Java",
            "links": [
                {
                    "type": "GET",
                    "rel": "self",
                    "uri": "api.treinaweb.com.br/cursos/3"
                },
                {
                    "type": "GET",
                    "rel": "curso_aulas",
                    "uri": "api.treinaweb.com.br/cursos/3/aulas"
                },
                {
                    "type": "PUT",
                    "rel": "curso_atualizacao",
                    "uri": "api.treinaweb.com.br/cursos/3"
                },
                {
                    "type": "DELETE",
                    "rel": "curso_exclusao",
                    "uri": "api.treinaweb.com.br/cursos/3"
                }
            ]
        }
    ]
}
```