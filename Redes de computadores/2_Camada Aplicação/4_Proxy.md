
Status: #Concluded 

---
# 1.Proxy/cache Web
 Proxy é um intermediário entre um cliente e um servidor. Você não acessa diretamente o site. O proxy que faz esse acesso.

O proxy tem tanto o papel de cliente como o de servidor. Quando um cliente faz uma requisição, o proxy **recebe essa requisição como um servidor**. Após receber a requisição do usuário, o proxy **encaminha a solicitação ao servidor web de destino**, agora atuando como um cliente.

**Motivos para se usar:**
1. **Segurança e privacidade:** O proxy esconde o IP real.
2. **Cache**: Proxies armazenam cópias de objetos acessados. Ex: Se você acessa o g1.com, o proxy salva uma cópia da resposta. O próximo usuário que acessar, o proxy entrega a cópia sem precisar consultar de novo.
3. **Controle e filtragem de conteúdo:** Por exemplo, uma empresa não quer que funcionários acessem redes sociais. O proxy intercepta a requisição e bloqueia o acesso a facebook.com, twitter.com, etc.
4. **Acesso a conteúdo com restrição geográfica**: Muitos usam proxies ou VPNs para acessar conteúdo que está bloqueado na sua região. O proxy usado é um proxy comercial, que mascara o IP real para enganar o site.
  
![Pasted image 20250508161045](../../attachments/Pasted%20image%2020250508161045.png)

**Proxy transparente** 
O proxy transparente é feito no roteador, ele verifica que uma requisição http foi feita e ele envia para o proxy, que aí sim faz a requisição.

**Get condicional**
Embora possa reduzir os tempos de resposta do ponto de vista do usuário, fazer cache introduz um novo problema — **a cópia de um objeto existente no cache pode estar desatualizada**. 

O HTTP tem um mecanismo que permite que um proxy verifique se seus objetos estão atualizados (get condicional). Uma mensagem HTTP é denominada GET condicional se usar o método GET epossuir uma linha de cabeçalho: ``If-Modified-Since``

 Quando o proxy guarda um objeto ele também guarda a data da última modificação. Quando o proxy precisar de um recurso, ele faz o get condicional:
![Pasted image 20250508161614](../../attachments/Pasted%20image%2020250508161614.png)
 Esse GET condicional está dizendo ao servidor para enviar o objeto somente se ele tiver sido modificado desde a data especificada. 


**Tipos de proxy**
1. **Forward proxy:** É o cliente que usa e fica entre o cliente e a internet. Serve para ocultar o cliente, filtrar acesso, armazenar cache.
2. **Reverse proxy:** É o servidor que usa. Fica entre o mundo externo e o servidor real e serve para:
	- Distribuir carga entre vários servidores
	- Proteger o servidor real (esconde IP real)
	- Fazer cache de respostas prontas

**Níveis de proxy**
1. Proxy na rede local: Muito usado em ambientes corporativos ou educacionais. 
2. Proxy do Provedor de Internet (ISP)
3. Proxy reverso 
