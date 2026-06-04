
#Concluded 

---
### **1. O Contêiner usa o SO do Computador ou da Imagem?**

Ele usa os dois, mas partes diferentes. Para entender, precisamos dividir um Sistema Operacional (como o Linux) em duas camadas principais:

1. **O Kernel:** É a parte que fala com o hardware (processador, memória, rede, disco).
    
2. **O Userland (O Espaço do Usuário):** São os arquivos, bibliotecas, utilitários e o visual. 

- O contêiner usa o **Kernel do seu computador**. Se você está no Linux Mint, todos os contêineres estão usando o coração do seu Linux Mint para processar dados. 
    
- O contêiner usa o sistema de arquivos da Imagem Base.

---
### **2. Qual a diferença direta entre Imagem e Contêiner?**

A imagem é como se fosse a classe e o container uma instancia de um objeto
#### **2.1 A Imagem**
- Ela contém o código, as bibliotecas, as configurações e o sistema de arquivos base.
- **É estática:** É apenas um arquivo no disco (uma coleção de camadas).
- **Read-Only:** Você não muda uma imagem depois de criada. 
#### **2.2 O Contêiner**
- É um processo rodando na CPU.
- **É leitura e escrita:** Quando o contêiner inicia, o Docker pega a imagem (que é fixa) e coloca uma camada de escrita. Qualquer arquivo que você cria ou modifica dentro do contêiner fica nessa camada temporária.
- Se você apagar o contêiner, aquela camada de escrita some. A imagem original permanece intacta.

---
### **3. Quais os estados de um container?**

Contêineres têm estados muito bem definidos. Como um contêiner é basicamente um **processo** rodando no seu computador, ele segue um ciclo de vida parecido com programas comuns.

1. **Created:**
    - O contêiner foi criado, mas ainda não começou a rodar o processo.
    - `docker create`: raramente usado, geralmente usamos o `run` que cria e inicia.
        
2. **Running:**
    - O processo principal está usando CPU e Memória RAM.
    - `docker start` ou `docker run`.
        
3. **Paused:**
    - O contêiner ainda está na memória RAM, mas o Docker "congelou" o processo.
    - `docker pause`.
        
4. **Exited:**
    - O processo principal terminou ou você mandou parar (`docker stop`).
    - O contêiner **NÃO** sumiu. O sistema de arquivos (aquela camada de escrita) ainda está lá, intacto, ocupando espaço no disco. Você pode iniciá-lo de novo e continuar de onde parou.
        
5. **Dead:**
    - Quando você roda o `docker rm`, o contêiner sai do estado _Exited_ e é apagado do disco. Aqui a camada de escrita é destruída.        
