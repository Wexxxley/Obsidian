
#Concluded 

---
O Node.js possui um ecossistema de pacotes centralizado através do **NPM (Node Package Manager)**. O NPM não é apenas um repositório, mas uma CLI (Command Line Interface) que gerencia o ciclo de vida das dependências e a execução de scripts do projeto.
![300](../../../../attachments/Pasted%20image%2020251121090514.png)

---
### **1. package.json**
Este arquivo declara o que o seu projeto precisa e como ele deve se comportar. Ele é escrito e mantido por humanos (desenvolvedores).
- **Função:** Define os requisitos mínimos e intervalos de compatibilidade.    

![](../../../../attachments/Pasted%20image%2020251121090553.png)

---
### **2. package-lock.json**

Enquanto o `package.json` lista apenas suas dependências diretas, o `package-lock.json` lista **tudo**, incluindo as dependências das dependências (nested dependencies). Garante que o servidor de produção tenha exatamente os mesmos bytes instalados que a sua máquina local.    

![](../../../../attachments/Pasted%20image%2020251121091351.png)




    