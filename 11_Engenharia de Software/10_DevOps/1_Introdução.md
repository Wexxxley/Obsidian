

---
### **1. Antes do DevOps**

Em organizações tradicionais, a área de TI era frequentemente dividida em dois grupos :
	   
1. **Desenvolvimento (Dev):** Focado em criar funcionalidades (programadores, analistas, arquitetos).
2. **Operações (Ops):** Focado em manter o sistema estável em produção (administradores de rede, BDs, suporte, infraestrutura).

O problema dessa divisão era um "muro" entre as equipes. A equipe de Ops, muitas vezes, só tomava conhecimento de um novo sistema na véspera da implantação (entrega). Isso causava atrasos de meses, pois só nesse momento problemas de infraestrutura, desempenho, segurança ou incompatibilidade eram descobertos. 

---
### **2. O Conceito de DevOps**

<mark style="background: #ADCCFFA6;">DevOps é um que visa unificar as culturas de Desenvolvimento e Operações com o objetivo de permitir a implantação (deployment) mais rápida e menos traumática.</mark>
    
- A ideia é que a implantação deixe de ser um evento estressante e passe a ocorrer em qualquer dia útil, de forma automatizada e sem que os clientes percebam (exceto pelas novas funcionalidades).
    
- **Equipes Integradas:** Um profissional de Operações pode participar dos times ágeis, ajudando a antecipar problemas de infraestrutura, desempenho ou segurança desde os primeiros sprints.
    
- **Automatização Total:** DevOps defende a **automatização de tudo** no processo de entrega: build, testes, configuração e ativação de servidores, carga de banco de dados, etc. O objetivo é que a implantação seja "tão simples como apertar um botão" .

---
### **Princípios Chave**

- Crie um processo **repetível e confiável** para entrega de software.
    
- **Automatize tudo** que for possível.
    
- Mantenha **tudo em um sistema de controle de versões** (não apenas o código-fonte, mas também scripts de build, configuração, documentação, etc.).
    
- **Se um passo causa dor, execute-o com mais frequência** (ex: integração de código causa dor? Faça-a continuamente em pequenas partes, o que veremos como Integração Contínua) .
    
- **"Concluído" significa "pronto para entrega"** (não "pronto, mas falta testar, documentar...") .
    
- **Todos são responsáveis** pela entrega (quebrando os silos) .