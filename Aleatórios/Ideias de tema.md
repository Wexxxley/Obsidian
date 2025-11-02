

---
### Jogo de Batalha RPG em Turnos

- **Interação com usuário:** Menu de batalha a cada turno: "1. Atacar", "2. Usar Habilidade", "3. Usar Item", "4. Fugir".
    
- **Abstração:** Classes como `Personagem`, `Arma`, `Habilidade`, `Item`.
    
- **Encapsulamento:** A classe `Personagem` teria atributos privados `vida`, `mana`, `forca`, `defesa`. Métodos públicos seriam `receberDano(int dano)`, `atacar(Personagem alvo)`, `usarMagia(Magia magia)`. O método `receberDano` calcularia o dano líquido (dano - defesa).
    
- **Herança:**
    - `Guerreiro` **é um** `Personagem`.
    - `Mago` **é um** `Personagem`.
    - `Arqueiro` **é um** `Personagem`.
        
- **Polimorfismo:**
    - O método `atacar()` seria a chave. O loop principal do jogo chamaria `jogador.atacar(inimigo)`.
        
        - Se `jogador` for `Guerreiro`, o método usaria o atributo `forca`.            
        - Se `jogador` for `Mago`, o método usaria o atributo `inteligencia` e gastaria `mana`.
        - Se `jogador` for `Arqueiro`, o método poderia ter uma chance de `acertoCritico`.
            
    - O método `subirDeNivel()` também poderia ser polimórfico, aumentando atributos diferentes para cada classe.

---
### Simulação de Sistema de Arquivos (Console)

Uma simulação de como um sistema operacional organiza arquivos e pastas.

- **Interação com usuário:** Um "prompt" de console (ex: `C:\>`) onde o usuário digita comandos como `ls` (listar), `mkdir <nome>` (criar diretório), `touch <nome>` (criar arquivo), `cd <nome>` (mudar de diretório), `pwd` (mostrar diretório atual).
    
- **Abstração:** Uma classe abstrata (ou interface) `NoDoSistema` (ou `FileSystemNode`).
    
- **Encapsulamento:** A classe `Diretorio` teria uma lista privada de `NoDoSistema` (seus "filhos"). A classe `Arquivo` teria seu `conteudo` e `tamanho` privados. Métodos públicos como `adicionarFilho` e `removerFilho` controlariam a estrutura.
    
- **Herança:**    
    - `Arquivo` **é um** `NoDoSistema`.
    - `Diretorio` **é um** `NoDoSistema`.
    - (Opcional) `ArquivoTexto` e `ArquivoBinario` podem herdar de `Arquivo`.
        
- **Polimorfismo:**
    - O método `getTamanho()`.
        - Para `Arquivo`, retorna o tamanho do seu conteúdo (ex: 50 bytes).
        - Para `Diretorio`, ele deve iterar por todos os seus filhos, chamar `getTamanho()` em cada um e retornar a soma total (isso é um ótimo exemplo, pois o diretório não sabe/precisa saber se o filho é um arquivo ou outro diretório).
            
    - O método `listar(int nivelDeIndentacao)`.
        - `Arquivo` imprime seu nome com indentação.
        - `Diretorio` imprime seu nome com indentação e, em seguida, chama `listar()` para cada um de seus filhos com `nivelDeIndentacao + 1`.

---
### Player de Mídia Simplificado

Um sistema que gerencia e "toca" diferentes tipos de mídias de áudio.

- **Interação com usuário:** Menu para "1. Listar todas as mídias", "2. Criar Playlist", "3. Adicionar mídia à Playlist", "4. Tocar Mídia", "5. Tocar Playlist".
    
- **Abstração:** Classe abstrata `Midia`.
    
- **Encapsulamento:** A classe `Playlist` teria uma lista privada de `Midia` e um índice `faixaAtual`. Métodos `proximaFaixa()` e `faixaAnterior()` controlariam o índice. A classe `Midia` teria `titulo`, `duracao`, `artista` como privados.
    
- **Herança:**
    - `Musica` **é uma** `Midia`. (Pode ter atributos extras como `album`, `genero`).
    - `Podcast` **é uma** `Midia`. (Pode ter atributos extras como `nomeDoPrograma`, `episodio`)
    - `Audiobook` **é uma** `Midia`. (Pode ter `narrador`, `capitulo`).
        
- **Polimorfismo:**
    - O método `tocar()` (ou `play()`).
        - `Musica` imprimiria: "Tocando música: 'Título da Música' - Artista (Álbum)".
        - `Podcast` imprimiria: "Tocando podcast: 'Nome do Programa', Ep. #X: 'Título do Episódio'".
        - `Audiobook` imprimiria: "Continuando livro: 'Título', Capítulo Y, narrado por Z".
            
    - Quando o usuário "Tocar Playlist", o sistema apenas chamaria `playlist.getFaixaAtual().tocar()`, e a saída correta apareceria na tela.
