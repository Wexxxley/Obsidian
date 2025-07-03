
---

Na camada física temos os **meios de transmissão cabeados** (Par trançado, cabo coaxial e fibra óptica).

### **1. Cabo de Par trançado**
Tipo de cabeamento **mais comum** usado em redes de computadores locais (LANs). Ele consiste em quatro pares de fios de cobre finos, onde cada par é trançado em conjunto e todos os pares são envoltos por uma capa protetora externa de plástico. A extremidade desses cabos é geralmente conectada a um conector chamado **RJ-45**.
![[Pasted image 20250703102837.png|350]] ![[Pasted image 20250703102939.png|250]]
#### **1.2 Por que os Fios são Trançados?**
- Fontes de ruído elétrico, como motores, cabos de energia e outros dispositivos eletrônicos, geram campos magnéticos. Esses campos podem gerar interferência no cabo.
- Dentro de um par, os dois fios transmitem sinais iguais, mas com polaridade oposta. Ao trançar os fios, eles trocam de posição constantemente. Isso significa que, em um ponto, o fio A está mais perto da fonte de ruído e, no seguinte, o fio B está. Ao longo do cabo, a quantidade de ruído em ambos os fios se torna praticamente a mesma. No dispositivo receptor, o circuito subtrai um sinal do outro. 
        
2. **Cancelamento de Diafonia (Crosstalk):**
    
    - **O Problema:** O sinal que passa por um par de fios gera seu próprio campo magnético, que pode "vazar" e interferir nos sinais dos outros pares de fios dentro do mesmo cabo. Isso é chamado de diafonia ou "crosstalk".
        
    - **A Solução (O Trançado):** O mesmo princípio de cancelamento se aplica aqui. Como os fios de um par têm sinais opostos, os campos magnéticos que eles geram também são opostos e tendem a se anular. Isso reduz drasticamente a interferência de um par sobre o outro, permitindo que vários sinais trafeguem pelo mesmo cabo sem se corromperem.
        

Em resumo, **o trançamento é uma forma passiva e eficaz de proteger a integridade do sinal**, garantindo uma comunicação mais estável e confiável.

### Benefícios do Par Trançado

- **Custo-Benefício:** É significativamente mais barato de produzir e instalar do que outras alternativas, como a fibra óptica.
    
- **Flexibilidade e Facilidade de Instalação:** Os cabos são finos, flexíveis e fáceis de manusear e crimpar (conectar o conector RJ-45).
    
- **Padronização:** É uma tecnologia amplamente estabelecida e padronizada (com categorias como Cat5e, Cat6, etc.), o que garante compatibilidade entre equipamentos de diferentes fabricantes.
    
- **Bom Desempenho para LANs:** Oferece velocidade e largura de banda mais do que suficientes para a maioria das aplicações domésticas e de escritório.
    

### Desvantagens e Limitações

- **Limitação de Distância:** O sinal em um cabo de par trançado se degrada com a distância (atenuação). Para redes Ethernet, o comprimento máximo recomendado é de **100 metros**. Para distâncias maiores, é necessário usar um repetidor, switch ou optar por fibra óptica.
    
- **Suscetibilidade a Interferência Severa:** Embora o trançamento ajude muito, ele não torna o cabo imune a fontes de interferência eletromagnética muito fortes, como as encontradas em ambientes industriais.
    
- **Largura de Banda Menor que a Fibra:** Comparado à fibra óptica, sua capacidade de transmissão de dados (largura de banda) é muito menor.
    
- **Segurança:** É possível interceptar os sinais de um cabo de cobre com equipamentos específicos ("wire tapping") de forma mais fácil do que em um cabo de fibra óptica.
    

### Tipos Comuns: UTP vs. STP

Existem dois tipos principais de cabos de par trançado, diferenciados pela presença ou ausência de blindagem adicional.

- **UTP (Unshielded Twisted Pair - Par Trançado Não Blindado):**
    
    - É o tipo mais comum e mais barato.
        
    - Não possui nenhuma blindagem metálica extra, dependendo exclusivamente do efeito de cancelamento do trançamento dos pares.
        
    - É usado na grande maioria das redes domésticas e de escritórios.
        
    - Exemplos: Cat5e, Cat6.
        
- **STP (Shielded Twisted Pair - Par Trançado Blindado):**
    
    - Possui uma blindagem metálica (geralmente uma folha de alumínio ou malha de cobre) que envolve os pares de fios.
        
    - Essa blindagem oferece uma camada extra de proteção contra interferência eletromagnética severa.
        
    - É mais caro, mais rígido e mais difícil de instalar.
        
    - É utilizado em locais com alto nível de ruído elétrico, como fábricas, hospitais ou perto de equipamentos de alta potência.
        
    - Exemplos: Cat6a, Cat7, Cat8.
        

### Conclusão

O cabo de par trançado representa um equilíbrio perfeito entre custo, desempenho e facilidade de uso. Sua técnica de trançar os fios para cancelar ruídos foi uma inovação que permitiu a criação de redes locais acessíveis e confiáveis, tornando-se a espinha dorsal da conectividade com fio em todo o mundo. Embora tenha limitações de distância e largura de banda, ele continua sendo a escolha ideal para a vasta maioria das conexões de rede local.