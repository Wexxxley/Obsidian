
#Concluded 

---
O pacote dotenv serve para implementar o princípio de **Separação de Configuração e Código**. Tecnicamente, ele é um módulo que carrega variáveis de ambiente definidas em um arquivo local para dentro do objeto global `process.env` do Node.js em tempo de execução.

### **1. O Problema**

Sem variáveis de ambiente, você acabaria escrevendo credenciais diretamente no código-fonte:

```js
// PERIGO: Credencial exposta no código (Hardcoded)
const dbPassword = "minha_senha_super_secreta";
const apiKey = "sk-1234567890";
```

1. **Segurança:** Se você enviar esse código para o GitHub/GitLab, suas senhas ficam públicas no histórico de versões.
2. **Flexibilidade:** Para mudar o banco de dados de "Desenvolvimento" para "Produção", você teria que editar o código-fonte, o que viola a integridade do build.

---
### **2. A Solução: Environment Variables**

O Node.js possui um objeto global chamado `process.env`, que expõe as variáveis do sistema operacional onde o processo está rodando. O dotenv  lê um arquivo de texto, faz o _parsing_ das chaves e valores, e injeta essas propriedades no `process.env`.

---
### **3. Implementação Técnica**

.env
```js
PORT=3000
DATABASE_URL=./backend/database/amethyst.sqlite
LLM_API_KEY=sk-abcdef123456
NODE_ENV=development
```

Você deve carregar o dotenv o mais cedo possível na sua aplicação.
```js
// server.js
const dotenv = require('dotenv');
dotenv.config({ path: './.env.' });

const dbPath = process.env.DATABASE_URL 
```

---
### **4. gitignore**

O arquivo `.env` contém segredos. Ele jamais deve ser commitado no repositório Git. Para que outros desenvolvedores saibam quais variáveis são necessárias, cria-se um arquivo de exemplo chamado .env.example  contendo apenas as chaves, sem os valores reais:

```js
PORT=3000
DATABASE_URL=
LLM_API_KEY=
```
