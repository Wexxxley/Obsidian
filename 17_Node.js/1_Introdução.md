

---
## **1. Runtime Environment**

O **Node.js é um ambiente de execução (runtime) JavaScript** construído sobre a **engine V8** do Google Chrome. Ele permite a execução de código JavaScript fora do navegador. Ao contrário de plataformas baseadas em threads concorrentes (como servidores Java tradicionais), o Node.js opera sob um modelo de **I/O não bloqueante e orientado a eventos**.

**Libuv**: Biblioteca C que fornece suporte a operações de I/O assíncronas baseadas em eventos. Embora o JavaScript seja single-threaded, a Libuv mantém um pool de threads para executar operações pesadas de sistema operacional.

É crucial entender que o Node.js é **Single-Threaded** no que tange a execução do código JavaScript do usuário e o Event Loop. No entanto, o Node.js é **concorrente** através do Event Loop.

---
## **1. Sistema de Módulos**

No Node.js, cada arquivo é tratado como um **módulo independente**. Uma variável declarada em um arquivo não polui o escopo global, a menos que explicitamente exportada.

O Node suporta dois sistemas de módulos: **CommonJS (CJS)** e **ECMAScript Modules (ESM)**. 

### **1.1 CommonJS (CJS)**

Este é o sistema de módulos padrão do Node.js.

- **Carregamento Síncrono:** O carregamento de módulos via **require()** é síncrono. O script para a execução na linha do require, carrega o arquivo, executa seu conteúdo e retorna o objeto exportado. Isso é aceitável em server-side, mas inviável em browsers.
    
- **Dinâmico:** O caminho do módulo em um `require(path)` pode ser construído dinamicamente em tempo de execução (ex: `require('./controllers/' + nomeDoController)`).

**Exportação e Importação**

```js
// math.js
const add = (a, b) => a + b;
module.exports = { add }; // Objeto exportado
```

```js
// app.js
const math = require('./math');
// ou destructuring
const { add } = require('./math');
```


---

### **2. ECMAScript Modules (ESM)**

Este é o padrão oficial da especificação JavaScript (ES6+), suportado nativamente pelo Node.js (versões recentes) e navegadores.

- **Carregamento Assíncrono e Análise Estática:** O ESM permite que o interpretador analise as dependências (`import`) antes de executar o código. Isso constrói uma árvore de dependências estática.
    
- **Strict Mode:** Módulos ESM rodam sempre em `'use strict'` automaticamente.
    
- **Falta de Globais CJS:** Em ESM, `__dirname`, `__filename` e `require` **não existem**. Para obter o caminho do arquivo, utiliza-se `import.meta.url`.
    

Para ativar o ESM no Node.js, você deve usar a extensão `.mjs` no arquivo ou definir `"type": "module"` no seu `package.json`.

#### **Live Bindings (Diferença Técnica Crítica)**

Diferente do CJS, que exporta uma _cópia_ dos valores (no momento da exportação), o ESM exporta **Live Bindings** (referências vivas). Se o módulo exportador mudar o valor de uma variável exportada, o módulo importador verá a mudança.

#### **Exportação e Importação (Sintaxe ESM)**

JavaScript

```
// math.mjs
export const add = (a, b) => a + b;
export default function log() { console.log('default'); }

// app.mjs
import log, { add } from './math.mjs';
```

---

### **Comparativo Técnico: Interoperabilidade**

1. **CJS no ESM:** Você pode importar CJS dentro de ESM usando `import`, mas apenas a exportação `default` (que será o `module.exports` inteiro) costuma funcionar previsivelmente. Named imports de CJS podem falhar dependendo da análise estática.
    
2. **ESM no CJS:** Você **não pode** usar `require()` para carregar um arquivo ESM, pois `require` é síncrono e ESM é inerentemente assíncrono. A única forma de importar ESM dentro de CJS é usando a função dinâmica `import()` que retorna uma Promise.
    

JavaScript

```
// Arquivo CJS importando ESM
(async () => {
  const module = await import('./meu-modulo.mjs');
})();
```

---

### **Padrão Singleton no Cache de Módulos**

Independente do sistema (CJS ou ESM), os módulos são **cacheados** após a primeira carga.

- Se você fizer `require('./utils')` em dois arquivos diferentes, o código de `./utils` será executado apenas **uma vez**.
    
- As chamadas subsequentes retornam o mesmo objeto exportado (a mesma instância na memória).
    
- Isso torna os módulos "Singletons" por natureza dentro do escopo daquele processo Node.js.
    
