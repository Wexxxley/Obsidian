


---
O Node.js possui um ecossistema de pacotes centralizado através do **NPM (Node Package Manager)**. O NPM não é apenas um repositório, mas uma CLI (Command Line Interface) que gerencia o ciclo de vida das dependências e a execução de scripts do projeto.

![](../attachments/Pasted%20image%2020251121090514.png)

---
### **1. package.json**

O arquivo `package.json` é a raiz do projeto Node.js. Ele define metadados, scripts de automação e listas de dependências.

![](../attachments/Pasted%20image%2020251121090553.png)
#### **Campos Técnicos Relevantes**

- **`main`**: O ponto de entrada da aplicação (ex: `index.js`). Quando alguém instala seu pacote e faz `require('seu-pacote')`, o Node carrega o arquivo definido aqui.
    
- **`scripts`**: Um mapa de comandos.
    
    - _Detalhe Técnico:_ Scripts executados via `npm run <script>` têm o diretório `./node_modules/.bin` adicionado automaticamente ao `PATH` do shell temporário. Isso permite executar binários de dependências (como `jest`, `eslint`, `nodemon`) sem precisar digitar o caminho completo.
        
- **`type`**: Define se o projeto usa CJS (`"commonjs"`, padrão) ou ESM (`"module"`), como visto no Módulo 2.
    

---

### **2. Categorias de Dependências**

O NPM separa as bibliotecas em escopos de uso:

- **`dependencies` (`npm install X`)**: Bibliotecas necessárias em tempo de execução (_runtime_) para a aplicação funcionar em produção (ex: `express`, `axios`, `pg`).
    
- **`devDependencies` (`npm install -D X`)**: Ferramentas necessárias apenas durante o desenvolvimento, testes ou build (ex: `typescript`, `jest`, `webpack`). Elas **não** são instaladas quando se executa `npm install --production` (comum em pipelines de CI/CD).
    
- **`peerDependencies`**: Declara que seu pacote precisa de uma dependência, mas espera que o projeto "hospedeiro" (quem instalou seu pacote) a forneça. É fundamental para arquiteturas de plugins (ex: um plugin do React não deve instalar sua própria cópia do React, mas usar a da aplicação).
    

---

### **3. Versionamento Semântico (SemVer)**

O ecossistema Node depende estritamente do SemVer (`MAJOR.MINOR.PATCH`) para gerenciar atualizações.

- **MAJOR (X.0.0)**: Mudanças incompatíveis de API (Breaking Changes).
    
- **MINOR (0.X.0)**: Novas funcionalidades compatíveis com versões anteriores (Backward Compatible).
    
- **PATCH (0.0.X)**: Correções de bugs compatíveis com versões anteriores.
    

#### **Operadores de Versão no package.json**

O NPM usa prefixos para definir o intervalo de versões aceitáveis ao executar `npm install` ou `npm update`:

- **Caret (`^`)**: Padrão do NPM. Permite atualizações que não alteram o número MAJOR (ex: `^1.2.3` aceita `1.3.0` e `1.9.9`, mas não `2.0.0`).
    
- **Tilde (`~`)**: Mais restrito. Permite apenas atualizações de PATCH (ex: `~1.2.3` aceita `1.2.4`, mas não `1.3.0`).
    
- **Exact (`1.2.3`)**: Instala exatamente essa versão.
    

---

### **4. Determinismo: `package-lock.json`**

Enquanto o `package.json` descreve intervalos de versões aceitáveis, o `package-lock.json` descreve a **árvore exata** instalada atualmente.

- **Função:** Garante que todos os desenvolvedores e o servidor de produção instalem exatamente as mesmas versões de todas as dependências (e subdependências).
    
- **Integridade:** Contém um hash de integridade (geralmente SHA-512) para cada pacote, garantindo que o código baixado não foi alterado em relação ao registro do NPM.
    
- **Regra:** Nunca edite este arquivo manualmente. Ele é gerado automaticamente pelo NPM.
    

---

### **5. Algoritmo de Resolução de Módulos (Module Resolution)**

Quando você executa `require('axios')` ou `import ... from 'axios'`, o Node.js segue um algoritmo estrito para localizar o arquivo:

1. **Core Modules:** Verifica se é um módulo nativo (ex: `fs`, `http`, `path`). Se sim, retorna imediatamente.
    
2. **Caminhos Relativos/Absolutos:** Se começar com `./`, `../` ou `/`, resolve o arquivo no caminho especificado.
    
3. **Node Modules (Resolução Hierárquica):** Se não for um caminho de arquivo:
    
    - O Node procura uma pasta `node_modules` no diretório atual.
        
    - Se não encontrar o pacote lá, ele sobe para o diretório pai (`../node_modules`) e procura novamente.
        
    - Ele repete esse processo recursivamente até atingir a raiz do sistema de arquivos (`/`).
        

Esse comportamento permite que projetos aninhados herdem dependências ou que ferramentas globais funcionem, mas também pode causar conflitos se não compreendido corretamente.

---

**Fim do Módulo 3.**

Agora que entendemos o ambiente e as dependências, devemos entrar no sistema de I/O e manipulação de dados binários, essenciais para performance.

Digite **next** para prosseguirmos para **Buffers, Streams e File System**.