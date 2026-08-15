**

## 2. Injeção de dependência 

 O ASP.NET Core foi projetado desde o início para aderir às boas práticas de engenharia de software. E, para a programação orientada a objetos, os princípios SOLID funcionam muito bem. Com base nisso, o ASP.NET Core possui a injeção de dependência incorporada no coração do framework. Independentemente de você querer usar ou não DI no seu código, as bibliotecas do framework em si dependem dela como um conceito.

 Vamos considerar um exemplo sem DI. Suponha que um usuário tenha se registrado no seu aplicativo Web e você queira enviar um e-mail para ele.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXduNQenXfN7x3vF5_mr4yczEY8qyIanjx8uDvPf7LQNvJ2BdqalaAEtOtJQhm8Y1PAd780FvPPSJUobPFjlJJ5fsqSrFlwdRfNFmPAEPwWnJb7XKVUyLQxMt16O30bgfOL0Jwoz7DDqr9CpvKTe3CsStIry?key=SZHaDLu24DLXyFgiFaRNLA) 

  

O EmailSender precisaria fazer muitas coisas para enviar um e-mail:

1. Criar uma mensagem de e-mail.
    
2. Configurar as configurações do servidor de e-mail.
    
3. Enviar o e-mail para o servidor de e-mail.
    

  

 Fazer tudo isso em uma única classe iria contra o princípio da responsabilidade única, então você acabaria com o EmailSender dependendo de outros serviços. A figura a seguir mostra como essa teia de dependências pode parecer. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcf1OQoO71F8obKxy-eV-jHPpjLCc7JqFUevn3kac9kZ4SiZTGwVCoPmarw-edrWKL0yWuwoHnXJa6FPCGtkP0TUWtiqnWFSDPy0Ksoagi7lES9aXahhs6RG7czCbkCAof10SIqlqJ8ZRykOTqTmjyfsK8p?key=SZHaDLu24DLXyFgiFaRNLA)

 O RegisterUser depende indiretamente de todas as outras classes, então ele deve criar todas elas. O EmailSender depende dos objetos MessageFactory e NetworkClient, então eles são fornecidos através do construtor.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4HQRzFlLSo5JbzdR_hc50R5C1sW_OswPI0e8oaY2LzevzAfSdX3ElVJeKb0DfyWudLyuU2r0dGYoccp-Jgd4NYoWSrnMoigbMMJeDUFAhBQsKmpBOxBfK9eZKcvIOxoPr5Az-Ag27zTARpZTbOgWIvioI?key=SZHaDLu24DLXyFgiFaRNLA)

 O NetworkClient depende do objeto EmailServerSettings, então é preciso passá-lo no construtor de NetworkClient.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXft_PyWdgjb3bZCA9BFWF5dVv8hi-NV-1Nm9KEkcMb-UqyuQHnT5mJNX7OUYWN4K5iqDWsjIjBWD__wnoZ4B2R9VY-0FMNiJcLVjJd9iiBZ7jYZOtzYpxqO69NhsUK0kLkfmndbRshu9xJI_0mdL92MFm4?key=SZHaDLu24DLXyFgiFaRNLA)

  

 A injeção de dependência visa resolver o problema de classe chamadora ter que criar suas dependências. Em vez de o manipulador RegisterUser criar suas dependências manualmente, uma instância já criada de EmailSender é passada como argumento para o método RegisterUser. Obviamente, algo precisa criar o objeto. O serviço responsável por fornecer a instância é chamado de container IoC.

|   |
|---|
|Definição: O container IoC é responsável por criar instâncias de serviços. Ele sabe como construir uma instância de um serviço criando todas as suas  dependências e passando-as para o construtor.|

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVqsH3FNrp9ewy5Rk8sFFVWeYQrijS0Wumoanq9iy-EEKm-BrPobpeYG3bW6h8QQNDNGnzoz7yHYadCjWgi5VDmgfDAc4KlIF1T9veLyJ2AzlleQ9At58iXEH0-GVqHGizloYxPsvzB549vbMRvJzcR4no?key=SZHaDLu24DLXyFgiFaRNLA)

 O RegisterUser declara que requer EmailSender, e o container fornece isso.

___________________________________________________________________________

### 2.1 Adicionando serviços do framework ASP.NET Core ao container

 Você registra serviços com a propriedade Services em WebApplicationBuilder.

Por exemplo, para usar Razor Pages, você precisa registrar os componentes no container da aplicação. Todas as bibliotecas comuns que você usa expõem métodos de extensão para cuidar dos detalhes complicados. 

 Esses métodos de extensão configuram tudo o que você precisa de uma vez só. O framework RazorPages expõe o método de extensão AddRazorPages().

|   |
|---|
|NOTA: A propriedade Services é do tipo IServiceCollection. É aqui que você registra a coleção de serviços que o container DI conhece.|

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdN86hJEAXiGog1zS3prbIAbih_qiYfftjc0nlm1O3yKRmlFCZkrRyRsaXhG3G_lz-qzd3D1po4pkQXaeLm1FQnNnXPcG9FEEURK4pKyskrU8IpAGsYYiTXFKDvawhxBYjzqttFI5jVhBnpU9_QvwPxX8Zh?key=SZHaDLu24DLXyFgiFaRNLA)

 Cada biblioteca que tiver serviços necessários deve expor um método de extensão Add*().  ___________________________________________________________________________

### 2.2 Usando serviços do container DI

Em uma Web API, você tem duas maneiras de acessar serviços do contêiner

1. Injetar no construtor de uma classe 
    
2. Injetar serviços em um manipulador de endpoint.
    
3. Acessar diretamente no Program.cs.
    

  

2.2.1 Injetar no construtor

Nesse exemplo, o contexto do database registrado no container é injetado em uma classe controller.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfX9sUaO3Kk3SphQVbzrXY7l9GggL68m1DynKf4pGIAH_9yGBGekBXajFZgsteRU-fpn9qkCTJXm1mvbQ_5qY9uPyzc6kemC_BL-IjWEmHiTEk6LeuKV4izYCW-deMj0KIaQN_thUsg6GPstacaU0CkWRw0?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  

2.2.2 Injetar serviços em um manipulador de endpoint.

 Você pode injetar um serviço em um manipulador de endpoint adicionando-o como um parâmetro. Vamos usar como exemplo o LinkGenerator.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdNdZWXRfZ1k1EScE2yh34k5SXPXjiZioICCAbRvOPidrmbbI3DWGlAedpin1-bfJfKnuhpgwFLYDNMw4KwRCxUZRpY13jm-oDpOCA1-oc72-I1Vp5QNjPHEGdchLM4BY4OLXdLNd1Gnz5S6x14uvPEsjUa?key=SZHaDLu24DLXyFgiFaRNLA)

 A implementação do LinkGenerator registrada no container declara as dependências que requer tendo parâmetros em seu construtor. Quando o container cria LinkGenerator, ele primeiro cria todas as dependências do serviço e as usa para criar a instância final.

  

2.2.3 Acessar diretamente o serviço em `Program.cs`.

 Às vezes você precisa acessar um serviço fora do contexto de uma requisição. Para isso você pode usar WebApplication.Services, que expõe o container como um IServiceProvider.

|   |
|---|
|NOTA: Você registra serviços em IServiceCollection exposto em WebApplicationBuilder.Services. Você solicita serviços com IServiceProvider exposto em WebApplication.Services.|

GetService<T>(): Retorna o serviço T se estiver no container; caso contrário, null.

GetRequiredService<T>(): Retorna o serviço T se estiver disponível no container; caso contrário, lança uma InvalidOperationException.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdj1oO317CS-2kIcik0AoEctWLmmkBWnx1Xmh53xuMQzkfYcDlz6CRxWrEX2D29me0STxc5273AXLxIxSeHO0I941pFlNLiMWcukgG31nTDpVtsjsBUGs9RkaodbRGDoq9Ss8BAwEnkvLv9R6JSJojX3Uqs?key=SZHaDLu24DLXyFgiFaRNLA)

___________________________________________________________________________

### 2.3 Registrando serviços personalizados

 Configurar o contêiner DI para serviços personalizados envolve informá-lo sobre qual tipo usar quando um determinado serviço for solicitado. Por exemplo:

1. Se um serviço requer IEmailSender, use a instância de EmailSender.
    
2. Se um serviço requer NetworkClient, use a instância de NetworkClient.
    
3. Se um serviço requer MessageFactory, use a instância de  MessageFactory.
    

  

|   |
|---|
|NOTA: Você também precisará registrar o objeto EmailServerSettings.  Faremos isso de forma diferente mais adiante.|

Essas declarações são feitas chamando métodos Add* em IServiceCollection. 

Cada método Add* fornece três informações ao contêiner:

- Tipo de serviço com TService: Esta classe ou interface será solicitada como uma dependência. Geralmente é uma interface, mas às vezes um tipo concreto.

- Tipo de implementação com TService ou TImplementation: O container deve criar esta classe para atender à dependência. Deve ser um tipo concreto.

- Tempo de vida com transiente, singleton ou scoped: O tempo de vida define por quanto tempo uma instância do serviço deve ser usada pelo contêiner DI.

Obs: Será explicado sobre tempo de vida mais adiante.

 A Listagem a seguir mostra como você pode configurar EmailSender e suas dependências usando três métodos: ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4yebcAEUoLwg9jxg8UIeTJr7md2giQW773OfqJzWzE0rOPIhFWpLiGJa3RKm3UKzLnvm5s9evydSMoAZqjjDZjW3esfK7AvG6vFIWNHxT_j7iucsBxTIfdkDXWZx6G_Kbo5uKcp795N4g7PG_HzN-f_g?key=SZHaDLu24DLXyFgiFaRNLA)

AddScoped<TService,TImplementation>:Se precisar de IEmailSender, use EmailSender.

AddScoped<TService>: Se precisar de um NetworkClient, use NetworkClient

AddSingleton<TService>: Se precisar de um MessageFactory, use MessageFactory.

___________________________________________________________________________

### 2.4 Tempo de vida de um serviço

 O tempo de vida de um serviço refere-se ao tempo que uma instância do serviço deve viver em um contêiner antes que o contêiner crie uma nova instância. 

  

No ASP.NET Core, você pode especificar três tempos de vida:

1. Transient: Sempre que um serviço é solicitado, uma nova instância é criada. Potencialmente, você pode ter diferentes instâncias da mesma classe dentro do mesmo gráfico de dependência.
    
2. Scoped: Dentro de um escopo, todas as solicitações para um serviço dão a você o mesmo objeto. Cada solicitação web recebe seu próprio escopo.
    
3. Singleton: Você sempre recebe a mesma instância do serviço, independentemente do escopo.
    

 Um serviço deve usar apenas dependências que tenham um tempo de vida maior ou igual ao tempo de vida do próprio serviço para ter segurança. 

4. Um serviço singleton pode usar apenas dependências singleton. 
    
5. Um serviço scoped pode usar dependências scoped ou singletons. 
    
6. Um serviço transiente pode usar dependências com qualquer tempo de vida.
    

  

Dependência cativa: Ocorre quando um serviço com um tempo de vida mais curto é injetado em um serviço com um tempo de vida mais longo, criando uma situação em que o serviço de vida curta acaba sendo mantido por mais tempo do que deveria. 

  

 O ASP.NET Core verifica esse tipo de dependência e lança uma exceção na inicialização do aplicativo ou no primeiro uso da dependência. Essa verificação tem um custo de desempenho, então, por padrão, ela é habilitada apenas quando seu aplicativo está rodando em ambiente de desenvolvimento. Você pode habilitar essa verificação da seguinte forma.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcsV0VbdaPI069CiLXmXc6xKWyIfbFYOFSWzvY7HuZ1ldM1p7oFZWalEsagCPjzkkLw0xKUDKTyZ6JZXMT-SMZfF2mSP-Dp4ilLXuLm7O4f1gKve6rXgsw5ZB616R511zR_CP9P5iK7ZyOLv8NbW7S_fuzt?key=SZHaDLu24DLXyFgiFaRNLA)

ValidateScopes validará escopos em todos os ambientes, o que tem implicações de desempenho.

ValidateOnBuild verifica se todos os serviços registrados têm todas as suas dependências registradas.

  

___________________________________________________________________________

### 2.5 Registrando serviços usando objetos e lambdas

 Como mencionado, não foi registrado EmailServerSettings, visto que  NetworkClient depende dele e é necessário adotar uma abordagem diferente.

 Os métodos anteriores usam genéricos para especificar o tipo da classe a ser registrada, mas não fornecem nenhuma indicação de como construir uma instância. Em vez disso, o contêiner faz suposições que você deve seguir: A classe deve ter apenas um construtor relevante. Para um construtor ser relevante, todos os argumentos devem ser registrados no contêiner ou devem ter valor padrão.

  

 O registro EmailServerSettings não atende a esses requisitos, pois exige que você forneça parâmetros sem valores padrão. Você deve criar uma instância do objeto EmailServerSettings e fornecê-la ao contêiner, conforme mostrado no exemplo.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe1xwzkRSgFj6ZARxg6UXJAwQPXli9lOxDj9YybYx7kzMNp6utkBxndaayB2FmIpsSqRvxea8F1mSk6Byhf-ZU32Ps-4n-wiVDqp-C6KcdzA--cu-dk3fCiqGUlSPNe8KbVsk_ykG4YOxIRHZolGVTt9OI?key=SZHaDLu24DLXyFgiFaRNLA)

 Esta instância de EmailServerSettings será usada sempre que uma instância for necessária.

  

 Este código funciona bem se você quiser ter apenas uma única instância de EmailServerSettings. O mesmo objeto será compartilhado em todos os lugares. Mas e se você quiser criar um novo objeto cada vez que um for solicitado?

  

 Em vez de fornecer uma única instância, você pode fornecer uma função que o contêiner invoca quando precisar.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDEqjnoatMS4f1xHJRRidpY3W5God7XhFQuzN6dadGcr_MUByYRKuAb7J92QAq5aAsHcoPzbJOrmOha-7kYm0_T20rooX0LuqO85wGJnn0jc2cbw-uLsD9mNTx3Ao8zL9BxLnQmpHA_tbE4_SqQ-pSs6P9?key=SZHaDLu24DLXyFgiFaRNLA)

 O construtor é chamado toda vez que um objeto EmailServerSettings é necessário, em vez de apenas uma vez.

___________________________________________________________________________

___________________________________________________________________________

### 2.6 Criando um método de extensão para adicionar serviços

 Todas as suas dependências estão registradas. Mas o Program.cs está começando a ficar um pouco bagunçado. Uma solução é criar um método de extensão a IServiceCollection para adicionar os serviços necessários.

  

Foi criada uma pasta Extensions que contém Métodos de extensão.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeUxh4kXZsdPC4GYN1FEwYc5YwCrwH83JirsM5Lmqilcin1ASV5__--S_gszdXPtRO0s571vuVjzvLYb_od48YJleOuuMT0I7tfv4dbDNqdGJeNDqr0sdkF48AtvkPCcQc6DtjEEKnbTsdhtNOm2ZXgkw8?key=SZHaDLu24DLXyFgiFaRNLA)

Implementação da extensão.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeE8vX8igPn0Kqm_RhGNgxxU23ZHEopluCNj9E1babjxlBpVJqv6ttJcRKmMemUBBakstqNw1mHtiPmU6ESAyoap66T5e_2r6tS0ieGgs0qw2hMO38yMxTBe5DqYhbl6tVOKTNXiX-mRYSfTKT6N2MMXdl2?key=SZHaDLu24DLXyFgiFaRNLA)

Código necessário na Program.cs

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXezqN-HXkrdAfWehBU-EhbCIPqc38cyjm1Kbm5F8LF8BoqjHqaOxRrjurzJlhhhe3NtXXsHfO21MSuQScVClzxzKELkx_beQIHvBeYoaB5ljxPqy332ZvYhpaSyGJUzkWLWPuiQKOSPbB2XcfNi-xveduY?key=SZHaDLu24DLXyFgiFaRNLA)

  

___________________________________________________________________________

### 2.7 Registrando um serviço no contêiner múltiplas vezes

 Uma vantagem de codificar usando interfaces é que você pode criar múltiplas implementações de um serviço. Suponha que você queira criar uma versão generalizada de IEmailSender para que possa enviar mensagens Email, SMS e Facebook. Você cria a interface IMessageSender e as várias implementações: EmailSender, SmsSender e FacebookSender. 

2.7.1 Injetando múltiplas implementações de uma interface

 Suponha que você queira enviar uma mensagem usando cada uma das implementações sempre que um novo usuário se registrar. A maneira mais fácil é registrar todas as implementações do serviço no seu contêiner e fazer com que ele injete uma de cada tipo no manipulador de endpoint. Então RegisterUser pode usar um simples laço para chamar cada implementação

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeliudQGAxzxklQInzXEq4Ffk2-nH0U-vrrqeK5THAi5Gzo02tM4v-bhiCqGpqAnmuCWQ7gu-sgLafUP_AsG5rYBt2BfQEJf3A9xebuu9TWStQ_DNCSWaqGFoq61YphCQyPPXtykWgwXrWO1GNs6AgLwgm3?key=SZHaDLu24DLXyFgiFaRNLA)

 Você registra múltiplas implementações do mesmo serviço no contêiner DI da mesma maneira que para implementações únicas.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcRu3P8cB4DlhuOhfIjssipfKlV43fbJkUC813cmOE1Jbpj1X7zyiB58kFX2X7q9azHaEYFMdPUCpgmrLGDyyopkyGL2Z9NMyZHAsA8k5L7UTdRGbI1w42XbDPpQXJfWAmkUPzQEZDcpY1n9hd_Eob5LX0d?key=SZHaDLu24DLXyFgiFaRNLA)

Então, você pode injetar IEnumerable<IMessageSender> em RegisterUser.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXefENlu3z9VSToPA8NMX2iV_tTv5wLDN8AFhQohyImASCOSMj7JHvVQXzLaXiblr_D-t0wifdu2PFyoDl-5aL0DVTf4KsPQ6VbVSRBmRgmom5NQexHzGbcRUtUk-hKK3HmtvWlNudCUEYu9kUsvy-uneXwd?key=SZHaDLu24DLXyFgiFaRNLA)

___________________________________________________________________________

  
  
**