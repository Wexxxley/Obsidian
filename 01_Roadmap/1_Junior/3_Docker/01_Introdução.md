
#Concluded 

---

![](../../../attachments/Pasted%20image%2020251208062224.png)

O Docker é uma plataforma para executar aplicações em unidades leves chamadas **containers**. Você junta a aplicação com todas as suas dependências, permitindo que ela rode da mesma maneira em qualquer lugar: no seu pc, no data center ou cloud.

1. **Contêineres são leves e descartáveis:** Você pode rodar dezenas no seu laptop. Eles não exigem muita memória e não deixam rastros quando removidos.
    
2. **Plataforma Específica:** Um contêiner construído para uma plataforma não rodará em outra nativamente. Em produção, você precisa de servidores correspondentes.
    
3. **Docker Desktop:** Suporta múltiplas plataformas. Ele tem emulação embutida.

---
### **1. Mas o que é um contêiner?**

Um contêiner é como uma caixa: você coloca sua aplicação dentro dele. Dentro dessa caixa, a aplicação "pensa" que tem um computador inteiro só para ela, com seu próprio hostname, endereço IP e disco. Esses recursos são **virtuais**, gerenciados pelo Docker.

O Docker equilibra dois problemas conflitantes da computação:
1. **Isolamento:** Aplicações precisam ser separadas. Se uma travar ou consumir muita CPU, não deve afetar as outras.
2. **Densidade:** Você quer rodar o máximo possível de aplicações em um único computador para economizar dinheiro e recursos.

#### **1.1 A Solução Antiga (Máquinas Virtuais):**
As VMs resolvem o isolamento, mas são pesadas. Cada VM precisa de seu próprio Sistema Operacional completo. Se você tem 3 apps em 3 VMs, você tem 3 sistemas operacionais consumindo memória e CPU só para manter a VM ligada.
#### **1.2 A Solução Docker (Contêineres):**
Cada contêiner tem seu ambiente virtual isolado. Mas todos compartilham o mesmo Sistema Operacional do computador. Isso os torna extremamente leves. V

![](../../../attachments/Pasted%20image%2020251207141954.png)

---
### **2. E o que é uma imagem?**

Uma imagem é um modelo **somente leitura** com instruções para criar um contêiner Docker. Frequentemente, uma imagem é baseada em outra imagem, com alguma personalização adicional. Por exemplo, você pode construir uma imagem baseada na imagem `ubuntu`, mas que instala o servidor web Apache e sua aplicação, bem como os detalhes de configuração necessários para fazer sua aplicação rodar.

Você pode criar suas próprias imagens ou usar apenas aquelas criadas por outros e publicadas em um registro. Para construir sua própria imagem, você cria um **Dockerfile** com uma sintaxe simples para definir os passos necessários para criar a imagem e executá-la. Cada instrução em um Dockerfile cria uma camada na imagem. Quando você altera o Dockerfile e reconstrói a imagem, apenas as camadas que mudaram são reconstruídas. Isso é parte do que torna as imagens tão leves, pequenas e rápidas quando comparadas a outras tecnologias de virtualização.