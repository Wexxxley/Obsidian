
#Concluded 

---

### **1. Extraindo componentes**
À medida que a aplicação cresce, manter toda a lógica no componente `App` torna-se insustentável. O processo de refatoração envolve extrair partes da UI para componentes dedicados.

**Extração do Componente List**
![](../../attachments/Pasted%20image%2020251123180211.png)

**Extração do Componente Search**
![](../../attachments/Pasted%20image%2020251123180227.png)

O componente App passa a atuar como um orquestrador, instanciando os componentes filhos.
![](../../attachments/Pasted%20image%2020251123180312.png)
![](../../attachments/Pasted%20image%2020251123180151.png)

---
### **2. Component Tree**

- App é o componente pai ou Root.
- List e Search são filhos de App e irmãos entre si.
- Componentes que não renderizam outros componentes são chamados de folhas.
	![](../../attachments/Pasted%20image%2020251123180611.png)

---
