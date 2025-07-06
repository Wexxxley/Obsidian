#Concluded

___
### **1. Async a await**

`.then()` e `.catch()` não são a primeira escolha hoje ao lidar com promessas, porque a sintaxe **`async/await` é simplesmente superior** na maioria dos casos. Um dos motivos é que o código com `async/await` é linear e parece síncrono, o que é muito mais fácil para o cérebro humano entender do que os blocos aninhados ou encadeados do `.then()`.

![600](../../attachments/Pasted%20image%2020250609152634.png)

---
### **2. Fetch**
**Fetch** é a maneira de fazer requisições de rede.  **Fetch** é **baseada em Promises**.

Ela recebe a **URL** do recurso que você quer acessar.

1. A chamada `fetch(url)` retorna uma **Promise**.
2. Essa Promise **não se resolve com os dados** diretamente. Ela se resolve com um objeto chamado **`Response`**.
3. `Response` é uma representação da resposta HTTP, incluindo o status, cabeçalhos e o corpo.

Para extrair os dados do corpo, você precisa usar um método específico:

- `response.json()`: para transformar o corpo da resposta em um objeto JSON.
- `response.text()`: para obter o corpo como texto puro.
- `response.blob()`: para dados binários (como imagens).

Esses métodos também **retornam uma Promise**, o que significa que temos um processo de duas etapas assíncronas.

#### **2.1 Recenbendo dados com fetch**

![550](../../attachments/Pasted%20image%2020250705144143.png)

#### **2.1 Enviando dados com fetch**

Para enviar dados, você passa um segundo argumento para a `fetch`,um objeto de configuração.

![](../../attachments/Pasted%20image%2020250705145309.png)