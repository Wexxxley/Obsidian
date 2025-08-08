
#Concluded 

---
O middleware é uma peça de software que faz parte do pipeline de solicitação HTTP. Ele processa a solicitação antes que ela chegue ao seu endpoint e também pode modificar a resposta antes que ela seja enviada de volta ao cliente. 

Em termos simples, cada middleware:
1. Recebe uma solicitação HTTP.
2. Decide se vai processar a solicitação ou passá-la adiante.
3. pode manipular a resposta antes de enviá-la de volta ao cliente.

O pipeline de middleware é processado de forma sequencial. Quando uma solicitação chega ao servidor, ela passa por cada componente de middleware na ordem em que foi registrada.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdReyt9t4uuGjWy8i5PD6m-mzQQdih8h2XrLGuixsQtJNP0NKzrKjR0p1UX2wqUCwvjAbUU4domCSewjNoP0NmebDkrX6q359Ii3YbY-BQ76YywH4vmvKYwIIiLYpLnVJMAq8-jMj7KI3FT63l9rLMNQgiW?key=SZHaDLu24DLXyFgiFaRNLA)

 Um middleware pode ser usado para várias funcionalidades, como:
- **Autenticação e Autorização:** Verificar se o usuário está autenticado e tem permissão para acessar o recurso solicitado.
- **Manipulação de Erros:** Capturar exceções e enviar respostas de erro apropriadas.
- **Registro de Logs:** Registrar detalhes da solicitação.  

O pipeline de middleware é definido no program.cs após builder.build()
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYyD4qbeQ3jIasH7Dx5JKgCDZmM-q1Y7O1qNmz7igpQlCXybBUDGxRH55Y6xbRh4ID8rvDtIUg75sJGOb8A_PXDrQ0-H5bzrC0yH45Cy62tleU43Z_YUdZ9MuRE7xtJUQbUQcFd9K4G5t9y5-vob_bEG4?key=SZHaDLu24DLXyFgiFaRNLA)


### 4.7 Tratando erros 

#### 4.7.1 Visualizando exceções em desenvolvimento

 Quando você está desenvolvendo uma aplicação, geralmente deseja ter acesso a todas as informações possíveis quando ocorre um erro. Por esse motivo, existe o DeveloperExceptionPageMiddleware, que você pode adicionar ao seu pipeline usando app.UseDeveloperExceptionPage();

|                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------- |
| NOTA: o WebApplication adiciona automaticamente este middleware quando você está em ambiente de Desenvolvimento. |

Quando uma exceção é lançada e se propaga pelo pipeline até este middleware, ela é capturada. Então, o middleware gera uma página HTML. Esta página contém uma variedade de detalhes sobre a requisição e a exceção.

#### 4.7.2 Lidando com exceções em produção

 A página de exceção do desenvolvedor é útil durante o desenvolvimento, mas você não deve utilizá-la em produção, pois expõe informações sensíveis. Você pode resolver esse problema com ExceptionHandlerMiddleware.   Se ocorrer um erro em sua aplicação, o usuário verá uma resposta de erro personalizada.

  

Obs: Ao adicionar ExceptionHandlerMiddleware, você fornece um caminho para a página de erro personalizada. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcblJNeepfY1EXWE8OybAG5TcXlq_U9kEoOv-T9ptMsd2voZgp1aLE7dTX6KfWGTbdJS7L9g7IIqSl4PgiuVt3rlZhIW_-WxgoPEr-05wLJGEPkakrb2FxwcYRH_3QFfuIyvDmjU9v0gPG0AKpv0T-5Us4?key=SZHaDLu24DLXyFgiFaRNLA)

 A maioria dos aplicativos ASP.NET Core adiciona seu middleware de tratamento de erro de forma condicional, com base no ambiente de hospedagem.

#### 4.7.3 Realizando tratamento global de exceção

Primeiramente, vamos criar um método para simular exceções.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXek72Zg4higUWpJTvPW6a1qNPl3xKq6IaFeZveSqdFAYFbVOPHnNxCj_CWwopOtXUgXQkDuGPkLcBH8S4xhkasgQ98DL_E88qrrppUIrcUQYYT0Yz79UsVkbJGM8hC7r5FakYU11mwfuGIoDkPqlYVL834?key=SZHaDLu24DLXyFgiFaRNLA)

 Agora, vamos criar um middleware para tratar exceções globais.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctqa8ZRXGOigQr8mJ584iAWsCiWD9SWWqhqHzxLIuNsN4o5wi70zzcTy6MbdDmVTrcFVb3qMd1dcK1gTpulpDan3igqU6D5MzqLkr8pBltirtNHfHZpNAqPJP8b0CIf_SPb7tuZiBcEmntTJUiDBmzDUz3?key=SZHaDLu24DLXyFgiFaRNLA)

  

GlobalErrorHandlerMiddleware: Classe responsável por capturar exceções globais durante a execução de requisições.

RequestDelegate: Um delegate que representa o próximo componente na linha do pipeline de requisições.

Invoke: É chamado quando o middleware é executado. Ele envolve a chamada do próximo middleware em um try-catch. Caso ocorra uma exceção, ela é capturada e passada para o método `HandleExceptionAsync`.

HandleExceptionAsync: Este método manipula a exceção e retorna uma resposta adequada ao cliente.

  

 Agora, é só usar o middleware criado no pipeline.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXepmYPb_TCqnRfQRIBJ6sPHrCTWlAAP9ZZaVv5fbpwqDKovEJHbjmHYcV3ar5Mh87vblPi1p1VZMtGx6rcqJBnUQZPI81axPVL4TRtL-_oHEHXGlEJRZhTrobxEWJckhr_n6Dluf4jtdHg8b0P_tqLRX0P7?key=SZHaDLu24DLXyFgiFaRNLA)

Assim fica o tipo de retorno.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-XVLJbsMdfnrIgjyJKpawGhWlSxXbMZOJRQjgvVl0h9-NP1e5VjbWg0KM9i4cEZBfVvGNxQoPnLG7Q92qbqM8-6Wz_KdY0-D8nSXDX_4kg9WwwstqfTkfFofGWeOZmSDQFdfQzjqU6GMdWzlYfzl7too?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

### 4.8 Data Transfer Object (DTO)

 DTO é um padrão de design utilizado para transferir dados entre diferentes camadas de uma aplicação. O principal objetivo de um DTO é encapsular os dados e reduzir a complexidade das interações, especialmente quando se trata de transferir grandes quantidades de dados entre as camadas.

  

Principais benefícios de um DTO:

1. Objeto simples: Um DTO é um objeto simples que contém apenas atributos sem lógica de negócios. Ele serve apenas para transportar dados.
    
2. Segurança: Ao utilizar DTOs, você pode controlar quais dados serão expostos e mantidos ocultos, evitando o retorno de dados sensíveis.
    
3. Organização: Em uma API, os DTOs são utilizados para enviar e receber dados no formato desejado, garantindo que os clientes recebam informações de forma clara e organizada.
    
4. Performance: Com DTOs, você pode controlar exatamente quais dados são transferidos, o que evita o envio de grandes volumes de dados. 
    

#### 4.8.1 Modelo de Visualização (View Model)

 Um View Model é um tipo de objeto usado em aplicações para representar os dados que serão exibidos na interface do usuário (UI). Ele serve como uma camada intermediária entre a lógica de negócios e a interface gráfica.

 Ao invés de enviar entidades do banco de dados para a UI, você cria um modelo que contém apenas os campos necessários para exibir na tela. 

  

View model x DTO

 O DTO é focado em transferir dados entre camadas da aplicação, normalmente entre o servidor e o cliente (API), sem envolver a apresentação dos dados. Mais usado em Web Apis.

 O View Model é criado com o objetivo de alimentar a interface do usuário, contendo apenas as informações que precisam ser exibidas. O conceito de View model é mais utilizado em aplicações MVC.

  
  
  
  
  
  

#### 4.8.2 Exemplo

 Considere essa classe anêmica de curso. Nele temos diversas propriedades, mas nem todas devem ser mostradas a um cliente ou serem utilizadas para transferência de dados entre camadas da aplicação.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXexxsFDrG4-hiwcywJUhjHn2kfeKPxIeIk6-nXEj-rvv2wjG7JZ-tBVVyaHVC2nIRRRCAeGeq2jfwo3sCoBijnqh8Q1J1Yu4jaIDh2M-uzNPgp6xjZi01nd81SJVgr6Jn9Lua8fnU2OANxPDnSARcQYGlQM?key=SZHaDLu24DLXyFgiFaRNLA)

 Portanto, foi criada a classe CursoDTO. Nela temos só as informações mais importantes.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfG6oXopeGafZ9jWjja-6n0_9t6O1eRyEt1MoCnZbxM7ZeUjzhNvRF3UsMoVcTz89wqKMfjYcHlHYT6cavr2UjCl7ZkvPkgSQ-9PH7_sPbjP3_7e6pR1898K2xv5Ri1RWaS2G3jZbu82mO3E5RFOaLaLHw?key=SZHaDLu24DLXyFgiFaRNLA)

  

#### 4.8.3 Mapeamento automático

 Para passar de um curso para um cursoDTO você pode fazer isso manualmente, mas adiciona código excessivo a seus métodos. Assim sendo, é interessante ter possibilidades de mapeamento automático. Duas alternativas são interessantes:

1. Criar uma classe estática com métodos de extensão para fazer a conversão.
    
2. Utilizar o pacote AutoMapper
    

  

 No geral é mais simples utilizar o AutoMapper, mas dependendo da complexidade dos seus modelos, a abordagem por método de extensão pode ser recomendada.

  

1. Instalando o pacote: dotnet add package AutoMapper
    
2. Criando uma classe Responsável por mapear as entidades. 
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHHmbBZo_suouwR3fDctqFI3LB3UM8vTOlrLEYeDgNDCuP0ZZzHZwTosimHf8eGr6Kht7A9ykTapvCtom2jPn5e344nFKZeJdeM3V0cHHj-A68aO0l_isVRByHTEejaitIMqces12mydl1Xx7-SBhQKcfl?key=SZHaDLu24DLXyFgiFaRNLA)

Com ReverseMap CursoRequest pode ser mapeado para Curso.

3. Adicionando ao contêiner.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrJ2_aqRBK7aMjcNHE48A_hWNmLxTHtiklt5DQZQaWR37iUJcHdBNEzwJqZx9NQafGw4hzVUvo6_0NatRERRVTe9fgnctRAKxcIJl3R-f1vGhxRJ0PjYBGsLp5Rb5kTD1JAjQmUv8PqLFRknQWWEb4faQV?key=SZHaDLu24DLXyFgiFaRNLA)

4. Fazendo a injeção de dependência na Controller.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfux749GeSrKSqOAAUsLXhksPKRhdq5bZZX1WhZrricSJkMFrIbCnB6ntuVh7IkurYu6p0IK1Dfz9_Q8zjqSU05vza-lWQJxp-jzPZA0V5b6zW10PYFYwVy_WS2mF_FSPVvBdpZxDA6UXGEh5gcMdP6E7BE?key=SZHaDLu24DLXyFgiFaRNLA)

5. Mapeando: Nova abordagem x Antiga abordagem.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcx_OpwZm_3ukz26bU_synrfeYQxaIBLvq64NpVBfwsDidoBnCxNraNlFDx2nf79L5ZJh8Cv1vOINnXHEai4Gt7cxSzf9VkoqNxwGKXbqnNAypjWWqjPvm4nYmmNnpOz_mxZLY6gridxXwvL9h9fLwBMRky?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
**