

---
### **1. O Contêiner usa o SO do Computador ou da Imagem?**

Ele usa os dois, mas partes diferentes. Para entender, precisamos dividir um Sistema Operacional (como o Linux) em duas camadas principais:

1. **O Kernel:** É a parte que fala com o hardware (processador, memória, rede, disco).
    
2. **O Userland (O Espaço do Usuário):** São os arquivos, bibliotecas, utilitários e o visual. 

- O contêiner usa o **Kernel do seu computador**. Se você está no Linux Mint, todos os contêineres estão usando o coração do seu Linux Mint para processar dados. Por isso contêineres são leves; eles não precisam "bootar" um kernel novo.
    
- O contêiner usa os arquivos da Imagem Base.

---

### **2. Qual a diferença direta entre Imagem e Contêiner?**

A imagme é como se fosse a classe e o container uma instancia de um objeto
#### **A Imagem**
- Ela contém o código, as bibliotecas, as configurações e o sistema de arquivos base.
- **É estática:** É apenas um arquivo no disco (uma coleção de camadas).
- **Read-Only:** Você não muda uma imagem depois de criada. 
#### **O Contêiner**
- É um processo rodando na CPU.
- **É leitura e escrita:** Quando o contêiner inicia, o Docker pega a imagem (que é fixa) e coloca uma **camada fina de escrita** por cima dela. Qualquer arquivo que você cria ou modifica dentro do contêiner fica nessa camada temporária.
- Se você apagar o contêiner, aquela camada de escrita some. A imagem original permanece intacta.
    

