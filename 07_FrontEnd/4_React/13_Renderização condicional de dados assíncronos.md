
#Concluded 

---
### **1. Deixando os dados assíncronos**

Até agora, utilizamos dados síncronos. Em aplicações reais, os dados vêm de uma API remota e chegam de forma assíncrona. Antes de conectarmos a uma API real, simularemos esse comportamento para entender o ciclo de renderização assíncrono.

O objetivo técnico é transformar a lista `stories` de um estado inicial síncrono para um estado que começa vazio e é preenchido após a resolução de uma _Promise_.

**Simulação da API**: Foi criado uma função fora do componente que retorna uma Promise.
![](../../attachments/Pasted%20image%2020251125133327.png)

**Inicialização do Estado**: Mudamos a inicialização de `const [stories, setStories]`. Agora a aplicação inicia com uma lista vazia. 

**useEffect:**  Introduzimos o hook useEffect para disparar a busca dos dados. Note que o Array de dependências vazio, isso garante que essa busca aconteça apenas **uma vez**, quando o componente é montado (aparece na tela pela primeira vez) .
![](../../attachments/Pasted%20image%2020251125134436.png)

---
### 4. Renderização Condicional

Com a introdução de dados assíncronos, criamos um problema de Experiência do Usuário: durante o atraso da requisição, a aplicação parece travada. Vamos focar em fornecer feedback visual (Loading e Erro) utilizando renderização condicional no JSX.

**Loading state:** Introduzimos um estado booleano `isLoading` para rastrear o status da requisição.

**Error state:** Em aplicações reais, requisições falham. Introduzimos o estado `isError` para capturar falhas na Promise.

![](../../attachments/Pasted%20image%2020251125140949.png)

- **Operador Ternário (`? :`):** Ideal para situações "Se/Senão". Se `isLoading` for verdadeiro, renderiza o parágrafo de carregamento; caso contrário, renderiza o componente `List`.
    
- **Operador Lógico AND (`&&`):** Ideal para situações "Se/Nada". Se `isError` for verdadeiro, renderiza a mensagem de erro; caso contrário, não renderiza nada.  

![](../../attachments/Pasted%20image%2020251125140933.png)

