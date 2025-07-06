
___
# 1 HTTP

 As páginas Web são referenciadas pela **URL**(Uniform Resource Locator), como `chat.deepseek.com`.  Uma **URI**(Uniform Resource Identifier) é a URL mais o HTTP.

**HTTP**: Protocolo da camada de aplicação da Web. Usa o modelo cliente/servidor.
- O Cliente (browser) solicita, o servidor envia os objetos e o browser os apresenta.
- Protocolo “sem estado”, o servidor não mantém informação sobre os pedidos passados.
- Utiliza o protocolo de transporte TCP

**HTTP Persistente:** técnica onde a mesma conexão TCP é reutilizada para enviar vários pedidos HTTP, em vez de abrir uma nova conexão para cada requisição. Antes o HTTP era não persistente, a cada requisição o navegador abria uma conexão TCP, fazia a requisição e fechava a conexão.

---
## **1.1 Formato do Request e response message**

**Response message**

![Pasted image 20250508160317](../../attachments/Pasted%20image%2020250508160317.png)

- CR(Carriage return): retorno do cursor.
- LF(Line Feed): Pula a linha.
- SP(Space): espaço em branco.

**Com método get**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcyujfV7oaza6FHi6b0fL9V616AIvE9KT8DGsxOrcc9auf5umHYGcpG8YT5CpaVU7Ml3cGPQxCXnbauDhgefOwtUQMica6ZF6Qvy5Vtyjrxf3GTU1uDd-lDp1GaKeklK6J4JpJXPQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Com método Put**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewOFt0a4Pe9a_5Jo1JgCrozaMzTDvK4zXIbQdGsfDauSrPLBQN5OCLhJEeFem7rr4NjGIK0r1sZkbSTCFTwMUYLUY9xiZMyrB3LMb99NEQRvZ2U1vBg3W0GHF50JswLKLsNO38TA?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Formato do Response message**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfDmPpFdskH2rw36i9oGJ_mKfY4EdYbALCl6NvQtc_jrz6STrJsxdzjVKpxRH69sFsQIn09EY3XTyB6Rg3Ke9o4eNQhU_tsXHMt4zaXT_Jb8IHOHjgI496KzWLulyo8yjhOIqBOdg?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Códigos de status**
São códigos utilizados nas respostas http para informar ao cliente se a requisição foi bem sucedida, se ocorreu algum erro, etc.
- **200 OK:** requisição bem-sucedida e a informação é entregue com a resposta. 
- **400 Bad Request:** código genérico de erro. 
- **404 Not Found:** o documento requisitado não existe no servidor. 
- **505 HTTP Version Not Supported:** a versão do protocolo HTTP  não suportada pelo servidor.

___
# **2 Cookies**

 São pequenos arquivos que os sites colocam no navegador do usuário para armazenar informações entre acessos.

**O que os cookies podem trazer?**
1. Permite que você continue logado mesmo fechando e abrindo o navegador.
2. Permite persistir o carrinho de compras mesmo você estando deslogado.
3. Permite recomendações personalizadas, o site lembra o que você viu, comprou, pesquisou e sugere conteúdos parecidos.

**Cookies e a privacidade**
Cookies permitem rastrear seu comportamento online. Se você preenche formulários com nome, e-mail, cpf, esses dados podem ficar associados a cookies. Empresas de propaganda (como o Google Ads) usam cookies para montar um perfil sobre você e exibir anúncios personalizados.

1. **Linha de cabeçalho Set-Cookie na resposta HTTP:** Quando você acessa um site pela primeira vez, o servidor envia um cookie com um ID e Esse cookie é armazenado no seu navegador.
2. **Linha de cabeçalho Cookie na requisição HTTP:** Quando você visitar o mesmo site de novo, o navegador envia o cookie, o site assim sabe que mé você.
3. **Arquivo de cookie no computador do usuário**: O navegador salva os cookies em arquivos locais. Esse arquivo é usado para saber quais cookies mandar para quais sites.
4. **Banco de dados do site:** O site guarda informações sobre cada visitante usando o ID do cookie.