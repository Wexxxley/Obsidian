


---
O **CORS (compartilhamento de recursos entre origens)** pode apresentar desafios para os aplicativos e APIs.

A segurança do navegador geralmente impede uma página da Web de fazer solicitações para outro domínio. Essa restrição é chamada de _política de mesma origem_. A política impede que um site mal-intencionado leia dados confidenciais de outro site. No entanto, às vezes, talvez seja interessante permitir que outros sites chamem sua API Web. CORS é um padrão W3C que direciona um servidor para permitir algumas solicitações entre origens e rejeitar outras.

[](https://learn.microsoft.com/pt-br/entra/identity/app-proxy/application-proxy-understand-cors-issues#identify-a-cors-issue)

## Identificar um problema de CORS

Duas URLs terão a mesma origem se tiverem esquemas, hosts e portas idênticos ([RFC (Solicitação de Comentários) 6454](https://tools.ietf.org/html/rfc6454)), como neste exemplo:

- `http://contoso.com/foo.html`
- `http://contoso.com/bar.html`

Essas URLs têm origens diferentes das duas anteriores:

- `http://contoso.net`: domínio diferente
- `http://contoso.com:9000/foo.html`: porta diferente
- `https://contoso.com/foo.html`: esquema diferente
- `http://www.contoso.com/foo.html`: subdomínio diferente

A política de mesma origem impede que os aplicativos acessem recursos de outras origens, a menos que usem os cabeçalhos de controle de acesso corretos. Se os cabeçalhos de CORS estiverem ausentes ou incorretos, as solicitações entre origens falharão.

Você pode identificar problemas de CORS usando as ferramentas de depuração do navegador:

1. Abra o navegador e vá para o aplicativo Web.
2. Selecione a chave **F12** para abrir o console de depuração no DevTools.
3. Tente reproduzir a transação e examine a mensagem do console. Uma violação de CORS produz um erro de console sobre a origem.