


---

A "inteligência" do agente é definida pela fórmula: <mark style="background: #FFB86CA6;">Agente = Arquitetura + Programa</mark>.

**Arquitetura:** O hardware onde o agente roda (os sensores e atuadores físicos)

**Programa:** O software que toma as decisões. É a implementação da função que mapeia percepções em ações.

---
### **1. Tipos de Programas de Agentes**

1. Agentes reativos simples
    
2. Agentes reativos baseados em modelos
    
3. Agentes baseados em objetivos
    
4. Agentes baseados em utilidade
    
5. Agentes baseados em aprendizagem

---
### 2. Agente Reativo Simples

Ele baseia suas ações _apenas_ na percepção atual. Ele não tem memória do passado e não pensa no futuro. Ele usa um conjunto de **Regras condição-ação**. 

- **Exemplo (Aspirador de Pó):** 
    - se situação = Sujo então retorna Aspirar.
    - senao se posição = A então retorna Direita.
    - senao se posição = B então retorna Esquerda.
        
- **Limitação:** É muito simples e só funciona se a decisão correta puder ser tomada com base _apenas_ na percepção atual. Ele falha em ambientes parcialmente observáveis.

---
### 3. Agente Baseado em Modelos

Para lidar com a informação que falta, o agente mantém um **estado interno** (uma memória) que representa sua crença sobre como o mundo está. Além das regras, este agente precisa de um **modelo** do mundo. 

- (Percepção Atual + Estado Antigo + Modelo) $\rightarrow$ (Estado Novo) $\rightarrow$ (Ação). Tem memória e uma "teoria" de como o mundo funciona.

![](../attachments/Pasted%20image%2020251108183523.png)