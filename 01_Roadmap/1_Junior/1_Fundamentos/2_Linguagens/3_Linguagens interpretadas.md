
#Concluded 

---
![650](../../../../attachments/Pasted%20image%2020251104061213.png)

---
### 1. Linguagens Interpretadas (Ex: Python, JavaScript, Ruby)

Este modelo é conhecido por sua simplicidade, flexibilidade e rapidez no desenvolvimento.
#### 1.1. Etapa de Development

1. **Source Code:** Você escreve seu código (ex: um arquivo `.py` ou `.js`).
    
2. **Ready to Use! :** Não existe um passo de compilação separado que o desenvolvedor precise executar. O próprio arquivo de código-fonte _é_ o programa que será distribuído.

#### 1.2. Etapa de Runtime

1. **Source Code:** Quando é hora de rodar, o **código-fonte** é entregue a um programa especial.
    
2. **Interpretador:** Este é o ambiente de execução (como o programa `python.exe` ou o motor V8 do Google Chrome).
    
3. **O Processo de Interpretação:** O interpretador lê o seu código-fonte **linha por linha**.    
    - Para cada linha, ele:
        1. Lê a instrução (ex: `print("Olá")`).
        2. Analisa o que ela significa.
        3. Traduz _na hora_ para instruções que o Sistema Operacional e o Hardware entendem.
        4. Executa essa instrução.
        5. Passa para a próxima linha.
            
4. **Operating System e Hardware:** O interpretador faz a ponte, enviando os comandos traduzidos para o SO, que por sua vez os executa no Hardware (CPU).
    
> [!NOTE]
> A imagem simplifica um pouco. Interpretadores modernos, como o do Python e o V8 do JavaScript, são muito inteligentes. Eles _também_ usam Bytecode e Compiladores JIT por baixo dos panos para otimizar o desempenho, tornando-os muito parecidos com o modelo híbrido do Java. No entanto, o modelo _fundamental_ e a forma como o desenvolvedor interage com eles é "interpretado": não há um passo de compilação explícito.

#### **1.3 Conclusão**

- **Vantagem:** É extremamente fácil e rápido começar. Você escreve o código e o executa. Além disso, o mesmo arquivo `.py` ou `.js` roda em qualquer Windows, Mac ou Linux que tenha o interpretador correto instalado.
    
- **Desvantagem:** Historicamente, a interpretação pura (linha por linha) é a forma mais lenta de execução, pois o trabalho de tradução é refeito _toda vez_ que o programa roda.