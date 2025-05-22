
________________________________________________________
# Flexbox
 O display flex é uma propriedade CSS que define um container flexível. Ele permite que os elementos dentro desse container sejam distribuídos de forma eficiente, independente do seu tamanho, com a possibilidade de alinhar, justificar e distribuir o espaço entre os itens de maneira mais controlada e responsiva. É a melhor maneira de organizar elementos dentro de um container

## **1. flex-direction:**
Define a direção principal do layout (se os itens serão organizados em linha ou coluna).
	- **row (padrão)**: Alinha os itens na horizontal. Deixa tudo em uma linha, ao ponto de ter que esticar as  imagens para fazer isso.
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHiVsQQ3Kp2wznsWqO0kaA1FJw0hk9GXnRlryBWksOKDiEuD9ItZqcDy98JiOGiif1wKSkp_tUpJ6VxUWVPOXCmUHD1ej9bFsdvnTdyrzrT7GcXJRrjQlZhxrxf2i62p04EgRC?key=VYJVAqKhTdZyHt8enJbiwA)
	**- column:** Alinha os itens na vertical (coluna).
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXesAM4mvvOX1YHveB__FigFvqWpqC-97CZO_6pGKLQPu88Fja8lEjEc0nyH29ASJd49_z9uV78BtmaM4J3C6LIHUvmPpZFgWwtZ6OXhMp6DPK3MMUIK4Owh3wp4A9rLkKVByh5X?key=VYJVAqKhTdZyHt8enJbiwA)
## **2. flex-wrap**
Cria uma nova linha ou coluna para comportar os elementos sem distorcê-los.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctaAlG9bhF65E2nKBsyZC5cHTWOUxr6l4ZhC1VNnZVHEg7zmCq8sjZwtNmekbKlhXsC_tObsmlhR0cHGKTLwiZa1tK0PRnBAXBJuqQKigBphgx48jP0aRRQOE8cGSSM9NC9ZWp?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeJlsKJi4ey_5P4gUNSEcPHg7Colw3I--QaJ5avYjh3PaaUC4kRMP6aFVonHcgoprggUU1QbTwkFYBV7_v-TH7MAnAEzDybpUhfz7HDKIsYHWrVHeWysRoVwCvMfENTbTfwYmRnTg?key=VYJVAqKhTdZyHt8enJbiwA)
- **Align content:** O align-content é uma propriedade do Flexbox que controla o alinhamento das linhas dentro de um contêiner multi-linha. Ele só faz efeito quando wrap está ativado e há múltiplas linhas dentro do contêiner.
## **3. justify-content**
Alinha os itens de acordo com o eixo principal estabelecido pelo flex-direction.
- flex-start (padrão): Alinha os itens ao início.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfKjTFP42SQ9h60spCJW6KvHA5JPQeqT0-HA8l1Cbh_ukL4_z9VPukH6xSuI4xB08D7ujd6q39vaHGhkW-Y9RSBj90nIgJ5Top-cVEUcHtu0yrzkU0AmaOBgEBqfzGHb-ExtUSuaw?key=VYJVAqKhTdZyHt8enJbiwA)
- flex-end: Alinha os itens ao final.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdlenHoHbUafO5rkNF2-9i0Ay--Wnjmjzx30gkFcvv45EPySTYhh3WZA3anM-yDnjH__3AtGUs4xzd-0zFlBSr5uPFWEcqTsFiu9UL6wXnqjEb85AnX3AyGM5hZwFdYrSmeMOEo?key=VYJVAqKhTdZyHt8enJbiwA)
- center: Centraliza os itens.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdgsNOWwFaSXCuSDRx2JQJmaFrCFhZd3UF7BX8Fl7WNw1FsixH_1g4-lj4e_CrVZ5oyoY9K-3PTHScQL1N9V3vV-9e7_yGFJbEbBpBBdV4f9gqnzCAJ-y75xBF2_rtoDyICHX_x?key=VYJVAqKhTdZyHt8enJbiwA)
- space-between: Distribui os itens com o maior espaço possível.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIAO8jlZA3BEnjsFmFblnc3oJhsXvYAh_5JppW3O0scGMCJmWz2O-9dN-Xa9P_9NUfhSU7_bfreNIlkqEhOuuqjhqDLGWWs-SDCSZtrkn_kr4Y5KYtnVOIt4JkYeB-2bsYYxj-pQ?key=VYJVAqKhTdZyHt8enJbiwA)
- space-around: distribui os itens e deixa respiros no começo e final. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdEWY_TeFtQqv8DD8HMUxpvc-rzu3JBRpYYZ5N_CUff6KWHk2uaRDm0FIifAREtF9KVT7Scod-OfcPeykmGPvaHftKGSDene7IfpT8J1d16NtClTs0XG7ab39UWcCOS9oWCKSmaRg?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXepmOWwToS7LlGYEGhBLRQLkQBdF0rZ6-KCWQZTmoqjGApz9H7X7CXucF-9zT8gKktc7TKY4KZegGngkBzecglP6nEUGbAS4_D0b5YChRJYU22Cd3kS9Gdh2JnIg2-Hk8H6cJozvQ?key=VYJVAqKhTdZyHt8enJbiwA)

## **4. align-items**
Alinha os itens no eixo contrário do estabelecido no flex-direction.
- flex-start
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc0tjkpI0ARtrunNsozu3fQdQe-xRTkJqEu0saZxpn_ekrrEuOlEK9BYS7tzleYFuwKKCgdg7C3gjf2LYQe2wibjC0oXK8HleO2fgorFalcgU36DzEhiKKKY3L_qYm65B6ocO-2kg?key=VYJVAqKhTdZyHt8enJbiwA)
- flex-end
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcxH5MABDaGjRHCwLDjM_2vQP0dtFVRnBWgOm4nAUAjTF6UszGQFN5Xd9dF528jod6pwDJPxdDCmHzo5N3GKQVj7Ebr161vj22R4q5tQ5ZiPufrhvfBSpTWsieGtC8Lv8Zp3lxtcg?key=VYJVAqKhTdZyHt8enJbiwA)
- center
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAYLfxE-L0xYB3mV33cBQB7Kq44VFpH_rfk-rAnbGtsR-g9bCyUoQMGJEe-ZxIPjWm1hqbsT3mi6GB4itBvm1v5Ipwux4LuqzPFhIVh7sybFqKWLsKByAUjvHE9isuKFaujZ2u?key=VYJVAqKhTdZyHt8enJbiwA)
- stretch: faz com que os elementos se estiquem para ocupar o espaço
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeE-FjqhKrz4KBkY07s6Duultp6NMuImEmEg5Y0Kxo3C9WD3aQX-0JDq8j5_YhpA9eL8K9KKj2c_3HuZQNPOLzSRub9U4e9WO-tGTDHOzakp2LEiVCTVH70BMFcgpmYM5D8B9s0AQ?key=VYJVAqKhTdZyHt8enJbiwA)

## **5. Gap**
Adiciona uma espaço entre elementos.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2WBw1bdBdagoOVEMRHPMcil0_xlklhnDFhtY6yrLUOOvDxcfVSZzuXEf8pVkYAzZAbzrSa9FusnDsnOe3n4pVNZhEHSST5D0cK1ZWJ2yMCd5QacTDgZsLQNKMr47owu3d5dG-?key=VYJVAqKhTdZyHt8enJbiwA)

## **6. GROW, BASIS E SHRINK**

 No Flexbox, as propriedades flex-grow, flex-basis e flex-shrink controlam como os elementos dentro de um container flexível se comportam em relação ao espaço disponível.
#### **6.1 flex-grow**
O flex-grow define a capacidade de um item flexível crescer e ocupar espaço extra dentro do container.
- flex-grow: 0; → O item não cresce (padrão).
- flex-grow: 1; → O item cresce proporcionalmente ao espaço disponível.
- flex-grow: 2; → O item cresce o dobro em relação a um item com flex-grow: 1 
![[Pasted image 20250522190124.png]]
  ![[Pasted image 20250522185953.png]]

2. flex-basis: O flex-basis define o tamanho inicial do item antes de o espaço extra ser distribuído.
Como funciona:

- flex-basis: auto; → O tamanho inicial do item é baseado no seu conteúdo (padrão).
    
- flex-basis: 50%; → O item começa ocupando 50% do container.
    
- flex-basis: 100px; → O item começa com 100px de largura.
    

3. flex-shrink: O flex-shrink define a capacidade de um item encolher quando o container não tem espaço suficiente.

Como funciona:

- flex-shrink: 0; → O item não encolhe.
- flex-shrink: 1; → O item encolhe normalmente.
- flex-shrink: 2; → O item encolhe o dobro em relação a um item com flex-shrink: 1.
    

  

4. Atalho): Podemos usar um atalho para definir as três propriedades de uma vez:

  flex: <grow> <shrink> <basis>;

  