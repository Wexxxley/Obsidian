
---
O middleware de roteamento analisa um modelo de rota dividindo-o em segmentos. Um segmento é separado pelo caractere ‘/’. Cada segmento é um valor literal ou um parâmetro.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfP7slGu49FtKc8TMoyZdPpY_SnOZRgMQfEr3N06oligiDFQMeOI0cnzC1tJTUd1nAhdw65_ng6tKq_85xduAxGkJuOLNlgNyOfuRtIWIODzxM4Qksp-MvYrh4uslT02bQMef4MG2Z-8EnsxTzj8UnNI_M9?key=SZHaDLu24DLXyFgiFaRNLA)

1. O segmento literal product e o parâmetro obrigatório {category}.
2. O parâmetro {name} possui um valor padrão especificado com =all.
3. O parâmetro {id?} define um parâmetro de rota opcional. 

---
### **1. Definindo as rotas**
Podemos definir uma rota que seja padrão para todos os endpoints da entidade.
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfEXsiysm7phbakansgiXs5SnYsROsL11m_IsM8S_v1joP6nnT0aBpZork3BIb0P0PpIS2v_WDbcscuAlqAXgU00PZb3h2Sg5Xvf3rMAbpEVuXu-oWGg2dF1zCEIvPVz6GU5FtMd8IY_TYXafvQcQWA4dx6?key=SZHaDLu24DLXyFgiFaRNLA)
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXehAM-ls-l1p8wTjSs1YvYO7P2SGt9p46zM9HX-N2WJjQnnnDkS3XGKRlUBTrMTaT7PpTcvCqzOzm1KzkGNPc2bl66wzkmMeiRhwdXjd8Qx3xwPFteuhPfZS9YFyhLU64Y9PoS6wXygYEnwKco8u2wQ79eI?key=SZHaDLu24DLXyFgiFaRNLA)
Nestes exemplos, as duas rotas são “Products”.

Nos endpoints é possível especificar mais ainda a rota.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfqh5Q7OndDyKT7lksobSaRAlwoZQ7X3ipbw8Pw9Dsawxtr_Xepb4MRJBxCsgDKntAo3irCiDDePUHEkkSqUmdYaAG76DZn6mFPly4UHjT2Jzxgg2h8NrTLt9LdiHoXdp6JaJ_BhNxU4IXqBUQWHWI5wCfO?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **2. Adicionando restrições aos parâmetros de rotas**
É possível adicionar restrições ao modelo de rota. Por exemplo, {id:int} adicionaria uma restrição na qual o valor atribuído deve ser conversível para int.
![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfa7VAOcpmV-ms6L63wJyZrm7enIFIMjO7NfIq8QQc-wPKvwXcqKjpjmtgHzh8k_DZUeoJeHvwHxe4ukLcP_hn_zskNjbB4qtmQEGcY_dWspcWJByEDoImBX0HC6OSwe3q2ETMzLcPeN1SA9wmfuWbP9to?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **3. Ligação de modelos (model binding)**
 A ligação de modelos extrai valores de uma solicitação e os usa para criar objetos que serão passados como parâmetros para os métodos.

 Quando você cria um método action que contém tipos simples (como int, string e double), o ASP.NET Core automaticamente tenta vincular. Se o nome do parâmetro corresponder ao nome de um parâmetro de rota, o ASP.NET Core vincula ao valor. Além dessa inferência, você pode forçar o ASP.NET a vincular de uma fonte específica adicionando atributos. 

  

Atributos from

 Os atributos [From] substituem a lógica padrão do ASP.NET e forçam os parâmetros a serem carregados de uma fonte de vinculação específica.

Obs: os atributos [from] estão no using Microsoft.AspNetCore.Mvc;

- [FromRoute] força o parâmetro a ser vinculado a um valor de rota.
    
- [FromQuery] força a vinculação de uma string de consulta.
    
- [FromBody] força a vinculação do body da requisição.
    
- [FromHeader] força um parâmetro a ser vinculado a um valor de cabeçalho.
    
- [FromServices] força vinculação a um serviço configurado no container DI.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSZEtI5TQjAl_oVSumFbvGU2jAUw96jUTQ-ZxtXtKzpQZKwaZzneustEvAvOqsYdaVP1urFz23P6m1HaSOWJ0uD1zHQ4DmYiBoYKzE8ZLzqOXtJb8FOudxYcZz0yDp8h4eQs-W44_zGv8sWQ6krw-vb71X?key=SZHaDLu24DLXyFgiFaRNLA)

 Nesse caso, não seria necessário o atributo, visto que já é o comportamento padrão do model binding.

  

___________________________________________________________________________

  
  
  
  
  
**