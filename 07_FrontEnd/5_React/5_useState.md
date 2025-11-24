
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

- No exemplo da busca, o novo valor não está dentro do React; ele está vindo do mundo externo (do navegador), gerado pela ação do usuário de digitar.
- O navegador empacota essa informação (quem disparou, qual o novo texto) dentro do objeto `event`.
- Precisamos do parâmetro `event` para acessar `event.target.value`.
    

JavaScript

```
// O novo valor vem de fora (do evento do navegador)
const handleSearch = (event) => {
  // "React, pegue o que o usuário digitou AGORA lá no HTML"
  setSearchTerm(event.target.value);
};
```

### 2. O Caso do Botão (Lógica Interna / Closure)

No exemplo do contador, o novo valor é calculado com base em um dado que **já existe** na memória do componente.

- **O Contexto:** A variável `count` já está disponível no escopo da função `App`.
    
- **A Lógica:** A operação é matemática (`count + 1`). Não precisamos saber coordenadas do mouse ou detalhes do clique para somar 1.
    
- **Closure:** A função `handleIncrement` tem acesso direto à variável `count` porque foi criada dentro do mesmo escopo.
    

JavaScript

```
// O novo valor é calculado internamente (matemática simples)
const handleIncrement = () => {
  // "React, pegue o valor que você JÁ TEM na memória e some 1"
  setCount(count + 1);
};
```

### Resumo Técnico

|**Cenário**|**Origem do Novo Valor**|**Precisa de event?**|**Por quê?**|
|---|---|---|---|
|**Digitar Texto**|**DOM (HTML)**|**Sim**|O React precisa ler o atributo `value` do elemento HTML que disparou o evento para saber o que foi digitado.|
|**Incrementar**|**Memória (JS)**|**Não***|O valor anterior (`count`) já está acessível via _Closure_ (escopo da função). O evento de clique não traz dados matemáticos.|

_*Nota técnica: O evento de clique também é enviado para o `handleIncrement` (o React sempre envia), mas nós optamos por ignorá-lo (não declarando o parâmetro) porque ele não é útil para a lógica de somar._

---

Diga **next** para voltarmos ao fluxo do livro em **React Controlled Components**, onde aplicaremos esse conceito de `event` para corrigir um comportamento do input.

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
    
