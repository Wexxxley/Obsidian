


---

O Node Package Manager (NPM) é o gerenciador de pacotes padrão para o ambiente Node. Ele é instalado juntamente com o Node.js por padrão. O Vue e outros frameworks de _frontend_ são exemplos de pacotes Node muito úteis.


De forma semelhante à verificação de versão do próprio Node, é possível realizar uma verificação da versão do NPM através do comando `npm -v`.

  

### Atualização e Escopo de Instalação do NPM

Para atualizar a versão do seu NPM, utiliza-se o seguinte comando:

`npm install npm@latest -g`.

  

Ao utilizar o parâmetro `@latest` (que significa "mais recente"), a ferramenta NPM atualiza automaticamente a própria versão para a mais atual disponível. Pode-se executar `npm -v` novamente para garantir que a atualização ocorreu corretamente. Também é possível substituir a palavra `latest` para direcionar a instalação a uma versão específica do NPM, utilizando o formato `xx.x.x`.

  

Adicionalmente, é necessário indicar a instalação em escopo global (ou seja, no sistema operacional como um todo, e não apenas na pasta atual) com a _flag_ (sinalizador de comando) `-g` para que o comando `npm` esteja disponível em qualquer diretório da sua máquina local. Por exemplo, ao executar o comando `npm install npm@6.13.4 -g`, a ferramenta buscará especificamente a versão 6.13.4 do pacote NPM para instalação e atualização.

  

O autor recomenda a instalação da versão 7.x do NPM para garantir a capacidade de acompanhar todos os exemplos de código NPM apresentados no livro.

  

### Gerenciamento de Dependências com NPM

Um projeto Node depende de uma coleção de pacotes Node (conhecidos como dependências) para estar operante. No arquivo `package.json`, localizado dentro do diretório do projeto, é possível encontrar esses pacotes instalados. Este arquivo também descreve o projeto, incluindo informações como o nome, os autores e outros comandos de _script_ aplicados exclusivamente àquele projeto.

  

Quando executa-se o comando `npm install` (ou a sua forma abreviada `npm i`) dentro da pasta do projeto, o NPM faz referência a este arquivo e instala todos os pacotes listados em uma nova pasta chamada `node_modules`, deixando-os prontos para o uso no projeto. Além disso, o processo adicionará um arquivo `package-lock.json` com a função de manter o registro exato da versão instalada de cada pacote e garantir a compatibilidade entre dependências comuns.

  

Para iniciar um projeto totalmente do zero com dependências, utiliza-se o comando `npm init` dentro do diretório do projeto. Este comando guiará o desenvolvedor através de uma série de perguntas relacionadas ao projeto e inicializará um projeto vazio, gerando um arquivo `package.json` que contém as respostas fornecidas. É possível pesquisar por quaisquer pacotes públicos de código aberto no site oficial do NPM.

  

### Introdução ao Yarn

Se o NPM é a ferramenta de gerenciamento de pacotes padrão, o Yarn é um gerenciador alternativo e popular desenvolvido pelo Facebook. O Yarn destaca-se por ser mais rápido, mais seguro e mais confiável, características que se devem ao seu mecanismo de _download_ em paralelo e ao seu sistema de armazenamento em _cache_ (uma área de memória rápida). Ele é totalmente compatível com todos os pacotes do NPM; portanto, pode ser utilizado como um substituto direto para o NPM.

  

### Instalação e Comandos Essenciais do Yarn

Pode-se instalar a versão mais recente do Yarn baseada no seu sistema operacional visitando o site oficial do Yarn. Caso o desenvolvedor esteja trabalhando em um computador macOS e possua o gerenciador de pacotes Homebrew instalado, é possível instalar o Yarn diretamente com o comando `brew install yarn`. Este comando instala o Yarn e o Node.js (caso este último não esteja disponível) de forma global.

  

Também é possível instalar o Yarn globalmente utilizando a própria ferramenta NPM com o comando `npm i -g yarn`. Após isso, você deve ter o Yarn instalado na sua máquina e pronto para uso.

  

Para verificar se o Yarn está instalado e confirmar sua versão em uso, utilize o comando `yarn -v`.

Para adicionar um novo pacote ao projeto, use o comando `yarn add <nome do pacote node>`.

  

Para instalar todas as dependências de um projeto, em vez de utilizar o `npm install`, você só precisa executar o comando `yarn` isoladamente dentro do diretório do projeto. Assim que esse processo terminar, de forma semelhante ao funcionamento do NPM, o Yarn também adicionará um arquivo de controle chamado `yarn.lock` no diretório do seu projeto.

  

### Conclusão e Próximos Passos

O material instrui que o Yarn será utilizado como a ferramenta de gerenciamento de pacotes para o código apresentado no livro.

  

Neste ponto, o ambiente essencial de codificação para o desenvolvimento com o _framework_ Vue está configurado. Na próxima seção, o texto abordará as Ferramentas de Desenvolvedor do Vue (_Vue Developer Tools_) e detalhará o que elas oferecem para o trabalho com o Vue.