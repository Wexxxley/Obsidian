
#Concluded 

---

Sistema de reatividade do Vue. O DOM é atualizado de forma autônoma sempre que as variáveis em memória sofrem alterações.
### **1. COM REF**
![500](../../../attachments/Pasted%20image%2020260823142734.png)
- **.value:** usado para acessar o valor das variáveis reativas.
- **Chaves duplas**: sintaxe Mustache. usado para extrair texto e escrever funções js no HTML.
- **@click**: diretiva que atua como um listener. A interação do usuário aciona a função.
- Você não é obrigado a definir o tipo explicitamente. Quando você fornece um valor inicial, o compilador do TS executa a inferência de tipo. 

A declaração explícita torna-se  necessária quando o tipo não pode ser inferido.
- **Arrays:** `const lista = ref<string[]>(['Item 1', 'Item 2']);`
- **Múltiplos Tipos:** `const id = ref<string | number>(123);` aceita números e strings.
- **Tipagem com Null:** `const token = ref<string | null>(null);` Utilizar null é a abordagem recomendada quando você deseja declarar que o estado está vazio por enquanto.

---
### **2. COM REACTIVE**

A principal diferença em relação ao ref é que a reatividade gerada pelo reactive é profunda. Isso significa que, se você instanciar um objeto com múltiplos níveis de aninhamento (como objetos dentro de objetos), todas as propriedades em todos os níveis serão monitoradas.
-  Permite que o acesso ocorra através da notação de ponto.

**Limitações**
1. **Bloqueio de Tipos Primitivos:** rejeita a injeção de tipos primitivos isolados.
2. **Perda de Reatividade na Desestruturação:** Se você tentar extrair uma propriedade do objeto reativo utilizando desestruturação, a variável será extraída como um dado estático.
![550](../../../attachments/Pasted%20image%2020260823151229.png)