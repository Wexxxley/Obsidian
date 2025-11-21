


---
O Node.js é frequentemente escolhido para aplicações de I/O intensivo. A eficiência nessas operações depende diretamente de como os dados são manipulados na memória e transferidos. 

### **1. Buffers**

JavaScript, historicamente, foi projetado para manipulação de strings e documentos DOM, lidando mal com dados binários brutos. O **Buffer** é a solução do Node para lidar com  dados binários.

Um Buffer é um espaço de memória de tamanho fixo alocado, mas referenciado por um objeto JavaScript. Ele armazena uma sequência de bytes.


```js
// Cria um buffer de 10 bytes
const buf = Buffer.alloc(10);

// Escreve string (convertida para binário UTF-8 padrão)
buf.write('Hello');

// Leitura
console.log(buf.toString()); // "Hello"
console.log(buf.toJSON());   // Representação em array de inteiros
```

---

### **2. Streams**

Streams são, fundamentalmente, coleções de dados que podem não estar totalmente disponíveis de uma só vez e não precisam caber inteiramente na memória. 

A vantagem técnica dos Streams em relação à leitura tradicional de dados é a eficiência espacial (RAM) e temporal (Latência).

- **Sem Streams:** Ler um arquivo de 4GB carrega 4GB na RAM antes de processá-lo.
    
- **Com Streams:** O arquivo é lido em pequenos pedaços (chunks), processado e liberado da memória sequencialmente.

