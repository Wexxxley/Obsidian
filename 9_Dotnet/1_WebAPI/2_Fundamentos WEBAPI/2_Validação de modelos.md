
#Concluded 

---
Em ASP.NET Core, as validações de modelos podem ser classificadas em built-in  e customizadas.

### **1. Validações Built-in (DataAnnotations)**
As validações built-in são aquelas fornecidas pela biblioteca ASP.NET Core através de Data Annotations. Elas são fáceis de usar e oferecem validações comuns prontas para uso. 

[5_DataAnnotations](9_Dotnet/1_WebAPI/1_Criando%20uma%20WebAPI/5_DataAnnotations.md)

---
### **2. Validações personalizadas**
Existem duas principais maneiras de aplicar validações personalizadas: 
1. Criando um atributo.
2. Implementando IValidatableObject.

#### **2.1 ValidationAttribute**
Vamos supor que a primeira letra do produto tem que ser maiúscula.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcl_zqBFzVLpqML8xJs4oF811qodtLSmLNXrM1EF2HJ5mUFXrKpvO9A3CPfahc8MzU3Jj9soX9JRm1vghLbf6iqIJ40SfhdvxXHdjk-1RIOcWpdjz2Eo3aDb9S7ZgHZATeZEYn9axGxCVjMCHj6AHQ-6LYe?key=SZHaDLu24DLXyFgiFaRNLA)
Foi criado a pasta Validations, e nela a classe FisrtLetterUppercaseAttribute que herda de ValidationAttribute. Nesta classe, sobrescrevemos o método IsValid().
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd6ppd3IpIZKf5Ezc0m8M90yPaMQSIfQWl8RdJOg2syoQbt_dbfdh8FtzVW39Vm0wk8vfNg51R2YiMSau8yHuHzART6gvUBG4DB5tja3TVofRpeiwTOcycsyoFZ6_w_hLcyuobLzyqucoPadY1XDzSLMQIo?key=SZHaDLu24DLXyFgiFaRNLA)

Exemplo recebendo parâmetro![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf8KPZMF3Rv0vvaIEvTn84kDkVvBVBEgVaYZmXnLJBOe_KmbdEJ3zjdnW6pMFuMJROis-c1kVO8sIxjGSE7hwYU0s93cxkRakdZyXjbBCgXHfrmEJ-msnFnw40g0451iRoysqo1rFSqCpPXyg878FPo1Fs?key=SZHaDLu24DLXyFgiFaRNLA)
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdjAw5orqp5_JVaZZzmCDNzZm5GPV3Emaxhrah1-I4YCCHfp7eW_KTUeEps-Jq1afoDb9COJxWSQeL1aYglivu4Ewy9bX73gHsOXEpYIQeEqkw-tsdq1z8wUxZn1xwZmDvEG_ygGdbd0kNDafK8e0Mry-hT?key=SZHaDLu24DLXyFgiFaRNLA)

#### **2.1 Implementando IValidatableObject**
A interface IValidatableObject é usada para permitir a validação personalizada em modelos. Ao implementar essa interface, você pode definir regras de validação que vão além das validações simples fornecidas por atributos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeTSjD9PBwn2FGQYdS8IzoRqq3JOYkVb7YNq8l4_tDPXchaxTB23QGHgSIsT14TCHAeBx85A3itM4W44hpXxjCPBLH_9VKAwAQVHx0H2KTSb0I6mdxI6nBp2Gpw1Uw7EbASbx1RPoCUML9KzZ0Q_q22yM7y?key=SZHaDLu24DLXyFgiFaRNLA)
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfueLkmtaAYx-YrHEa4QbQzBz2FOMfL3RxH-bY6pUWS0ja-kYFfRr_XeX663iadWfOu3sCwCVtZefSrmLqh4iG3eS9YAohKdBpnkJ9FmB963XiPg5hPbFOp6h_4CSNc2SEnBUGoUifGEbcS4DXwC-om2yW5?key=SZHaDLu24DLXyFgiFaRNLA)

___________________________________________________________________________
