
#Concluded 

---

Ambos **Stack** (pilha ) e **Heap** (pilha de alocação) são apenas **regiões da memória RAM** que o seu processo usa. Mas a forma como eles são usados e gerenciados é completamente diferente.

### **1. Stack (Pilha)**

A Stack é uma região de memória usada para armazenar dados de escopo local. Ela funciona como uma pilha de pratos.
- **Como funciona:** Quando você chama uma função (ex: calcularMedia(a, b)), o programa "empilha" um Stack Frame nessa pilha.
    
- **O Stack Frame possui:**
    - Os argumentos da função.
    - As variáveis locais declaradas _dentro_ da função.
    - Para onde a CPU deve pular de volta quando a função terminar.
        
- **Termino:** Quando a função termina, seu o Stack Frame é "desempilhado"  e todo o seu conteúdo é destruído.
    
- **Velocidade:** Isso é extremamente rápido.
    
- **Tamanho Fixo:** A Stack tem um tamanho fixo (definido quando o processo/thread é criado, geralmente 1MB a 8MB).
    
- **Stack Overflow**: Acontece quando você tenta "empilhar" mais coisas do que cabem na Stack. Por exemplo quand você usar Recursão infinita. 

---
### **2. Heap**

É um grande "depósito" desorganizado, usado para alocar dados de forma dinâmica, ou seja, dados que você não sabe o tamanho ou o tempo de vida quando está escrevendo o código.

- **Como funciona:**    
    1. Você pede ao SO: "Ei, preciso de 500 bytes de memória no Heap para guardar um objeto". (Ex: new no Java/C#)
    2. O SO procura um bloco de memória livre desse tamanho.
    3. Ele "aluga" esse bloco para você e te devolve um ponteiro.
    4. Esse ponteiro é armazenado em uma variável na sua **Stack**.
    
- **Velocidade:** A alocação no Heap é _muito mais lenta_ que na Stack.
    
- **O que vai para o Heap?**
	- **Objetos:** Em linguagens como Java e C#, _todos_ os objetos vão para o Heap.
	- **Dados de "Tempo de Vida Longo":** Qualquer dado que precise sobreviver _depois_ que a função que o criou terminar. Se estivesse na Stack, ele morreria. No Heap, ele vive até ser explicitamente destruído.
    
#### **1.1 Limitações e Problemas**

- **Gerenciamento Manual:** Você é responsável por "devolver" a memória quando não precisar mais (Ex: `delete` no C++)
    
- **Memory Leak**: Ocorre quando você aloca memória no Heap, e perde o ponteiro antes de devolver o espaço. O espaço fica "alugado" para sempre, inacessível. 
        
- **Garbage Collector (Java, C#, Python):** Linguagens como java, c# e python possuem  um Garbage Collector, um processo de fundo que automaticamente encontra e libera memória do Heap que não está mais sendo usada, prevenindo a maioria dos vazamentos.
    
- **Fragmentação:** Com o tempo, o Heap fica cheia de pequenos blocos alugados e liberados. Pode ser difícil encontrar um bloco _contínuo_ grande o suficiente, mesmo que o total de memória livre seja alto.

