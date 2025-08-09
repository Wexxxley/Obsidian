
#Concluded 

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
### **2. Gerenciando mudanças com migrações**
Uma prática comum é versionar o esquema do database  junto com o código da sua aplicação. O EF Core fornece sua própria versão de gerenciamento de esquema chamada migrações. Uma migração é um arquivo que define como o modelo de dados mudou.

Você precisa instalar a ferramenta .NET EF Core na sua máquina para executar os comandos.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdfz9uM091wu2UrKkXV39rn1YBlilfPszq6lnhs91vhrhVTZFN_JlMC0C9g-_4h5sBf2gHfWK-MrCoT6RCSGTqYKyKF0GvnOeHQ4fwyijxlGXU9Fl7KvYAZbrrgpFo3Vh8BhRTA-OFX_hlTuyywTyUUbFJ8?key=SZHaDLu24DLXyFgiFaRNLA)

Criando a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcNhXtfLxao2X0nD2hcI3wZ5kyWgMfK0ePqLFus7dV4EUGcTQ4-Wymwcf2tu5ZJxndJYQ6mFZNCu9FQXbiBWiosLCVAWS2eITlaZL_qj8gqC4IGD6wGq4E_Z6LVaOIcVEcQKlxa76Dedm0d1eJ5UT0c4QsD?key=SZHaDLu24DLXyFgiFaRNLA)

Esse comando cria dois arquivos na pasta Migrations em seu projeto

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXYAYlUSVxbyTyD7IfuFz2CsURfv19-fgfzB6pPA9dsrtwxxMLQEavDuLXl4TFtN6Kr5XTKOzf4LpUDUfPyCfrM-hWRsUlmj8IkFIqSgek8PWjs9_GdqyRSuCkw11GErgvIZzio24u1_KBPPX6WaG_r_8?key=SZHaDLu24DLXyFgiFaRNLA)

Atualizando o database com a migração

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcmvm7pb7nQWb2riS3aMfWsTSLZHgwMESpafbaRqHzkLXDhkcKxmTkJgabC7vVrsu-uuOwqq1u0RK8qrdTd11Y7-c02R6p5dTkFfi8iooSC883RdkKF9Dookw0ZrmmlW_b-R5Z0HjvGyJkU0yAYY2ZgcUw?key=SZHaDLu24DLXyFgiFaRNLA)

- O EF CORE possui algumas convenções, por exemplo, string é passada como nvarchar(max) para o banco de dados e propriedades com “Id” são passadas como primary key. 
- Quase sempre é necessário sobrescrever os padrões adotados pelo EF CORE e, para isso, existe a biblioteca Data Annotations.

  
  
  