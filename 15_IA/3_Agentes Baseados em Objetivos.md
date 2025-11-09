

---

Este agente não se baseia mais em "Regras condição-ação" pré-programadas para cada situação. Em vez disso, ele tem **Objetivos**. 
    
Em vez de apenas reagir, este agente **planeja**. Ele considera sequências de ações futuras para encontrar uma que o leve ao seu estado de objetivo. Isso levanta três questões centrais:
    
1. Como definir um problema?         
2. Como definir um objetivo? 
3. Como construir algoritmos que alcancem os objetivos? 

### 1. Formulção de problemas

Um problema é composto por **cinco componentes**:

1. **O Estado Inicial:** Onde o agente começa.
    
2. **Uma Descrição das Ações:** O que o agente _pode_ fazer em um determinado estado $s$. (definido como $ACOES(s)$).
    
3. **Um Modelo de Transição:** O que uma ação $a$ faz no estado $s$. (definido como $RESULTADO(s, a)$).
    
4. **O Teste de Objetivo:** Uma forma de determinar se um estado específico é o estado-objetivo.
    
5. **Um Custo de Caminho:** Uma função que atribui um custo a uma sequência de ações (caminho).

---
### 2. Exemplo: O Mapa da Romênia

- **Estado Inicial:** "Em Arad"21.
    
- **Ações:** "Ir para Sibiu", "Ir para Zerind", "Ir para Timisoara".
    
- **Modelo de Transição:** `RESULTADO("Em Arad", "Ir para Sibiu")` = "Em Sibiu".
    
- **Teste de Objetivo:** "Estamos em Bucharest?".
    
- **Custo de Caminho:** A soma das distâncias em km entre as cidades.
    
