


---
O Node.js é frequentemente escolhido para aplicações de I/O intensivo. A eficiência nessas operações depende diretamente de como os dados são manipulados na memória e transferidos. 

### **1. Buffers**

JavaScript, historicamente, foi projetado para manipulação de strings e documentos DOM, lidando mal com dados binários brutos. O **Buffer** é a solução do Node para lidar com  dados binários.

Um Buffer é um espaço de memória de tamanho fixo alocado mas referenciado por um objeto JavaScript. Ele armazena uma sequência de inteiros (bytes), onde cada entrada representa um byte (0 a 255).
    
- **Alocação:**
    
    - `Buffer.alloc(size)`: Aloca memória e a preenche com zeros. É seguro, mas ligeiramente mais lento.
        
    - `Buffer.allocUnsafe(size)`: Aloca memória rapidamente, mas **não limpa** o conteúdo anterior.
        
        > **Risco de Segurança:** Se você usar `allocUnsafe` e expor o buffer sem sobrescrevê-lo totalmente, pode vazar dados sensíveis que estavam na memória RAM anteriormente.
        

**Exemplo de manipulação:**

JavaScript

```
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

Streams são, fundamentalmente, coleções de dados que podem não estar totalmente disponíveis de uma só vez e não precisam caber inteiramente na memória. Eles são instâncias da classe `EventEmitter`.

A vantagem técnica dos Streams em relação à leitura tradicional de dados é a **eficiência espacial (RAM)** e **temporal (Latência)**.

- **Sem Streams:** Ler um arquivo de 4GB carrega 4GB na RAM antes de processá-lo.
    
- **Com Streams:** O arquivo é lido em pequenos pedaços (_chunks_), processado e liberado da memória sequencialmente.
    

#### **Tipos de Streams**

1. **Readable:** Fonte de dados (leitura). Ex: `fs.createReadStream`, `req` (em HTTP).
    
2. **Writable:** Destino de dados (escrita). Ex: `fs.createWriteStream`, `res` (em HTTP).
    
3. **Duplex:** Pode ler e escrever (canais independentes). Ex: Sockets TCP (`net.Socket`).
    
4. **Transform:** Duplex onde a saída é uma transformação da entrada. Ex: `zlib.createGzip` (compressão), `crypto.createCipher` (criptografia).
    

#### **Pipe e Backpressure**

O método `.pipe()` é o mecanismo para conectar uma `Readable Stream` a uma `Writable Stream`.

JavaScript

```
sourceStream.pipe(destinationStream);
```

Backpressure (Contrapressão):

É um problema de engenharia de fluxo onde a fonte de dados (Readable) envia dados mais rápido do que o destino (Writable) consegue processar.

- Se não tratado, a memória interna do buffer do Node.js encheria até estourar a RAM.
    
- O mecanismo interno do `.pipe()` gerencia isso automaticamente: se o buffer de escrita (highWaterMark) enche, ele sinaliza para a stream de leitura pausar (`pause()`) até que o buffer seja drenado (`drain` event), retomando (`resume()`) em seguida.
    

---

### **3. File System (`fs`)**

O módulo `fs` fornece a API para interagir com o sistema de arquivos. Ele oferece três formas de interação para a maioria das operações:

1. **Síncrona (`readFileSync`)**: Bloqueia o Event Loop e a Thread Principal até o disco responder.
    
    - _Uso:_ Apenas na inicialização da aplicação (ex: ler config). **Nunca** em handlers de requisição (HTTP).
        
2. **Callback (`readFile`)**: Assíncrono, usa o padrão _Error-First Callback_. Legado, propenso a "Callback Hell".
    
3. **Promises (`fs/promises`)**: A forma moderna e recomendada para fluxos assíncronos, compatível com `async/await`.
    

**Exemplo Prático: Servindo um arquivo grande com Streams**

Abaixo, a diferença crítica de performance entre carregar na memória vs usar streams em um servidor HTTP.

**Método Ineficiente (Alto uso de RAM):**

JavaScript

```
import { readFile } from 'node:fs/promises';

// O servidor carrega o arquivo inteiro na RAM antes de enviar
server.on('request', async (req, res) => {
    const data = await readFile('./big-file.mp4');
    res.end(data);
});
```

**Método Eficiente (Stream - Baixo uso de RAM):**

JavaScript

```
import { createReadStream } from 'node:fs';

// O servidor envia chunk por chunk assim que lê do disco
server.on('request', (req, res) => {
    const src = createReadStream('./big-file.mp4');
    src.pipe(res); // 'res' é uma Writable Stream
});
```

No segundo exemplo, mesmo que o arquivo tenha 10GB, o processo Node.js usará apenas alguns Megabytes de RAM (definido pelo tamanho do buffer do stream, padrão 64kb).

---

**Fim do Módulo 4.**

O próximo passo é entender como o Node.js lida com redes e a criação de servidores web, que é a aplicação mais comum da tecnologia.

Digite **next** para prosseguirmos para **Networking: Módulos HTTP, Net e Criação de Servidores**.