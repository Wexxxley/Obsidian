

---
### 1. O que é Git?

Git é o sistema de controle de versão (VCS) de código aberto mais popular que existe. Ele foi criado por **Linus Torvalds**, a mesma pessoa que criou o Linux2.
    
- Seu objetivo principal é **rastrear mudanças no código-fonte** 3333e ajudar os programadores a coordenar o trabalho4.
    
- Para um programador, saber usar Git é essencial5555.
    
- O livro em si é um guia de código aberto, distribuído sob a **Licença MIT** 6, o que significa que pode ser usado e modificado livremente7.
    

#### Controle de Versão (VCS)

- Controle de Versão (também chamado de _Source Control_) é o que permite rastrear e gerenciar todas as mudanças feitas no seu código ao longo do tempo8.
    
- **Por que usá-lo?**
    
    - Permite que **várias pessoas trabalhem no mesmo projeto** simultaneamente9.
        
    - Mantém um **histórico de todas as alterações**101010.
        
    - Permite que a equipe trabalhe ao mesmo tempo e depois **junte (faça o "merge")** esse trabalho11.
        
    - Se algo der errado, ele permite que você **reverta facilmente para um estado anterior** que estava funcionando12.
        

#### Git é Distribuído

- Git é um VCS **Distribuído**1313. Isso é um conceito-chave!
    
- Significa que você não tem apenas uma cópia do código. Você tem:
    
    1. Um **repositório local** (no seu computador)1414.
        
    2. Um **repositório remoto** (em um servidor, como o GitHub)151515.
        
- A grande vantagem é a segurança: se algo acontecer com seu notebook (por exemplo, quebrar), seu código ainda estará salvo e seguro no repositório remoto16.
    

#### Instalando o Git

- Para usar o Git, você precisa primeiro instalá-lo na sua máquina17.
    
- Linux (Debian/Ubuntu):
    
    `sudo apt install git-all` 18
    
- Linux (RHEL):
    
    `sudo dnf install git-all` 19
    
- Mac:
    
    Recomenda-se usar o Homebrew: brew install git20.
    
- Windows:
    
    Você deve baixar o instalador21. Durante a instalação, é importante selecionar a opção Git Bash, que fornecerá um terminal para usar os comandos22.
    
- Para verificar a versão
    
    Depois de instalado, você pode usar o comando git-version para ver qual versão está rodando23. (O livro mostra um exemplo de saída: git version 2.25.1 24).
    

#### Comandos Básicos do Shell (Terminal)

- Como o Git é usado principalmente pela linha de comando, o livro revisa alguns comandos básicos do terminal25.
    
- `ls`: (List) **Lista** os arquivos e pastas no seu diretório atual26. (No CMD do Windows, o comando equivalente é `dir` 27).
    
- `pwd`: (Print Working Directory) **Mostra** o caminho completo da pasta onde você está agora28.
    
- `cd`: (Change Directory) **Navega** entre as pastas29.
    
    - `cd nome-da-pasta` (para entrar em uma pasta)30.
        
    - `cd ..` (para voltar um nível)31.
        
- `rm`: (Remove) **Deleta** arquivos32.
    
    - Para deletar um diretório (pasta), você precisa usar a flag `-r` (ex: `rm -r nome-da-pasta`)33.
        

---

Esta foi a nossa introdução aos conceitos básicos de Git, controle de versão e os comandos de terminal necessários.

Quando estiver pronto para avançar para as **páginas 21-30** (que cobrem a Configuração inicial do Git e a Introdução ao GitHub), basta dizer **next**.