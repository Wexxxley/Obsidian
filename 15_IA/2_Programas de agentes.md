


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
    
1. O sensor pergunta: "Como está o mundo agora?"9.
        
    2. O programa encontra uma regra que corresponde a essa percepção (ex: `SE o mundo está sujo`)10.
        
    3. Ele executa a ação dessa regra (ex: `ENTÃO aspirar`)11111111.
        
- **Exemplo (Aspirador de Pó):** Os slides mostram o pseudocódigo exato12:
    
    - `se situação = Sujo então retorna Aspirar` 13
        
    - `senao se posição = A então retorna Direita` 14
        
    - `senao se posição = B então retorna Esquerda` 15
        
- **Limitação:** É muito simples e só funciona se a decisão correta puder ser tomada com base _apenas_ na percepção atual. Ele falha em ambientes parcialmente observáveis.
    

---

### 4. Tipo 2: Agente Baseado em Modelos

Este é um agente mais sofisticado, projetado para lidar com ambientes onde o agente não pode ver tudo de uma vez (ambientes parcialmente observáveis).

- **Como Funciona:** Para lidar com a informação que falta, o agente mantém um **estado interno** (uma memória) que representa sua crença sobre como o mundo está.
    
- **Mecanismo:** Além das regras, este agente precisa de um **modelo** do mundo16. Este modelo responde a duas perguntas:
    
    1. **Como o mundo evolui?** (O que acontece no mundo que eu não controlo?) 17
        
    2. **O que minhas ações fazem?** (Se eu me mover para a Direita, o que acontecerá com o estado?) 18
        
- **Fluxo de Decisão:**
    
    1. O agente recebe uma percepção.
        
    2. Ele usa sua memória (`estado` anterior 19), sua última `ação` 20, a nova `percepção` e seu `modelo` para **atualizar seu estado interno**21. Ele essencialmente recalcula "Como está o mundo agora?" 22 com base em sua memória e na nova informação.
        
    3. _Só então_ ele usa as regras condição-ação 23sobre esse _estado interno_ atualizado para escolher uma ação24.
        
- **Exemplo (Aspirador de Pó):** A Figura na página 16 25 é o **modelo** deste agente. É um diagrama de estados que mostra todas as 8 possíveis combinações de estados do mundo (ex: `[A: Robô Sujo] [B: Limpo]` 26) e como as ações (`Aspirar`, `Esquerda`, `Direita`) fazem o agente transitar entre eles.
    

### Resumo da Diferença

- **Reativo Simples:** (Percepção Atual) $\rightarrow$ (Ação). Não tem memória.
    
- **Baseado em Modelo:** (Percepção Atual + Estado Antigo + Modelo) $\rightarrow$ (Estado Novo) $\rightarrow$ (Ação). Tem memória e uma "teoria" de como o mundo funciona.