
---
### **1. Definindo um relacionamento n-para-1**
Uma categoria pode ter vários produtos e um produto pode ter uma categoria.
![450](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcJtpLVdRdkK2Ly4OGjNe33s1kHpqqXwQI_E1HzuKED5dI7m8ow3sG30KnsYLoaW4K2WEmWkyFmblKnzhWMemkvwhEZNKZxA_iTYmcBA72tB_1rJnD6_rP177cpDjnLZU-c8r4cMGI_UZt_C0kYnaAeWwR-?key=SZHaDLu24DLXyFgiFaRNLA)
**Products**: Coleção que representa os produtos associados a categoria. Ela permite acessar todos os produtos que pertencem a essa categoria.
**Construtor**: O construtor inicializa Products. Evitando que a coleção seja nula.
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd26XdDXOut2wiGKnD2sL5HawRzo3MSzKb_JBfKFSBPmgC9qFjbEIF9YE9mM6dNB-z4nj887Ot84cJN9gekttAHn_T-vnhhDoUROalk_q_cvfCw3N0ruN7t2elWp2LCzeVRuMkTPCq7BmS9vX9nuQOrngE?key=SZHaDLu24DLXyFgiFaRNLA)
**CategoryId**: chave estrangeira
**Category**: Propriedade de navegação. Ela permite que você acesse os detalhes da categoria diretamente a partir do objeto Product.

Obs: Propriedades de navegação não são mapeadas para o banco de dados. 

---
### 2. Gerenciando mudanças com migrações

 Gerenciar mudanças no esquema de bancos de dados, como quando você precisa adicionar uma nova tabela, é difícil. A dificuldade com bancos de dados é que eles contêm dados, então excluí-los e criar um novo a cada implantação não é possível. Uma prática comum é versionar o esquema do database  junto com o código da sua aplicação. O EF Core fornece sua própria versão de gerenciamento de esquema chamada migrações. Migrações fornecem uma maneira de gerenciar mudanças no esquema de um database quando seu modelo de dados EF Core muda.

  

 Uma migração é um arquivo que define como o modelo de dados mudou: quais colunas foram adicionadas, quais as novas entidades, e assim por diante. 

  

 Você precisa instalar a ferramenta .NET EF Core na sua máquina para executar os comandos via terminal.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdfz9uM091wu2UrKkXV39rn1YBlilfPszq6lnhs91vhrhVTZFN_JlMC0C9g-_4h5sBf2gHfWK-MrCoT6RCSGTqYKyKF0GvnOeHQ4fwyijxlGXU9Fl7KvYAZbrrgpFo3Vh8BhRTA-OFX_hlTuyywTyUUbFJ8?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  

Criando a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNhXtfLxao2X0nD2hcI3wZ5kyWgMfK0ePqLFus7dV4EUGcTQ4-Wymwcf2tu5ZJxndJYQ6mFZNCu9FQXbiBWiosLCVAWS2eITlaZL_qj8gqC4IGD6wGq4E_Z6LVaOIcVEcQKlxa76Dedm0d1eJ5UT0c4QsD?key=SZHaDLu24DLXyFgiFaRNLA)

Esse comando cria dois arquivos na pasta Migrations em seu projeto:

- Arquivo de migração: Este arquivo, com o formato Time_MigrationName.cs, descreve as ações a serem realizadas no database, como criar uma tabela, adicionar uma coluna e etc. 
    
- AppDbContextModelSnapshot.cs: Este arquivo descreve o modelo interno atual do EF Core. Este arquivo é atualizado quando você adiciona outra migração, então ele deve sempre ser igual à migração atual. 
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXYAYlUSVxbyTyD7IfuFz2CsURfv19-fgfzB6pPA9dsrtwxxMLQEavDuLXl4TFtN6Kr5XTKOzf4LpUDUfPyCfrM-hWRsUlmj8IkFIqSgek8PWjs9_GdqyRSuCkw11GErgvIZzio24u1_KBPPX6WaG_r_8?key=SZHaDLu24DLXyFgiFaRNLA)

  

 Esses dois arquivos encapsulam o processo de migração, mas adicionar uma migração não atualiza nada no banco de dados em si. Para essa tarefa, você deve executar um comando diferente para aplicar a migração ao banco de dados.

  

Atualizando o database com a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcmvm7pb7nQWb2riS3aMfWsTSLZHgwMESpafbaRqHzkLXDhkcKxmTkJgabC7vVrsu-uuOwqq1u0RK8qrdTd11Y7-c02R6p5dTkFfi8iooSC883RdkKF9Dookw0ZrmmlW_b-R5Z0HjvGyJkU0yAYY2ZgcUw?key=SZHaDLu24DLXyFgiFaRNLA)

 Quando você aplica as migrações ao banco de dados, o EF Core cria as tabelas necessárias no banco de dados e adiciona as colunas e chaves apropriadas. 

 A tabela _EFMigrationsHistory é usada pelo EF core para armazenar os nomes das migrações que ele aplicou ao banco de dados. Da próxima vez que você executar dotnet ef database update, o EF Core poderá comparar essa tabela com a lista de migrações no seu aplicativo e aplicar apenas as novas.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfQnxcRExNGBsYKOh3qBpE13rRi_GTF_vxZha-GiGdjbPCf8jgHtN2sj0Qiu71eE_bF_2HhZPkP1bx0cjq7Nb3bjanF-r3WNvGbQPRzDBpw0CGQMYE6vRRpjfaRkuH1A9X5GCwRseAlKbB-ZK2NGI5Ne9s?key=SZHaDLu24DLXyFgiFaRNLA)

  

 O EF CORE possui algumas convenções, por exemplo, string é passada como nvarchar(max) para o banco de dados e propriedades com “Id” são passadas como primary key. 

 Quase sempre é necessário sobrescrever os padrões adotados pelo EF CORE e, para isso, existe a biblioteca Data Annotations.

  
  
  

#### 3.2.5 Data Annotations

 Data Annotations é um conjunto de atributos que você pode aplicar a classes e membros de classes para configurar o comportamento no EF Core. Esses atributos são muito úteis para definir regras de validação e restrições de banco de dados sem a necessidade de escrever código adicional de configuração.

  

|   |
|---|
|DEF:  Atributos são declarados usando colchetes ‘[]’ antes do elemento que você deseja anotar. Atributos são usados como metadados sobre os elementos.|

É necessário esses dois Usings:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcC99CazaPcldcjQg2q9zjTKSJ-22xhAUChI4HZ0AAA9j5gQBbYpYeq9Xz_XMx1_002YG-D_HmdFlcPe7Esgn-3P7TVImb3l4xpqQBjKvNxaOG4idiaLSbjNtN2ZUI_pI8Dnt-7HIubkFb0Ba4bwCoCE0iI?key=SZHaDLu24DLXyFgiFaRNLA)

  

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
    
14. [Compare]: Utilizado para validar se o valor de uma propriedade é igual ao de outra propriedade. ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe00tT6MWC_PgtcPKeZRbWpPazB0jkS5q06cxmQXB8oMEdJmyXJzVpRWcN1vZ7Bvu1YTeI5A4Jjgsrnx0wN87jH_tza5ZPXMqfoivO1zCzEgHy_jDpvL2FF77YXoGAKECj0iBijZRytPVwSWxjm0MaS7UgU?key=SZHaDLu24DLXyFgiFaRNLA)
    

-Neste caso, Compara ConfirmPassword com Password.

  
  

Assim ficou as classes com Data Annotations

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeX5IcCT-NurpUJH5gbpaO2y5ls6Yw2nolx7cPHiXk7aURyUJ064vbxuyYLhjGrFSP4raJBfVz0_FN805EZhw5RptkWpeXw0N7qiQRYmHUd9uXzbmFsT9mg3vFssiKnQAYSZKm44RENE8JdSSQD_xsJaEc?key=SZHaDLu24DLXyFgiFaRNLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7ZoBirCkc0QH8DyroUEESQoE-h2X6nPl5AVQaSQhEHNB90gT29cWcIF1MBKDrmjWKijX29s45Nr24XhazfC6jF2qNesR7Mth1HQGwJv22-yx5tOmz9ZQ94aBCKzBiS9R0mb6yeFG5XBae4NyoJAR2Wglo?key=SZHaDLu24DLXyFgiFaRNLA)

Após essas mudanças, basta adicionar uma migração e atualizar o database.

#### 3.2.6 Populando as tabelas

 Foi criado uma migração sem alterações e, manualmente, eu inseri os inserts necessários para Categories. Posteriormente enviei as alterações para o database.

Up: Executa as mudanças necessárias no banco de dados.

Down: Reverte as mudanças feitas no Up.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7nFFgCvMR8jJbp2DFLa8ilGZYVwd-SH52LN6PyMn-78Hdd91GvvWE1Sufw1jlYAUMYNIVMvPXQv9quPBJrr3ze90p2gDxgkvw5YmQq2yU1CEtKLj0MMgA_xj_pw95yndVKqLEWt_MPkTfaLuJZMmv7HZn?key=SZHaDLu24DLXyFgiFaRNLA)

  

A mesma coisa foi feita com a tabela Products.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdroVbflpzeHLHfbHfIPKCE3AnGcGYD59dfxex3cmrXT9Nu-V-BlZCj5T25eUE3_1bPF4m-e1nZLxT1tqli17D75HD4wxUvsqrR-w31MkncMVUTje3kZjHJy_RwoCQpj46yWNSXJ52RO2NoHwFdk5Tk-LZX?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

#### 3.2.7 Database first

O banco de dados já está criado. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrXpNx96_D0oPhVlKFFjaSjCq7Kvpj-XNFqd_Eid5jPk-h9o8VwKuAszF1wBKloZABxYeR5KugssoJv5w_7lixpFcfTl-8jTpLCYTtDCNsZwtcbbSr7z22KSpbOvVryAY1SM2cO84KsNbtcHepx2QQC8-E?key=SZHaDLu24DLXyFgiFaRNLA)

  

Como o database foi feito no PostgreSQL, é preciso adicionar um provedor.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf3rVPXCmAv72a_rvalF4llY3McMp0AEE0dWnkN2snwhCZqh5KgH4F2LfIqgOaIZKWjThLbmDNeo1Np-2k3Zyq2FQwk32UeG4pSCf-TwOonOFrY5n4Uq0gfMV64JIpQXNCCGwz-8u0JgSmXxpUqb51KGQkJ?key=SZHaDLu24DLXyFgiFaRNLA)

  

 Com o comando abaixo, é possível criar todos os modelos no EF Core automaticamente.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe9Dh_wRl-EmurF-y8xffrekW_kyFy1e8a2GDMrjL45x0ayNdAoMANF2RMbRoGpMnbldhz4l6FYxeoWukAkaBSzzBstyFM6of4rAjYQBlZU7Su03dKPbqPNRt0wrXP8t9pkmjLd6vyJQz8v7O_XiEHWNHpz?key=SZHaDLu24DLXyFgiFaRNLA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
**