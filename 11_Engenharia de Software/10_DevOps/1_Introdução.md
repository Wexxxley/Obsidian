
#Concluded 

---
### **1. Antes do DevOps**

Em organizações tradicionais, a área de TI era frequentemente dividida em dois grupos :
	   
1. **Desenvolvimento (Dev):** Focado em criar funcionalidades (programadores, analistas, arquitetos).
2. **Operações (Ops):** Focado em manter o sistema estável em produção (administradores de rede, BDs, suporte, infraestrutura).

O problema dessa divisão era um "muro" entre as equipes. A equipe de Ops, muitas vezes, só tomava conhecimento de um novo sistema na véspera da implantação (entrega). Isso causava atrasos de meses, pois só nesse momento problemas de infraestrutura, desempenho, segurança ou incompatibilidade eram descobertos. 

---
### **2. O Conceito de DevOps**

<mark style="background: #ADCCFFA6;">DevOps visa unificar as culturas de Desenvolvimento e Operações com o objetivo de permitir a implantação (deployment) mais rápida e menos traumática.</mark>
    
- A ideia é que a implantação deixe de ser um evento estressante e passe a ocorrer em qualquer dia útil, de forma automatizada e sem que os clientes percebam (exceto pelas novas funcionalidades).
    
- **Automatização Total:** DevOps defende a **automatização de tudo** no processo de entrega: build, testes, configuração e ativação de servidores, carga de banco de dados, etc. O objetivo é que a implantação seja "tão simples como apertar um botão" .

---
### **3. Sistema de Controle de Versões**

Como software é desenvolvido em equipe, precisamos de um servidor central para armazenar o código-fonte, permitindo que os desenvolvedores colaborem. Um VCS mantém o histórico de todas as versões dos arquivos (código, documentação, configuração, etc.). Isso permite recuperar versões antigas de um arquivo
    
1. **VCS Centralizado:** Existe u **único servidor central** que armazena o repositório principal.

2. **VCS Distribuído:** Cada desenvolvedor possui um servidor completo e um repositório inteiro em sua máquina local.
	- **Trabalho Offline:** Você pode fazer _commits_ e gerenciar versões sem estar conectado à rede.
	- **Commits Frequentes e Rápidos:** Como os _commits_ são locais, eles são muito rápidos e podem ser feitos com mais frequência.
        
**Multirepos vs. Monorepos:**

1. **Multirepos:** A abordagem tradicional, onde cada projeto ou sistema tem seu próprio repositório separado (ex: `empresa/sistema1`, `empresa/sistema2`).
      
2. **Monorepos:** Uma abordagem adotada por grandes empresas (Google, Facebook) onde **todos** os projetos da organização residem em um **único repositório gigante**, organizados em subdiretórios.
    - **Desvantagem:** Requer ferramentas especializadas para lidar com o tamanho imenso da base de código.
    - **Vantagens:** Fonte única da verdade, incentiva reúso, mudanças que afetam múltiplos projetos podem ser feitas em um único _commit_ e facilita refatorações em larga escala.    
