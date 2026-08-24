
#Concluded 

---
### **1. Componente Reutilizável**

O componente Search atual tem dois defeitos principais de arquitetura:

1. **Acoplamento ao Domínio:** Ele "sabe" que é uma busca (o label é fixo como "Search").
2. **Duplicação de IDs:** Se renderizarmos dois componentes `Search` na mesma página, teremos dois elementos HTML com `id="search"`. Isso viola a regra do HTML de IDs únicos.
 
Vamos renomear o componente tornar dinâmicas todas as propriedades que o prendem a um caso de uso específico. 
![](../../../../../attachments/Pasted%20image%2020251124175307.png)
- **Parâmetro Padrão:** Na assinatura da função, `type = 'text'` garante que o componente funcione mesmo se o desenvolvedor esquecer de passar a prop `type`.
- **ID Dinâmico:** A prop `id` é usada tanto no atributo `htmlFor` do label quanto no `id` do input, garantindo que o vínculo de acessibilidade seja único para cada instância.

Agora precisamos atualizar o `App` para usar esse novo componente genérico, passando os dados específicos da busca.
![](../../../../../attachments/Pasted%20image%2020251124180057.png)

Ao generalizar, aumentamos a API de Superfície do componente (ele precisa de mais props para funcionar). Perdemos a simplicidade de <Search /> (que já sabia tudo o que tinha que fazer), mas ganhamos um componente que pode criar qualquer campo de texto na aplicação.

---
### 2. Componentes com conteúdo interno

Até agora, tratamos nossos componentes  como tags de fechamento automático, passando dados exclusivamente através de atributos (props). No entanto, elementos HTML nativos frequentemente possuem conteúdo interno. O React permite imitar esse comportamento utilizando a prop especial **`children`**.

No componente `App`, em vez de passar o texto "Search" através de uma prop explícita `label`, nós o passamos entre as tags de abertura e fechamento do componente `InputWithLabel`.
![](../../../../../attachments/Pasted%20image%2020251124180728.png)

Agora precisamos atualizar o `InputWithLabel` para renderizar o conteúdo que foi passado "dentro" dele. O React injeta esse conteúdo automaticamente na prop `children`.
![](../../../../../attachments/Pasted%20image%2020251124180745.png)
- A API do componente fica mais intuitiva, comportando-se como elementos nativos do DOM.

