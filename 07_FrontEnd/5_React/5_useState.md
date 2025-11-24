
#Concluded 

---
Enquanto props são usadas para passar informações, o state é <mark style="background: #ADCCFFA6;">usado para gerenciar informações que mudam ao longo do tempo dentro de um componente</mark>. O State persiste os dados na memória do React entre renderizações.

---
### **1. Exemplo com input** 
![](../../attachments/Pasted%20image%2020251124063152.png)
1. **Interação:** O usuário digita, disparando `handleChange`.
2. **Atualização:** `setSearchTerm` é chamado com o novo valor.
3. **Re-renderização:** O React detecta a mudança de estado e re-executa a função do componente `Search`. O valor atualizado de `searchTerm` é refletido .
![300](../../attachments/Pasted%20image%2020251124081903.png)

---
### **2. Exemplo contador**

![](../../attachments/Pasted%20image%2020251124104008.png)
![](../../attachments/Pasted%20image%2020251124103903.png)

---
### **3. Exemplo mostrar detalhes**

![](../../attachments/Pasted%20image%2020251124131323.png)
![150](../../attachments/Pasted%20image%2020251124105032.png)
![200](../../attachments/Pasted%20image%2020251124105049.png)

---

### **4. Diferenças de uso**

A diferença fundamental está na **origem do novo dado**. "De onde vem o valor que eu quero salvar?"

**Exemplo da busca**: No exemplo da busca, o novo valor não está dentro do React; ele está vindo do mundo externo (do navegador), gerado pela ação do usuário de digitar.
- O navegador empacota essa informação dentro do objeto `event`. Precisamos do parâmetro `event` para acessar `event.target.value`.

**Exemplo do contador:** No exemplo do contador, o novo valor é calculado com base em um dado que já existe na memória do componente.
- A função `handleIncrement` tem acesso direto à variável `count` porque foi criada dentro do mesmo escopo.
m comportamento do input.
