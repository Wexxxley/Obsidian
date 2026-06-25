

---
### 1. Formas de armazenamento usadas

1. **Banco de Dados Relacional (Room)**: O Room é uma camada de abstração (Object-Relational Mapping) sobre o SQLite. Mapeia objetos Kotlin para tabelas do banco.
	- Base do sistema, responsável por armazenar todos os dados estruturados do negócio.
	- O projeto utiliza DAOs (Data Access Objects) para operações de leitura, escrita e exclusão.

2. **Preferências do Usuário (Jetpack DataStore)**: Chave valor, assíncrono.
	- UserPreferences Data class que modela os dados salvos.
	- UserPreferencesRepository Centraliza a lógica de leitura e escrita.
		![](../../attachments/Pasted%20image%2020260624134019.png)

  3. **Sistema de Arquivos Interno**: Usado para armazenar arquivos binários. Como imagens de perfil, produtos e serviços. O banco de dados armazena apenas o caminho do arquivo.
	- API de armazenamento interno do Android (context.filesDir).
	- Centralizado no objeto ImageUtils.kt. ImageUtils gerencia a compressão, salvamento, criação de nomes únicos (UUID) e deleção de arquivos, garantindo que o armazenamento interno seja mantido limpo.

**AppDatabase**
![400](../../attachments/Pasted%20image%2020260624131936.png)
**from**: Recebem o Enum, extrai a string e armazena no db
**to:** Recupera o texto armazenado. Utiliza a valueOf para instanciar o enum na memória.

![400](../../attachments/Pasted%20image%2020260624133059.png)
- **companion object** implementa o padrão **Singleton**. Garante que apenas uma única instância do banco de dados (AppDatabase) seja criada e mantida na memória durante todo o ciclo de vida do aplicativo.
- O bloco **synchronized(this)** atua como um mecanismo de bloqueio para garantir segurança em operações simultâneas. 

AnotaSmartApplication
![500](../../attachments/Pasted%20image%2020260625131541.png)
Classe que herda da classe base Application. É o primeiro componente a ser instanciado quando o aplicativo é aberto e o último a ser destruído. Atua como o contêiner da conexão do banco de dados Room. O uso `by lazy` garante que a pesada operação de leitura e construção do `AppDatabase` ocorra apenas uma única vez em todo o ciclo de vida do aplicativo.
- **By lazy:** O bloco de código {...} só é acionado na primeira vez que o sistema tentar ler o valor dessa variável. Após a primeira execução, o resultado gerado pelo bloco é salvo internamente. Em todas as leituras subsequentes, o bloco de código é ignorado. O Kotlin apenas devolve imediatamente o valor que já estava salvo no cache.

### 2. Navegação

Usei o **Jetpack Compose Navigation**.

As telas do aplicativo são mapeadas classe selada Screen. 
![](../../attachments/Pasted%20image%2020260625132621.png)

A navegação em sí ocorre em MainActivity.kt e ScreenStructure:
   * **NavController**: O objeto central que rastreia qual tela está ativa, gerencia o histórico de telas visitadas (Back Stack) e executa as transições.
   * **NavHost:** Funciona como o catálogo de rotas. Ele escuta o NavController e carrega o Composable (a tela em si) correspondente à rota ativa.
   * **Scaffold**: Componente que organiza o espaço do app e decide de forma quando exibir ou ocultar elementos como a barra inferior e a barra superior com base na tela ativa.

   1. **Setup Interceptor:** Se o usuário abrir o app e ainda não tiver configurado seus dados básicos, o sistema intercepta a navegação e o redireciona automaticamente para a tela de Setup, limpando o histórico para impedir que ele pule essa etapa essencial.
   2. Navegação Dinâmica com Parâmetros: A rota da tela de detalhes de um
      cliente é dinâmica: "cliente_detalhes/{clientId}". O NavHost consegue
      extrair o clientId diretamente da rota para carregar os dados específicos
      daquele cliente no ViewModel correspondente.
   3. Menu Lateral Dinâmico (ModalNavigationDrawer): O usuário pode arrastar o
      dedo a partir do canto da tela ou clicar no ícone de menu superior para
      abrir uma gaveta lateral que dá acesso às opções secundárias.

  ---

  4. Termos Técnicos Mais Importantes (Glossário para a Apresentação)
  Se você citar estes termos em sua apresentação, demonstrará excelente domínio
  técnico do ecossistema Android moderno:

   * NavController / NavHostController: O "piloto" da navegação. Responsável por
     comandar a ida para novas telas (navController.navigate("rota")) ou a volta
     à tela anterior (navController.popBackStack()).
   * NavHost: O "palco" onde as telas são trocadas. É o contêiner reativo que
     renderiza a tela atual associada à rota selecionada.
   * Back Stack (Pilha de Navegação): O histórico de telas visitadas. Quando
     você avança, as telas são "empilhadas". Quando você clica em voltar, a tela
     do topo é removida para revelar a anterior.
   * popUpTo & inclusive: Uma estratégia para limpar a pilha de navegação. 
       * Exemplo: Ao terminar uma venda com sucesso, o app usa
         popUpTo(Screen.Venda.route) { inclusive = false } para esvaziar todas
         as telas intermediárias do carrinho e da finalização. Isso impede que o
         usuário aperte o botão "voltar" do celular e caia de novo na tela de
         pagamento da venda já finalizada.
   
   


  ---

  1. Cor de Fundo Base da Janela (Evita o "Flickering")
  A Surface na raiz ocupa a tela inteira (Modifier.fillMaxSize()) e aplica
  imediatamente a cor do tema atual (MaterialTheme.colorScheme.background). 
   * O problema de tirar a Surface: Se você não colocar a Surface no topo, o
     Android desenhará o plano de fundo padrão da Activity (que geralmente é
     branco ou preto estático do sistema) antes de carregar o Compose. 
   * Ao alternar entre tema claro e escuro, ou durante transições de tela,
     poderiam ocorrer piscadas (flickers) mostrando a cor antiga da janela do
     sistema. A Surface garante que o fundo correto do tema seja pintado
     instantaneamente em toda a tela.

  2. Propagação Automática do Conteúdo (LocalContentColor)
  No Material Design 3, a Surface faz mais do que pintar o fundo. Ela define
  automaticamente a cor do conteúdo padrão (como textos e ícones) que fica por
  cima dela.
   * Se o fundo é escuro, ela ajusta o LocalContentColor para claro.
   * Isso garante que qualquer texto ou componente básico que você use no
     aplicativo herde a cor de contraste correta de forma automática, sem que
     você precise definir manualmente cor por cor.

  3. O Scaffold não é a Raiz Real
  Se você olhar a hierarquia, o Scaffold está envelopado por outro componente
  gigante: o ModalNavigationDrawer (o menu lateral).

   1 Surface {
   2     ModalNavigationDrawer {
   3         Scaffold {
   4             // Telas...
   5         }
   6     }
   7 }
   * O menu lateral precisa deslizar por cima do conteúdo e escurecer o fundo.
   * Se o Scaffold fosse a raiz, o menu lateral estaria "fora" dele. A Surface
     na raiz garante que tanto o Menu Lateral (Drawer) quanto o Scaffold e as
     telas internas herdem o mesmo comportamento de tema, cores de superfície e
     tratamento de toque.

  4. Caixas de Diálogo e Popups (Overlays)
  Muitos componentes como Dialog (caixas de confirmação), DropdownMenu e
  BottomSheets são renderizados em "janelas flutuantes" separadas do fluxo
  normal do Scaffold. 
   * Ter uma Surface englobando todo o tema garante que, mesmo que um Dialog
     seja disparado fora da área do Scaffold, ele ainda respeite as diretrizes
     de cores e contraste do tema configurado.

  ---

  💡 Resumo para a Apresentação:
  > "Usamos a Surface logo abaixo do AppTheme para servir como a 'tela de
  pintura' base do aplicativo. Ela garante que, ao abrirmos o app ou mudarmos o
  tema (claro/escuro), a janela inteira do Android assuma a cor correta
  instantaneamente, evitando oscilações visuais. Já o Scaffold funciona mais
  internamente como um organizador de layout estrutural das telas, cuidando
  especificamente das posições das barras superior, inferior e do conteúdo
  principal."

