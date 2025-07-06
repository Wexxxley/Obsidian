
---

Em APIs, a segurança é dividida em autenticação e autorização 

### **1. Autenticação com JWT**

 Autenticação é o processo de confirmar a identidade de um usuário. Existem diversas abordagens, a mais comum é o uso de tokens para autenticar as requisições. 

#### **1.1 JWT (JSON Web Token)**

O JWT é um padrão de token. Ele permite que os sistemas garantam que o remetente de uma solicitação está autenticado sem precisar armazenar informações de sessão no servidor. 

Podemos ver na imagem abaixo um cenário onde será requisitado um token, que irá devolver um token válido para que nas próximas requisições seja utilizado.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdsTzvPneiOPOShl6aj3gIaZMPsMnUjRGCGSx0JYgOIQeQ4S4B6ijq2V_VnvRu_6OdYyP3WX8i3RTvqTmZYCmNCQJ8rbh0VpwwfLjOjlcG9w36MSFvYa0rRCfWVmgWHaDHI4VVRsGFa8Febkol4RCdo4taU?key=SZHaDLu24DLXyFgiFaRNLA)

Quando um usuário se autentica, o servidor cria o JWT. O JWT é enviado ao cliente, que geralmente o armazena localmente e o envia em cada requisição subsequente ao servidor. Em cada requisição, o servidor decodifica o JWT, verifica a assinatura e valida as claims (como a data de expiração). 

  

O JWT é um token composto por três partes principais, separadas por pontos:

1. **Header:**  Contém metadados sobre o token, incluindo o tipo de token e o algoritmo de criptografia usado para assinar o token.
2. **Payload:** Contém as claims, que são informações sobre o usuário e dados específicos da aplicação.
	- Padrões definidos pelo JWT, como iss(emissor), exp(expiração) e sub(assunto).
	- Claims criadas pelo desenvolvedor.
3. **Signature**: assinatura do token

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpVIz9DyfCPhzHylztCdImzjYzncXs8B1PXBuOEzRcuCuYbtfleQOzdVyTIhp8o2MRZr5a7G4un2l45SsnhgCGA-4fPgQuuAAIOxW0s1Y7uBhJjmmqHV_x7C9WuPYL6AAS7oOomVaO0wpaN_cbxZWfO_k?key=SZHaDLu24DLXyFgiFaRNLA)

**Boas Práticas**
1. **Expiração Curta e Refresh Tokens:** Use tokens de acesso com uma expiração curta e tokens de atualização para permitir a renovação segura do token.
2. **HTTPS:** Use HTTPS para proteger o token durante a transmissão.
3. **Armazenamento Seguro no Cliente:** Guarde o JWT em um local seguro.
4. **A chave secreta** deve ser mantida no servidor e nunca compartilhada, pois é o que garante a autenticidade do token. 

Usamos jwt no python com ``pip install pyjwt``
