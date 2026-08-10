
#Concluded 

---
Sombras são uma ferramenta de design fundamental para criar <mark style="background: #ADCCFFA6;">a ilusão de profundidade e hierarquia numa interface.</mark> Elas fazem com que os elementos pareçam "flutuar" acima do fundo, ajudando o utilizador a entender o que é clicável, o que é importante e como os elementos estão organizados.

Existem duas propriedades principais para sombras:
1. `box-shadow`: Aplica uma sombra à "caixa" de um elemento.
2. `text-shadow`: Aplica uma sombra diretamente ao texto dentro de um elemento.

---
### 1. box-shadow

```css
box-shadow: [offset-x][offset-y][blur-radius][spread-radius][color][inset];
```

- `offset-x` (obrigatório): O deslocamento horizontal da sombra.        
- `offset-y` (obrigatório): O deslocamento vertical da sombra.
- `blur-radius` (opcional): O raio de desfoque. É o que deixa a sombra "esfumaçada" e suave.
    - `0px` cria uma sombra com bordas totalmente nítidas. Quanto maior o valor (ex: `16px`), mais desfocada e suave a sombra se torna.
- `spread-radius` (opcional): O raio de expansão. Faz a sombra crescer ou encolher
    - Um valor positivo (ex: `5px`) faz a sombra aumentar de tamanho em todas as direções.        
    - Um valor negativo (ex: `-5px`) faz a sombra encolher.
- `color` (opcional): A cor da sombra.
    - Quase nunca use preto puro. A melhor prática é usar um preto com transparência, como `rgba(0, 0, 0, 0.25)`.
- `inset` (opcional): Uma palavra-chave que muda a sombra de externa (padrão) para interna, fazendo o elemento parecer "pressionado" ou afundado.


**1. Sombra Básica e Dura (estilo "adesivo")**

```css
.elemento {
  box-shadow: 4px 4px 0px #111; /* Sem blur, a borda é nítida */
}
```

**2. Sombra Suave e Realista (A mais usada em UIs modernas)** É a que você usou no seu projeto.

```css
.elemento {
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.5); 
}
```

**3. Sombra Interna (Efeito "pressionado")** Ótima para campos de formulário quando estão ativos (`:focus`) ou para botões pressionados.

```css
.input-field:focus {
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.4);
}
```

---
### 2. text-shadow

```css
text-shadow: [offset-x] [offset-y] [blur-radius] [color];
```

