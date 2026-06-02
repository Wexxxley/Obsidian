


---
### **1. ViewModel**

A viewModel deve:
- **Reter o Estado:** Ele deve armazenar todos os dados que a tela precisa exibir. 
- **Processar Eventos da UI:** Ele deve conter funções públicas que a tela possa chamar quando o usuário interagir (ex: `adicionarAoCarrinho()`, `realizarBusca()`).
- **Gerenciar Tarefas Assíncronas:** Ele deve iniciar buscas no banco de dados ou chamadas de rede. 
- **Formatar Dados para a View:** Se o banco de dados retorna uma data como `2026-05-06T15:32:05`, o ViewModel deve formatá-la para `06/05/2026`.

![](../../../attachments/Pasted%20image%2020260506153730.png)
Observe o padrão de **Backing Property**. Nós criamos um estado mutável e privado que só o ViewModel pode alterar, e expomos uma versão pública e somente leitura para a tela.

---
### **2. Flow e StateFlow**

Ambos os conceitos, Flow e StateFlow, pertencem à API de Corrotinas da linguagem Kotlin. Eles são a implementação para o paradigma de programação reativa, cujo princípio básico consiste em emitir uma sequência de dados ao longo do tempo de forma assíncrona para componentes que se inscrevem para observá-los.

**Flow**: O Flow é uma estrutura classificada como um fluxo de dados assíncrono frio.
- **Comportamento Frio:** Indica que o código encapsulado dentro de um construtor de um Flow não é acionado no momento de sua criação. A execução da lógica (como acessar um banco de dados) permanece inerte e só é iniciada no exato instante em que um consumidor invoca a função de coleta (`collect`).
- **Ausência de Estado:** O `Flow` não possui retenção de memória. Ele apenas computa, emite o valor pelo canal e o descarta imediatamente da sua responsabilidade.

**StateFlow**: Ele é classificado como um fluxo quente e atua explicitamente como um detentor de estado.
- **Comportamento Quente:** A existência e a retenção dos dados em memória independem de existirem componentes observando-o. O StateFlow está sempre ativo em memória a partir do momento de sua criação.
- **Valor Inicial Obrigatório:** Diferente de fluxos temporários, um estado nunca pode ser indefinido. Todo StateFlow requer a passagem de um valor inicial obrigatório.
- **Retenção do Último Estado:** Ele armazena persistentemente em memória o último valor emitido. Se um observador (uma tela) for destruído e recriado após alguns minutos, assim que ele invocar a função `collect`, ele receberá de imediato o valor mais recente consolidado na memória.
- **Aplicação:** É a ferramenta definitiva e recomendada oficialmente pelo Google para o gerenciamento de estado dentro de ViewModels.

![](../../../attachments/Pasted%20image%2020260530143921.png)

