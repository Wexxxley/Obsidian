

---
### **1. HTTP Cache**

O cache HTTP é um mecanismo essencial que armazena uma resposta associada a uma solicitação e a reutiliza para solicitações subsequentes. 

A **reutilização** de respostas armazenadas apresenta várias vantagens funcionais:

1. **Latência Reduzida:** A resposta é entregue mais rapidamente, pois a solicitação não precisa ser roteada ao servidor de origem. O exemplo típico é o cache armazenado no próprio navegador.
    
2. **Redução da Carga do Servidor de Origem:** Quando uma resposta é reutilizável, o servidor de origem não precisa processar a solicitação.

### 2. Tipos de cache HTTP

**Cache privado**
Um cache privado é um cache vinculado a um cliente específico, normalmente um cache de navegador. Um cache privado pode armazenar uma resposta personalizada para esse usuário.

Você deve especificar uma diretiva `private`.
![](../../attachments/Pasted%20image%2020251119133603.png)
Os conteúdos personalizados são geralmente controlados por cookies, mas a presença de um cookie nem sempre indica que é privado e, portanto, um cookie por si só não torna a resposta privada.

**Cache compartilhado**
O cache compartilhado está localizado entre o cliente e o servidor e pode armazenar respostas que podem ser compartilhadas entre os usuários. E os caches compartilhados podem ser subdivididos em **caches de proxy** e **caches gerenciados**.

**Caches de proxy**
Além da função de controle de acesso, alguns proxies implementam cache para reduzir o tráfego fora da rede. Isso geralmente não é gerenciado pelo desenvolvedor do serviço, portanto, deve ser controlado por cabeçalhos HTTP apropriados e assim por diante.


Por outro lado, se um proxy de ponte [TLS](https://developer.mozilla.org/pt-BR/docs/Glossary/TLS) descriptografa todas as comunicações de maneira intermediária instalando um certificado de uma [CA (entidade certificadora)](https://developer.mozilla.org/en-US/docs/Glossary/Certificate_authority) gerenciada pela organização no PC e executa o controle de acesso, etc. — é possível ver o conteúdo da resposta e armazená-la em cache. No entanto, como [CT (transparência do certificado)](https://developer.mozilla.org/en-US/docs/Web/Security/Certificate_Transparency) se tornou comum nos últimos anos e alguns navegadores permitem apenas certificados emitidos com um SCT (carimbo de data e hora do certificado assinado), esse método exige a aplicação de uma política empresarial. Em um ambiente tão controlado, não há necessidade de se preocupar com o cache do proxy estar "desatualizado e não atualizado".