
#Concluded 

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

---
### **2. Preflight**

O Preflight é um mecanismo de segurança do navegador que funciona como uma verificação de segurança antes de enviar a requisição real que você programou.

Antes de fazer uma operação que possa alterar dados no servidor, o navegador pergunta ao servidor se aquela operação é segura.

Quando você escreve um código em JavaScript (usando `axios` ou `fetch`) para fazer uma requisição considerada "complexa", o navegador automaticamente intercepta:

1. **Preflight:** O navegador envia uma requisição leve usando o método HTTP **OPTIONS**.
    - Ele pergunta: "Servidor, você aceita o método `POST` vindo da origem `meusite.com` com o cabeçalho `Content-Type: application/json`?"

2. **A Resposta do Servidor:** O servidor responde e envia os cabeçalhos  de acesso.
		![](../../attachments/Pasted%20image%2020251216071644.png)
		**Access-Control-Allow-Methods:** Define quais verbos HTTP são permitidos para esse recurso. Você pode querer que uma API seja apenas de leitura.
		**Access-Control-Allow-Headers:** Esta linha define quais cabeçalhos customizados o navegador tem permissão para enviar.	
		**Access-Control-Max-Age**: Esta linha define por quanto tempo o navegador pode lembrar dessas regras.

Nem toda requisição dispara um preflight. O navegador só faz isso se a requisição for considerada **"Complexa"**.
