
---
### **1. BGP (Border Gateway Protocol):**
A  função do BGP é permitir que diferentes Sistemas Autônomos troquem informações de roteamento sobre os prefixos IP que controlam e os caminhos que podem usar para alcançar outros prefixos. Ele toma decisões de roteamento baseadas em políticas, atributos de caminho e caminhos completos.

Quando um Sistema Autônomo anuncia um prefixo via BGP, ele está dizendo: =="Olá, outros ASes! Eu sou o AS X, e eu sou o responsável por este bloco de endereços IP== (Ex, `203.0.113.0/24`). Se você tiver tráfego destinado a qualquer endereço IP dentro deste bloco você pode enviá-lo para mim, e eu sei como entregá-lo.

Os contratos de emparelhamento e de trânsito estabelecidos entre provedores são os motivadores por trás de muitas das decisões de roteamento que vemos na internet global.


---
#### **1.2 Sessões BGP**
Usam o TCP para confiabilidade.
- **Sessão eBGP:** Usada para estabelecer sessões entre roteadores de borda em diferentes Sistemas Autônomos vizinhos. Através dessas sessões, os ASes trocam informações de prefixos que controlam ou que podem alcançar.
- **Sessôes iBGP**: Uma vez que um roteador de borda aprende uma rota externa, ele precisa anunciar essa rota para outros roteadores dentro do seu próprio AS para que eles saibam como rotear o tráfego para fora.
 
![[Pasted image 20250606100212.png]]
- Quando AS2 comunica um prefixo ao AS1, AS2 está prometendo que irá encaminhar todos os datagramas destinados a esse prefixo em direção ao prefixo.
- Quando um roteador aprende um novo prefixo, ele cria uma entrada para ele em sua tabela de roteamento.

---
#### **1.2 Prefixos + atributos = rota**
- **Atributo NEXT_HOP:** ==O endereço IP do próximo roteador no caminho para o prefixo de destino==. Para eBGP, é o endereço do roteador vizinho. Para iBGP, é o endereço de um roteador de borda.
- **Atributo AS_PATH:** Lista ordenada de ASes que o tráfego atravessaria para chegar ao destino. Cada vez que um prefixo é anunciado por um AS, o AS de origem adiciona seu próprio número de AS ao AS_PATH. O BGP prefere caminhos com AS_PATH mais curto.

---
#### **1.3 Processo de Seleção de Rota do BGP**
Um roteador pode aprender mais do que 1 rota para o mesmo prefixo. O roteador deve selecionar uma rota usando as regras de eleiminação.

- Atributo de valor de preferência local: decisão de política.
- AS-PATH (caminho) mais curto
- Roteador do NEXT-HOP (próximo salto) mais próximo: roteamento da “batata quente”.
- Critérios adicionais .


