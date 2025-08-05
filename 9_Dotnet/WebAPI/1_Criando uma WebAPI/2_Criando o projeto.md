
---
Quando você cria um novo projeto, é possível escolher dois tipos de Web APIs:
1. Web APIs com controllers
2. Web APIs sem controllers (minimal api)

Ao instalar o .net, é possível verificar os tampletes disponíveis com: ``dotnet new list``
![](attachments/Pasted%20image%2020250804140139.png)
---
### **Solution File**
Um arquivo `.sln` é um arquivo de organização usado pela plataforma .NET para agrupar e gerenciar um ou mais projetos relacionados. É como um **contêiner** com metadados sobre a estrutura da sua aplicação.

1. **Agrupar Projetos:** Uma solução pode conter múltiplos projetos. 
    - Um projeto de API Web (`.csproj`).
    - Um projeto de testes unitários (`.csproj`).
    - Um projeto de front-end, como Angular ou React (`.esproj`).
2. **Definir Dependências entre Projetos:** Ele define a relação entre os projetos. 
3. **Integração com o IDE:** Ao abrir um arquivo `.sln` no Visual Studio ou no Visual Studio Code, o IDE carrega automaticamente todos os projetos listados

Criando solução.
![](attachments/Pasted%20image%2020250804141303.png)

Criando Projeto WEBAPI.
![](attachments/Pasted%20image%2020250804141318.png)

Adicionando a solução
![](attachments/Pasted%20image%2020250804141337.png)

Para verificar se esta funcionando.
![](attachments/Pasted%20image%2020250804142343.png)

---
### **Configurando o Swagger**
Intale o seguinte e pacote e aplique as seguintes configurações.
![](attachments/Pasted%20image%2020250805090656.png)
![550](attachments/Pasted%20image%2020250805090807.png)

---
### **Criando as entidades**
Criando classes para representar nossas entidades.
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9_vvkVmaaD1lTbulQoMl2LcmsGY2ygx8fK3xuzeVcsaRvoE9BcL_reZLLb9psjbg-L9IIcj15F4cD2zOd8fi2OaDvDUhOEy46lFZFkcWvPL94FZL3aXwK_azfmaamihVZkfmJp88OTXyWqgUKbhXMLbSN?key=SZHaDLu24DLXyFgiFaRNLA)

![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0hI8Tzva3_fx0hTiYzJamZ0uuEB0SHOxynnXWR7mLyfcvCslWFySwK4W8SLrgEfi9SBIZ0J7Q5Ffzz0rpZ98aX7i6zaHHFe04FaA-uSecCxfaM4o1KdP6BgMUxS5EC-C8_4eDHyRMFQaPK7yof7UlhHSg?key=SZHaDLu24DLXyFgiFaRNLA)

Essas classes são consideradas anêmicas, mas o que é isso? Uma classe é considerada "anêmica" quando não possui lógica de negócio e contém apenas propriedades com métodos getter e setter. Essas classes não têm métodos que encapsulam a lógica de negócio, essa lógica é movida para outro serviço.

  
  

___________________________________________________________________________

### 3.2 Entity Framework Core - básico

 O EF Core é uma biblioteca que fornece uma maneira orientada a objetos de acessar bancos de dados. Ele atua como um mapeador objeto-relacional (ORM), comunicando-se com o banco de dados para você e mapeando as respostas do banco de dados para classes e objetos do .NET.

|   |
|---|
|DEFINIÇÃO: Com um mapeador objeto-relacional (ORM), você pode manipular um banco de dados com conceitos orientados a objetos, como classes e objetos, mapeando-os para conceitos de banco de dados, como tabelas e colunas.|

O Entity Framework Core usa o modelo Code First, esse modelo é usado para definir o esquema do banco de dados a partir do código em vez de definir o banco de dados primeiro e gerar o código a partir dele. Com o Code First, você começa escrevendo classes de domínio e o EF cuida da criação e gerenciamento do database.C

#### 3.2.1 Escolhendo o provedor de banco de dados

 Adicionar suporte a um banco de dados específico envolve adicionar alguns pacotes. Você instala um provedor de banco de dados em sua aplicação e o pacote Microsoft.EntityFrameworkCore.Design. Este pacote contém componentes necessários para construir o modelo de dados do EF Core para sua aplicação.

Pacotes e instalações necessárias para SQL Server

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWaQw4UXziG_fURwH6aPv_FipqhqYDTka18htHQKrbvgJ8sfDUlNE99JbG7RIFFwG1R2IDuJYxixGvU-e3YmbnGj_1ORdb0m_0sF9eBL5Yhnz0Y4R2EuIewMhipkvRu4a3EvMNG-sAnzRvTgkjj8NyJiI?key=SZHaDLu24DLXyFgiFaRNLA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdihRD0g69tv2PP2VzaijUqnTwjqKUKf9cix2XEFovPazDO7iuD3XjV8LXLXFpY_QgFq33rtPY9vxszsdYd9aTFfdIqjd8dHZ4uDl3j0twOaWDnghwHZWkOzn8YmDraZgmAHqZbagIqO4uakDA35JSBqNv?key=SZHaDLu24DLXyFgiFaRNLA)

  

 Além de definir as entidades, você define DbContext para seu aplicativo. O DbContext é o coração do EF Core em seu aplicativo, e é usado para todas as chamadas ao banco de dados.  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdJp0dZi6blaAYblVjWW8eZah71bEQzEQ6n6EYtZfeYC1crbEZ9hIoNUTIoNEKQOzg8Is2HQwqh5kBHGv4yghi08tmJvbBA0prAZck33Xmills-L3hWxbR_2y4HDfXN5JTzg2HOwA3wrSi5kviByIfWtM0M?key=SZHaDLu24DLXyFgiFaRNLA)

1️⃣ AppDbContext deriva da classe base DbContext. Esta classe expõe DbSet<> para que o EF Core possa descobrir e mapear as entidades.  

2️⃣ options do construtor contém configurações, como a string de conexão.

#### 3.2.2 Registrando um contexto de dados

 Você deve registrar seu AppDbContext no contêiner de DI. Ao registrar seu contexto, você também configura o provedor de banco de dados e a string de conexão.

  

 O EF Core fornece o método de extensão AddDbContext<T>, o método aceita uma função de configuração para uma instância de DbContextOptionsBuilder.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfeRFle4vLIAlwGwatcCiCukNn9BfyMVimoFKH50apK1jY6NbVaoTZekMXydfFsA0d029SOpTLoWqSJbsC9QDTUDaRMSrs5_B3LbE3Pq1em1tMRQIL6bqiwfeX4Ac5XnK9ksUpLBnPwbmrWwTNmny4w47Fz?key=SZHaDLu24DLXyFgiFaRNLA)

1️⃣  A string de conexão é obtida da configuração, da seção ConnectionStrings. 

2️⃣ Registra o DbContext do seu aplicativo usando-o como parâmetro genérico. 

3️⃣ Especifica o provedor de database nas opções para o DbContext.

  

 A string de conexão é um segredo, então carregá-la da configuração faz sentido. Em tempo de execução, a string correta para o seu ambiente é usada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdeP1vYWf4ct8ceR_oMTZwmJvehIM9LfIVWmevU3ODPmym70BNpjM4P47vyCO9oUjzW27iLdgQm_SPXRWWmGyNgn6xBWcivLy3bax_2f4C8HLTQW8ns_lWpstYiwvhkfNaV11XypSZuuUPzDaglMlL7Axjf?key=SZHaDLu24DLXyFgiFaRNLA)

#### 3.2.3 Definindo um relacionamento n-para-1

 Uma categoria pode ter vários produtos e um produto pode ter uma categoria.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcHtUsDfKNMLeqkrTeJ_pHw4tYcLT_evf9lQwOIFIRkRJAUnXl9q_73hkxe1hR6Z1_qgY_vMesQ4mM_lR6bSjWb2UTBdEp9LOz_-XYXiQ_yEx8xXlxU3FFgeQirUxiwjfWVbQ0miGJZAAs1goy-RVJ91vZO?key=SZHaDLu24DLXyFgiFaRNLA)

Products: Esta propriedade é uma coleção que representa os produtos associados a categoria. Ela permite acessar todos os produtos que pertencem a essa categoria.

Construtor: O construtor inicializa Products. Evitando que a coleção seja nula.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcoKOiYq2RDbk4zqlGWZ0sAeY0HGkmZaOpfXuFi86tBCjGPfdvJpAqIpi1xkZ6iubC01Ich8kZhWkRumZ4Kk3h-GCHtZT5JVJVN6U86C8USeeB8fTP00zUpU5qBP-3WFM_2aHQqU1NTdj7NsWI0YCbSJ80?key=SZHaDLu24DLXyFgiFaRNLA)

CategoryId: Esta propriedade representa uma chave estrangeira que faz referência à entidade Category. 

Category: Esta é uma propriedade de navegação que representa o objeto Category relacionado ao produto. Ela permite que você acesse os detalhes da categoria diretamente a partir do objeto Product.

  

Obs: Propriedades de navegação não são mapeadas para o banco de dados. 

#### 3.2.4 Gerenciando mudanças com migrações

 Gerenciar mudanças no esquema de bancos de dados, como quando você precisa adicionar uma nova tabela, é difícil. A dificuldade com bancos de dados é que eles contêm dados, então excluí-los e criar um novo a cada implantação não é possível. Uma prática comum é versionar o esquema do database  junto com o código da sua aplicação. O EF Core fornece sua própria versão de gerenciamento de esquema chamada migrações. Migrações fornecem uma maneira de gerenciar mudanças no esquema de um database quando seu modelo de dados EF Core muda.

  

 Uma migração é um arquivo que define como o modelo de dados mudou: quais colunas foram adicionadas, quais as novas entidades, e assim por diante. 

  

 Você precisa instalar a ferramenta .NET EF Core na sua máquina para executar os comandos via terminal.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4X1zm3sn37ujIi3-Yn_wO21UcDxUFzXq1_2Zgp6SzrLmRI3op_La23fz8WVC_c4oqC7zz8Wx1orNjdhhLqhZw3870a8I9LKgX1TMnV5WBatFntaaMEuy3vfChvpYh2AEWeyFPsMPPt8rzFzzxP0c1eLXr?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  

Criando a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUtJVZ6jXb89yhrxYInncLUNUHZVsDR-wLFpAMHdmoeTQF8x_ldE3ijCU82KhtNwv9mEKtJDo8yrB46l7jq2r6qwUDtSiMXJSOl_oBqI6j_i5e48XIDeG7ewpwIDeWs5XfuMBexN9Ag8nOJ-Ybrf57Tkiw?key=SZHaDLu24DLXyFgiFaRNLA)

Esse comando cria dois arquivos na pasta Migrations em seu projeto:

- Arquivo de migração: Este arquivo, com o formato Time_MigrationName.cs, descreve as ações a serem realizadas no database, como criar uma tabela, adicionar uma coluna e etc. 
    
- AppDbContextModelSnapshot.cs: Este arquivo descreve o modelo interno atual do EF Core. Este arquivo é atualizado quando você adiciona outra migração, então ele deve sempre ser igual à migração atual. 
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwk3jiMuIH9LoEbEN5Db_VQXm4-_ifL8X71bo1ipWzxA3ZkvXVx2snCAoXib2VLtWKOqRV_MmT-xVkpts8r9gUCM3c_V0FjEeZwCuKp4iSojmMryECskNzYfNZYxNzUDovJxrUqYE_84hxVuic6iceB6U?key=SZHaDLu24DLXyFgiFaRNLA)

  

 Esses dois arquivos encapsulam o processo de migração, mas adicionar uma migração não atualiza nada no banco de dados em si. Para essa tarefa, você deve executar um comando diferente para aplicar a migração ao banco de dados.

  

Atualizando o database com a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcrDBzV1jM4OmmvHn2AIfD7Nr6tLlw7KEDFHbFvmyUQ8HpvterYKpl1CoYvoJro4AJgUrXr7HL3MPB2Bvwu8zaDxzxYkoSpgM46Ne8ZBCG4q8eCTVcp6ZGIr-5GCq6Ulfa3ZF59p_tDrjmBm-1MeqHU9rU?key=SZHaDLu24DLXyFgiFaRNLA)

 Quando você aplica as migrações ao banco de dados, o EF Core cria as tabelas necessárias no banco de dados e adiciona as colunas e chaves apropriadas. 

 A tabela _EFMigrationsHistory é usada pelo EF core para armazenar os nomes das migrações que ele aplicou ao banco de dados. Da próxima vez que você executar dotnet ef database update, o EF Core poderá comparar essa tabela com a lista de migrações no seu aplicativo e aplicar apenas as novas.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc7gTJcMP8kgcRZ_f2HhFKZsD428_NLgeEjqCWRnfndsFVkGKJ_riibWFNWSf2KN1lsn_lm4Swl1VGiQ28BJP0Cv2-v8Gnwv3ovaWX8PKgaqJ1vZNWBUSIlnxNjJIWHPW_B2wPGZ6Q_mRb2T8sdlBc_gcQ?key=SZHaDLu24DLXyFgiFaRNLA)

  

 O EF CORE possui algumas convenções, por exemplo, string é passada como nvarchar(max) para o banco de dados e propriedades com “Id” são passadas como primary key. 

 Quase sempre é necessário sobrescrever os padrões adotados pelo EF CORE e, para isso, existe a biblioteca Data Annotations.

  
  
  

#### 3.2.5 Data Annotations

 Data Annotations é um conjunto de atributos que você pode aplicar a classes e membros de classes para configurar o comportamento no EF Core. Esses atributos são muito úteis para definir regras de validação e restrições de banco de dados sem a necessidade de escrever código adicional de configuração.

  

|   |
|---|
|DEF:  Atributos são declarados usando colchetes ‘[]’ antes do elemento que você deseja anotar. Atributos são usados como metadados sobre os elementos.|

É necessário esses dois Usings:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdr1RODlTHc_9DA1EsWISeZfFPkPHWMOCJvQsSv-jkhLUVtvC93S8KcaiqergwgMQR4tS2cSZ2I1IXY_XvgrW5es-9UU6bE3cWCihE6OMz4nnp2ibPqay-6Iv47K8W3SAqQDLzuBx9AJzTJeY0VlejA1lJ?key=SZHaDLu24DLXyFgiFaRNLA)

  

Principais atributos: 

1. [Key]: Indica que a propriedade é a chave primária da entidade.
    
2. [ForeignKey]: Indica que a propriedade é uma chave estrangeira.
    
3. [Required]: Específica que é not null
    
4. [Table(”name”)]: Especifica o nome da tabela para qual a classe deve ser mapeada.
    
5. [Column(TypeName = "decimal(10,2)")]: especifica o tipo usado no database.
    
6. [MaxLength]: Especifica o tamanho máximo de uma string para o database.
    
7. [MinLength]: Especifica o tamanho mínimo de uma string para o database.
    
8. [StringLenght]: usado para validar o tamanho máx e mín de uma string.
    
9. [EmailAddress]: Valida se a propriedade contém um formato de e-mail.
    
10. [Phone]: Valida se a propriedade contém formato de número de telefone.
    
11. [Url]: Valida se a propriedade contém um formato de URL válido.
    
12. [CreditCard]: Valida se contém um número de cartão de crédito.
    
13. [Range(min,max)]: Define o intervalo máximo e mínimo de valores permitido para um campo numérico. Usado para validação.
    
14. [Compare]: Utilizado para validar se o valor de uma propriedade é igual ao de outra propriedade. ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJmtCTWAvxTVX1IK8bsoHGxWp1T2r-7qqVvgr7MfKoh1vJGJZHTGvSsZhU-I_1RiaLKuvZUeELc4RcYYwNwLoAFRWjxBNBaXXW_wxS1an2iFsjdX-tOqOmkHq644t8sNqXr18MCzTmOB0A5SFamvZ93bLG?key=SZHaDLu24DLXyFgiFaRNLA)
    

-Neste caso, Compara ConfirmPassword com Password.

  
  

Assim ficou as classes com Data Annotations

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcJRnJ6icNZYYK_TTlP2cUx12kaqxO5mFnWHOPLcJl-tIDtNXdTmRvgZDc-jqCnAlZBmVdc85bJYyIh_s7vxzGN-TA3s5YuoJSrH43gY7QqeKOloh4DgAdArVSkogAgTKzR2AEbnh3_8dWh4a-wQBUPjPc?key=SZHaDLu24DLXyFgiFaRNLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdCOxVfmWdr6C0WxAhuC3WANwAectzgI9RjOe5_cxP_55P30g5MzMV1TvTpqrPv10ECYrvi_Eu7EfsDkQkI4JMxnv3LAB_qJ9Te7yoHaWJh2tdXOEZa_UwfvUAXdiZPm6MN0iMzgcCq1hXI7bF5Zm8AQV8D?key=SZHaDLu24DLXyFgiFaRNLA)

Após essas mudanças, basta adicionar uma migração e atualizar o database.

#### 3.2.6 Populando as tabelas

 Foi criado uma migração sem alterações e, manualmente, eu inseri os inserts necessários para Categories. Posteriormente enviei as alterações para o database.

Up: Executa as mudanças necessárias no banco de dados.

Down: Reverte as mudanças feitas no Up.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfI6PiRDGBwbqEwboCq-vyBEpSULYozPR8p182jSwGV4RYf_t4CpuwQxJORTaPqCp91TMuK3LxOZVuQbb5L0onamSv0D3W-_hdTOFqvbbXzb9OzuIxsHW9XYfg0SjQ9rVZBFIW79rhqQJ4S_LY-5RZIRJBG?key=SZHaDLu24DLXyFgiFaRNLA)

  

A mesma coisa foi feita com a tabela Products.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeCOq6mKVm0vn3C4UFxh74IZdkeDvwPr_AuCYx1NJXJw6t22HQan9Bg9VR7zlhLX_AneXq9UopNWDKkc_n0yfqP9YwLTSBvcSgzC167LWlQIIKUTZcaCuHlT9zqX5hkK5lqIfo21VO3J6D3WJBm3is3mXYH?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

#### 3.2.7 Database first

O banco de dados já está criado. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe18EbOhjxEuln5B3zMalm14HJ3o-hLjX3683esDEYmVGwkbp0ce8reUkZvv5YUMQtd-hh7K5ZSRySohAEW2XqbQkya_V_lOwI_xLJECGudfmzVQHcWQmxEsJb05p19r6vKN8TrTQaKRbj7d04J1aqFW5l2?key=SZHaDLu24DLXyFgiFaRNLA)

  

Como o database foi feito no PostgreSQL, é preciso adicionar um provedor.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXed3GyX-ikJKzgardG-sgyzxuSrof8aIdkmdgytcRnnUjMsuoYyDn640zltW7BC334QWlqPR-33KIVP5JFEY6Duma86hv_iJdJtKKZyXE6q1tPS0dR8lV8TL7jLKOH6dUZy5imJ_ZQLFvAkOrIr9wE9tL5X?key=SZHaDLu24DLXyFgiFaRNLA)

  

 Com o comando abaixo, é possível criar todos os modelos no EF Core automaticamente.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeeoJEN7aOkqhyCAwr_jnCPROwgYPikKxKBxnUxVL6iz6YSgGXBuFG9XdN1wKZESykgRspc9wb2m0z7gKvyCxkZRv6wVNQxpiq6u91X0tPUz0YjSdG6HADM9dCAhFyoURhRlGbH4eUG2WNFI1_sTk2gPfjj?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
**