
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
### **3. Arrow functions**

O livro propõe a refatoração das declarações de função padrão para **Arrow Functions**, alinhando-se aos padrões modernos de JavaScript.

**Refatoração para Arrow Functions**
![](../../attachments/Pasted%20image%2020251123182606.png)

**Retorno Implícito**
Se o componente não possui lógica antes do return , pode-se omitir as chaves {} e a palavra-chave return. Esta é uma boa forma para componentes "stateless" ou puramente visuais, tornando o código mais limpo.
![](../../attachments/Pasted%20image%2020251123183448.png)


