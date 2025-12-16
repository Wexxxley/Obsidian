

---
### **1. CORS (Cross-Origin Resource Sharing)**

A segurança do navegador geralmente impede uma página da Web de fazer solicitações para outro domínio. Essa restrição é chamada de política de mesma origem. A política impede que um site mal-intencionado leia dados confidenciais de outro site. No entanto, às vezes, talvez seja interessante permitir que outros sites chamem sua API Web. 

![](../../attachments/Pasted%20image%2020251216070635.png)

Duas URLs terão a mesma origem se tiverem esquemas, hosts e portas idênticos:
- `http://contoso.com/foo.html`
- `http://contoso.com/bar.html`

Essas URLs têm origens diferentes das duas anteriores:
- `http://contoso.net`: domínio diferente
- `http://contoso.com:9000/foo.html`: porta diferente

Mas, analisando essas variações, como lidamos com situações em que nosso front-end precisa consumir uma API com url diferente sem termos problemas com o CORS? 

Ao enviar uma requisição para uma API de origem diferente, o servidor precisa retornar um header chamado **Access-Control-Allow-Origin**. Dentro dele, é necessário informar as diferentes origens que serão permitidas, por exemplo:
- `Access-Control-Allow-Origin: http://localhost:3000/`

É possível permitir o acesso de qualquer origem utilizando do símbolo **asterisco**:
- `Access-Control-Allow-Origin: *`

![](../../attachments/Pasted%20image%2020251216071644.png)
**Access-Control-Allow-Methods:** Esta linha define quais verbos HTTP são permitidos para esse recurso. Você pode querer que uma API seja apenas de leitura para sites externos.

**Access-Control-Allow-Headers:** Esta linha define quais cabeçalhos customizados o navegador tem permissão para enviar.

**Access-Control-Max-Age**: Esta linha define por quanto tempo (em segundos) o navegador pode lembrar dessas regras.
