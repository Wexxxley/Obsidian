
---
### **1.1 Ambiente virtual python e instalação de dependências**

Um ambiente virtual é um espaço isolado onde você pode instalar pacotes Python sem afetar os pacotes que estão instalados globalmente. O python tem um ambiente global, que é onde os pacotes vão parar quando você não está usando um ambiente virtual. 

Imagine que você tem dois projetos:

- Projeto A precisa de dependências X
- Projeto B precisa do dependências Y

 Se você instalar tudo globalmente, vai dar conflito. Com ambientes virtuais, cada projeto tem suas próprias dependências. 

Como criar um ambiente virtual

1. Vá até a pasta do projeto:
2. Crie o ambiente virtual.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfuMzGwoZtrxvhK2r5oIZsMlegP2guU4z8rD6kM84HAXdO24wAPevn17CBP5fK8otOMDdXp26aPC4YK-kWsBvtxiZUjw2rIlc7VJDs5gk71fACeAmrw2gAY4jV6AiGMsDpyrQu-bA?key=jnfZcvbkf1zKPUZCAbeT6ysv)

- -m venv: módulo para criar ambiente virtual.
- fastapienv: nome da pasta que vai conter o ambiente.
1. Ative o ambiente virtual: venv\Scripts\activate

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXenRIORk2DV0j6yATu8_aS3ozPd5_ZIvs9MhHDNt1-k1sob4vx2sSwM_8ki4Rfd4j5Qdsy5D4W6UtNzGuCTmyBb0sCE62M7So1n-CagJbLXkUVtsmqckaSaXOQS59IXfZt_CQhlig?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Os pacotes instalados com pip vão para dentro do ambiente virtual, e não para o ambiente global.

**Instalando as dependências necessárias**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfYWqrxxvBno-GwkVwKYfDHcgI27Z6tzgzMqa3tCc6S_YZq8Zs0gbuFCKNkjkXzzpEr-RQIXsFkmsmTuU2QmGSeSbrqP4s8Q1kOtR3Vr1lVmxu4t6CNE6TADo9U8Yfdqy9NiIAWiw?key=jnfZcvbkf1zKPUZCAbeT6ysv)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfLOduxjHbWwqfVTZU_fWZlmM_SqO4YiRcNrJQXQ9hEsNKKa3zT22RaZ_ONvucylsIEEopqdKBxfzMLIotdmqzPGwGnHDTPtaO9BmyZl_K2vaM7eruV0Rp2lbwPTUIEwQIjE9ndWA?key=jnfZcvbkf1zKPUZCAbeT6ysv)

uvicorn é um servidor web leve utilizado para aplicações web.

___
### **1.2 Primeiros endpoint**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfaYFqZyyqftiYg6PVsOm4Z3a3jPynrPXEzuWvLwkq-4n2BNnBlq4NSdRUvs3BUEdu8vv-ZUeev_21NiKYIUUzLnc5HKzYW0f6KcxSnEdNT8A-CajvoiHmTo35Jn4SnKuxl59xE?key=jnfZcvbkf1zKPUZCAbeT6ysv)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdLQNXR9Zx70G66GXfBt4OhswarzYvUOGy21Uo1ajt9FpxMLxFstdrLbVe3nJd6L-Brr164rMVBhzh4FUjRAc8s-F42tyERxC-D7Mdfm63blLOviG456OIssId0RAclabO1MQw-?key=jnfZcvbkf1zKPUZCAbeT6ysv)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdl0fmtWBWpZVhjF5el9-6FkF5WjD-ZW8TEbXEXam_-ccDeDRFlM-q_m27EWS50fAL_uxBAjiS0eNsP3oJ9xH__m7Kyq2D9bXtuedCq_sFmoZB3oid1y6_puD3ReMF1wk337LByig?key=jnfZcvbkf1zKPUZCAbeT6ysv)

 A ordem dos endpoints é importante, os endpoints com parâmetros devem ficar para o final. O fastapi já se auto documenta. Com o endereço + /docs é mostrado o swagger que é muito bom para testes. E endereço + /redoc é mostrado uma outra documentação que é muito boa para leitura.

**Query parameters**: Quando você não especifica um parâmetro na rota e requisita mais parâmetros na função, os valores são passados pela query de pesquisa.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqIhdF9Kmq1_W0d9D2lfPLzRPMjmUcJjRuL32EaHOcuAayLLnnJZ2qazJt6RPQMPyvrsOJXsQDID2wIcgIQaWMNzgr7DInJBCFlp2QOwznTs-AsauoWEyfnkm_EyHK6HYzTFm67w?key=jnfZcvbkf1zKPUZCAbeT6ysv)

-Casefold: é basicamente o lower mais abrangente.

---
## **1.3 Base model** 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewQbVP7fqWa-W7Fd65dcE31yPqmPByAzkRwjKd5IVovMVzvqul0DhTSQPikjUCFtLfbNDZ9auVoyE4gumQUSsQPZ3pdOJeKZyvNb6lIFPjfn7JhXiyi0IJh7AzoLawhQWtvaBcDw?key=jnfZcvbkf1zKPUZCAbeT6ysv)

 Quando você cria uma classe que herda de basemodel, você está dizendo quero que essa classe:

- Tenha validação automática de tipos
- Aceite dados vindos de um JSON
- Ajude a construir a documentação da API

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfeh3KwBQxfdz3GX51h3ZHR-rgkCLmXT7kD5QzZpeKt-HkZneS5_g_Tqekpq54xGgybAKNuFkzrV6N_LBJX-HOJ6nxT1A1udUglb8h9yjyUTVaOybJMBPOuW2tZKbeyksvA7vB5?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Update

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeeHvJtN9FPIgSBE0uric4hkSGJT748UfLrGf8qoTm4l6Nxe57uT8JkY98jQw4wCn0BXGVRxJdOtRtbFCHkwsURRHd3koYJa987J3uGnvXp3yXqzApkvPJPCwoBbpwmrz725WyG-Q?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Delete

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXevwfj_ZBQHNK2a_Kn4AZi1VW0oNEGHYwt5ml008zVVkS0eLTwBbtuHAMDU6e4UDG2gASXrzszSanxSy9UQXyWYaENufX_J9o73XHUdi2g5U3I36Ge03UOzaccRhhhx_nknabWq?key=jnfZcvbkf1zKPUZCAbeT6ysv)

  
  
  
  
  
  
  
  
  
  
  
  
  

