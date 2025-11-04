

---

![650](attachments/Pasted%20image%2020251104061213.png)

---
### **1. Linguagens Compiladas (Ex: Go, C, C++)**

Esta primeira coluna ilustra o modelo clássico de compilação, usado por linguagens conhecidas pelo seu alto desempenho.
#### **1.1. Etapa de Development**

1. **Source Code:** É o código que você, o desenvolvedor, escreve em um editor de texto. 
    
2. **Compiler:** Você pega o seu código-fonte e o executa através de um programa especial chamado "Compilador" (como o `gcc` para C/C++). O compilador lê o seu código _inteiro_ de uma vez. Ele o <mark style="background: #ADCCFFA6;">analisa, otimiza e traduz diretamente para Machine Code.</mark>
    
3. **Machine Code (Resultado):** O resultado é um arquivo executável (como um `.exe` no Windows ou um binário no Linux). Esse arquivo contém as instruções binárias (os 0s e 1s) que a CPU do seu computador entende nativamente.

#### 1.2. Etapa de Runtime

1. **Machine Code:** Agora, o usuário pega esse arquivo executável e o executa.
    
2. **Operating System:** O SO carrega esse código de máquina na memória RAM.
    
3. **Hardware:** O SO entrega as instruções para o Hardware (especificamente, a CPU). A CPU executa essas instruções _diretamente_.

#### **1.3 Conclusão**

- **Vantagem:** A execução é extremamente rápida, pois o trabalho "pesado" de tradução foi feito _antes_ da execução. A CPU está apenas lendo sua língua nativa.
    
- **Desvantagem:** O "Código de Máquina" é específico para a plataforma onde foi compilado. Um `.exe` compilado para um PC Windows não vai rodar em um Mac ou em um celular Android. Você precisa _recompilar_ seu código-fonte para cada sistema diferente.