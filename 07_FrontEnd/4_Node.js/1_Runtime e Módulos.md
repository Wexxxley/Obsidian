
#Concluded 

---
## **1. Runtime Environment**

O **Node.js é um ambiente de execução (runtime) JavaScript** construído sobre a **engine V8** do Google Chrome. Ele permite a execução de código JavaScript fora do navegador. Ao contrário de plataformas baseadas em threads concorrentes (como servidores Java tradicionais), o Node.js opera sob um modelo de **I/O não bloqueante e orientado a eventos**.

**Libuv**: Biblioteca C que fornece suporte a operações de I/O assíncronas baseadas em eventos. Embora o JavaScript seja single-threaded, a Libuv mantém um pool de threads para executar operações pesadas de sistema operacional.

É crucial entender que o Node.js é **Single-Threaded** no que tange a execução do código JavaScript do usuário e o Event Loop. No entanto, o Node.js é **concorrente** através do Event Loop.

---
## **2. Sistema de Módulos**

No Node.js, cada arquivo é tratado como um **módulo independente**. Uma variável declarada em um arquivo não polui o escopo global, a menos que explicitamente exportada.

O Node suporta dois sistemas de módulos: **CommonJS (CJS)** e **ECMAScript Modules (ESM)**. 

### **2.1 CommonJS (CJS)**

Este é o sistema de módulos padrão do Node.js.

- **Carregamento Síncrono:** O carregamento de módulos via **require()** é síncrono. O script para a execução na linha do require, carrega o arquivo, executa seu conteúdo e retorna o objeto exportado. Isso é aceitável em server-side, mas inviável em browsers.
    
- **Dinâmico:** O caminho do módulo em um `require(path)` pode ser construído dinamicamente em tempo de execução (ex: `require('./controllers/' + nomeDoController)`).

Cada arquivo Node.js começa com um objeto vazio pré-definido: `module.exports = {}`. Você tem duas abordagens principais para povoar esse objeto:

#### **A. Exportando Vários Itens**

Você anexa propriedades a esse objeto. É útil quando o módulo é uma biblioteca de utilitários.
```js
// utils.js

// Função privada
const _validar = (n) => typeof n === 'number';

// Funções públicas
const somar = (a, b) => _validar(a) ? a + b : 0;
const subtrair = (a, b) => a - b;

// Opção 1: Atribuindo ao objeto existente
module.exports.somar = somar;
module.exports.subtrair = subtrair;

// Opção 2: Sobrescrevendo com um novo objeto
module.exports = {
    somar,
    subtrair
};
```

```js
const utils = require('./utils');
utils.somar(2, 2); // Funciona
utils._validar(2); // Erro: undefined
```

#### **B. Exportando a Entidade Inteira**

Isso é muito comum quando o arquivo representa uma única **Classe** ou uma única **Função**. Ao fazer isso, você descarta o objeto {} inicial e define module.exports diretamente para a sua entidade.

```js
// UserService.js
class UserService {
    constructor(db) {
        this.db = db;
    }
    create(user) {
        return this.db.insert(user);
    }
}

// A exportação É a própria classe, não um objeto contendo a classe
module.exports = UserService;
```

```js
const UserService = require('./UserService');
const service = new UserService(database);
```

---
### **2.1 Padrão Singleton no Cache de Módulos**

Independente do sistema (CJS ou ESM), os módulos são **cacheados** após a primeira carga.

- Se você fizer `require('./utils')` em dois arquivos diferentes, o código de `./utils` será executado apenas uma vez.
- As chamadas subsequentes retornam o mesmo objeto exportado. Isso torna os módulos "Singletons" por natureza dentro do escopo daquele processo Node.js.
