
#Concluded 

---
### **1. React State**

Enquanto props são usadas para passar informações, o state é usado para gerenciar informações que mudam ao longo do tempo dentro de um componente.

**Hook useState:** O `useState` é um React Hook que permite adicionar estado a componentes funcionais. O State persiste os dados na memória do React entre renderizações.
![](../../attachments/Pasted%20image%2020251124063152.png)

1. **Interação:** O usuário digita, disparando `handleChange`.
2. **Atualização:** `setSearchTerm` é chamado com o novo valor.
3. **Re-renderização:** O React detecta a mudança de estado e re-executa a função do componente `Search`. O valor atualizado de `searchTerm` é refletido no JSX .

![](../../attachments/Pasted%20image%2020251124081903.png)

---
### **2. A Mecânica do useState**

Quando você escreve:
![](../../attachments/Pasted%20image%2020251124065047.png)
Está acontecendo o seguinte:

1. **React.useState('')**: Você solicita ao React um espaço na memória associado a este componente específico. O valor inicial é ''.
2. **O Retorno**: O Hook retorna um array com exatamente dois itens:
    - **searchTerm:** O valor atual armazenado na memória do React. (Leitura).
    - **setSearchTerm:** Uma função específica para atualizar esse valor. (Escrita).
    

**O Fluxo de Atualização:**
1. O usuário digita no input. O evento `onChange` dispara.
    
2. Sua função `handleChange` captura o texto (`event.target.value`).
    
3. Você chama setSearchTerm('novo texto'). Ao chamar essa função de atualização, o React marca o componente como "sujo" (precisa de atualização).
    
4. O React executa a função `App` inteira novamente.
    
5. Desta vez, quando a linha `const [searchTerm...] = useState('')` é executada, o React ignora o valor inicial `''` e devolve o valor que foi salvo na memória.
    
6. O JSX é retornado com o novo valor e o navegador atualiza o HTML.
    
