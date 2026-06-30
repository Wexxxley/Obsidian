

---
### 1. Formas de armazenamento usadas

1. **Banco de Dados Relacional (Room)**: O Room é uma camada de abstração (Object-Relational Mapping) sobre o SQLite. Mapeia objetos Kotlin para tabelas do banco.
	- Responsável por armazenar todos os dados estruturados do negócio.
	- O projeto utiliza DAOs (Data Access Objects) para operações de leitura, escrita...
2. **Preferências do Usuário (Jetpack DataStore)**: Chave valor, assíncrono.
	- UserPreferences Data class que modela os dados salvos.
	- UserPreferencesRepository Centraliza a lógica de leitura e escrita.
		![](../../attachments/Pasted%20image%2020260624134019.png)
  3. **Sistema de Arquivos Interno**: Usado para armazenar arquivos binários. Como imagens de perfil, produtos e serviços. O banco de dados armazena apenas o caminho do arquivo.
	- API de armazenamento interno: filesDir.
	- Centralizado no objeto ImageUtils.kt. ImageUtils gerencia a compressão, salvamento, criação de nomes únicos e deleção de arquivos.

**AppDatabase**
![400](../../attachments/Pasted%20image%2020260624131936.png)
**from**: Recebem o Enum, extrai a string.
**to:** Recupera o texto armazenado. Utiliza a valueOf para instanciar o enum na memória.

![400](../../attachments/Pasted%20image%2020260624133059.png)
- **companion object** implementa o padrão **Singleton**. Garante que apenas uma única instância do banco de dados (AppDatabase) seja criada e mantida na memória durante todo o ciclo de vida do aplicativo.
- O bloco **synchronized(this)** atua como um mecanismo de bloqueio para garantir segurança em operações simultâneas. 

AnotaSmartApplication
![500](../../attachments/Pasted%20image%2020260625131541.png)
Classe que herda da classe base Application. É o primeiro componente a ser instanciado quando o aplicativo é aberto e o último a ser destruído. Atua como o contêiner da conexão do banco de dados Room. O uso `by lazy` garante que a pesada operação de leitura e construção do `AppDatabase` ocorra apenas uma única vez em todo o ciclo de vida do aplicativo.
- **By lazy:** O bloco de código {...} só é acionado na primeira vez que o sistema tentar ler o valor dessa variável. Após a primeira execução, o resultado gerado pelo bloco é salvo internamente. Em todas as leituras subsequentes, o bloco de código é ignorado. O Kotlin apenas devolve imediatamente o valor que já estava salvo no cache.

---
### 2. Navegação

Usei o **Jetpack Compose Navigation**.

As telas do aplicativo são mapeadas classe selada Screen. 
![](../../attachments/Pasted%20image%2020260625132621.png)

A navegação em sí ocorre em MainActivity.kt e ScreenStructure:
   * **NavController**: O objeto central que rastreia qual tela está ativa, gerencia o histórico de telas visitadas (Back Stack) e executa as transições.
   * **NavHost:** Funciona como o catálogo de rotas. Ele escuta o NavController e carrega o Composable (a tela em si) correspondente à rota ativa.
   * **Scaffold**: Componente que organiza o espaço do app e decide de forma quando exibir ou ocultar elementos como a barra inferior e a barra superior com base na tela ativa.
[1_JetpackNavigationCompose](2_Jetpack%20Compose/2_Navegação%20e%20Grids/1_JetpackNavigationCompose.md)
  
Por que usar surface se mais internamente tem o Scaffold?
![](../../attachments/Pasted%20image%2020260625134632.png)
A Surface na raiz ocupa a tela inteira e aplica a cor do tema atual. Sem ele ao alternar entre tema claro e escuro, ou durante transições de tela, poderiam ocorrer piscadas  mostrando a cor antiga da janela do sistema.

O Scaffold não é a Raiz Real, pois o Scaffold está envelopado por outro componente gigante: o ModalNavigationDrawer.
   * O menu lateral precisa deslizar por cima do conteúdo e escurecer o fundo.
   * Se o Scaffold fosse a raiz, o menu lateral estaria "fora" dele. A Surface
     na raiz garante que tanto o Menu Lateral (Drawer) quanto o Scaffold e as
     telas internas herdem o mesmo comportamento de tema.


---
### 3. Tela de venda

**ViewModel**: A viewmodel armazena todos os estados que a tela precisa exibir, procesa eventos, gerenciar tarefas assíncronas e etc. Por exemplo:
   * O VendaViewModel armazena a lista de produtos, a busca ativa e a categoria selecionada.
   * searchQuery é um estado que  viewModel gerencia
![](../../attachments/Pasted%20image%2020260625150117.png)
- A variável com _ é declarada como private. O modificador `Mutable` indica que esta estrutura possui métodos de escrita embutidos.
- A variável sem o _ é pública. A função `asStateFlow()` converte a referência da variável mutável original em uma versão restrita. A interface `StateFlow` não possui métodos de escrita .
- A adoção deste padrão implementa a arquitetura de Fluxo Unidirecional de Dados. Dividindo o estado em duas variáveis, a interface visual é forçada a acionar um método do _ViewModel_ informando que o usuário digitou uma letra. O _ViewModel_ processa essa intenção internamente e atualiza a variável privada `_searchQuery`. Automaticamente, a variável pública `searchQuery` reflete essa mudança.

Em vez de um componente criar e controlar seu próprio estado, ele o "eleva" para um nível superior (para quem o chamou).

Veja a BarraBusca:
![](../../attachments/Pasted%20image%2020260625145720.png)
A BarraBusca não sabe o que é uma "Venda" ou um "ViewModel". Ela é um componente burro e reutilizável. 
