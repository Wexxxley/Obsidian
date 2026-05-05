
#Concluded 

---
Um cookie é um pequeno pedaço de dados que um servidor envia para o navegador de um usuário. O navegador pode armazenar cookies, criar novos cookies, modificar os existentes e enviá-los de volta ao mesmo servidor com solicitações posteriores. Os cookies permitem que os aplicativos da web armazenem quantidades limitadas de dados e lembrem informações de estado.

Normalmente, o servidor usará o conteúdo dos cookies HTTP para determinar se diferentes solicitações vêm do mesmo navegador.
![600](../../attachments/Pasted%20image%2020251216073337.png)

Os cookies são utilizados principalmente para três fins:

- **Gestão de sessão**: Status de login do usuário, conteúdo do carrinho de compras,ou quaisquer outros detalhes da sessão do usuário que o servidor precise lembrar.
- **Personalização**: Preferências do usuário, como idioma de exibição e tema da interface do usuário.
- **Rastreamento**: Registrar e analisar o comportamento do usuário. Por exemplo, empresas como o Google Ads utilizam cookies para registrar quais sites você visitou e quais produtos clicou, criando um perfil de consumo para exibir anúncios personalizados baseados no seu histórico.    

**Cookies e a privacidade**
Cookies permitem rastrear seu comportamento online. Se você preenche formulários com nome, e-mail, cpf, esses dados podem ficar associados a cookies. Empresas de propaganda (como o Google Ads) usam cookies para montar um perfil sobre você e exibir anúncios personalizados.

1. **Set-Cookie na resposta HTTP:** Quando você acessa um site pela primeira vez, o servidor envia um cookie com um ID e Esse cookie é armazenado no seu navegador.
2. **Cookie na requisição HTTP:** Quando você visitar o mesmo site de novo, o navegador envia o cookie, o site assim sabe quem é você.
3. **Arquivo de cookie no computador do usuário**: O navegador salva os cookies em arquivos locais. 
4. **Banco de dados do site:** O site guarda informações sobre cada visitante usando o ID do cookie.