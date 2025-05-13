

___
# 1. Box model
 Os elementos do html estão dentro de caixas. Caixas são contêineres que armazenam conteúdo e até outras caixas e são muito importantes para organizar o design do seu site.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfCuMvs8mFQCyouusrz7U22PodT9YKpz5ykHZwVGsa3IoYJ2P80Dg-FC1R8l8Kq8JRVbRJxo0pnUrRBETTs0dtNlF3No17ZHX7WIm_H64w-AmcyrKMTdXraN-Jl-645dG6wlABD52xWhHTeDGgmQewFHQX2?key=VYJVAqKhTdZyHt8enJbiwA)
- Width: Largura do conteúdo.
- Height: Altura do conteúdo.
- Padding: É o preenchimento entre conteúdo e borda.
- Border: Borda da caixa que pode ter espessura, tamanho e formato.
- Outline: É o contorno, traçado fora da borda.
- Margin: Margem que serve como um espaçamento com outras caixas.
 
**Padding**: Você pode ajustar o padding de modo geral, de forma individual e de forma individual com um comando.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJ_zic0cX_SaxogBNltOMB5FginKhkwQO40ls-ck_MQPFRmQHtGkNAK7d3hgeOCaDrP9F1Mg7Pj28WsiUfT1bK8Wwxqz_zS3dMjoM5SmC6FOyXFHTRt-UvCG9HZ-Z0a3LnkXmUfQ?key=VYJVAqKhTdZyHt8enJbiwA)
Obs: o margin funciona da mesma forma que o padding.

___
# 2. Respeitando medidas com o box-sizing

 O box-sizing é uma propriedade que define como o navegador deve calcular o tamanho total de um elemento, especialmente em relação à largura e altura. Ele determina se o padding e a borda são incluídos no tamanho total ou não.

1. **content-box (padrão):** Apenas o conteúdo é contabilizado no valor de width e height. O padding e a borda não são incluídos e aumentam o tamanho total.
2. **border-box:** Inclui o padding e a borda no valor definido de width e height. O border-box é amplamente preferido porque simplifica o cálculo do tamanho total.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc0NcGl7Wa9At1ZqTxb0j_xaA_mt1wb1vIFBD_OFSdcnqzahQyEpkeEEbuK0BQ6l5j1N8vmMhu90Y57SqKPpi7XLf53FymykgY0g17P_QdJgne__0vIEpkgf5pizgX4YyYYwoTarw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc4Q0fdqyGtk2HWaboYQSMaEnGbQlRgZRd38M7gJjxrblgVwGP-iccZRJA1-ESoh2m0FF62ygQwsjB7hPBjPX-Ncmu-aRK8Dr491iVHmSasqPeZUugbhR1sziueKv2F358URUyd2g?key=VYJVAqKhTdZyHt8enJbiwA)

___
# 3. Bordas 

1. border-color:  edita cor da borda.
2. border-width: edita largura da borda.
3. border-style:  edita o estilo (solid, double, dashed,dotted, groove)
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdLiqj87k96_H2DoyOA8V-bu0S6K4CAK117bnvMDPYLAZn5f-CLboWT5NWS1VG2scOhdHbLCfzFHNT160thdgG6qJFac9pnWkSbEi4BLw3OW8FYeO3uNTO43HnkhzmIr4hNuf1Mcg?key=VYJVAqKhTdZyHt8enJbiwA)

**Arredondamento**: O arredondamento de bordas é feito com a propriedade border-radius. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJoexbfLpPKxzlxCMx8_I2R29FhvhfGKhq5OY7fCCESAPxyEU2wNvXT0mrWHFGsuRQmUqOjvAGmV4NVyc_YhL41lEhO8HscaWcvtrB9DYqavLy9od4crHDOAudlzKOrCrtF64kEA?key=VYJVAqKhTdZyHt8enJbiwA)
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcE1x3gUPldOChmQ0xu2RSo5UnGYFwLRGuRraP3n5oruFk5OKY2Sw9G6mYTKt_h4f4d_5estezaajAYFXHwa9p4RZPuRtEgbm8lKbWkuAnYjUnaoOkebN_N-FhEg23RkGid50X3GA?key=VYJVAqKhTdZyHt8enJbiwA)


___
# 4. Tipos de caixa

O **comportamento visual das caixas** depende do valor da propriedade `display`. Por padrão, existem dois tipos principais: block e inline.
#### **a) Caixa de bloco (`block`)**
- Ocupa toda a largura disponível (por padrão).
- Quebra linha antes e depois.
- Permite definir largura (`width`) e altura (`height`).

**Exemplos de elementos que usam display block: `<div>`, `<p>`, `<h1>`, `<section>`.
#### b) **Caixa inline (`inline`)**
- Ocupa apenas o espaço necessário ao conteúdo.
- Não quebra linha antes ou depois.
- Ignora `width` e `height`.
- Apenas aceita `padding` e `margin`.

**Exemplos de elementos que usam display inline por padrão:**

- `<span>`, `<a>`, `<strong>`, `<em>`, etc.
    

##### c) **Caixa inline-block (`inline-block`)**

- Mistura características de `block` e `inline`.
    
- Não quebra linha automaticamente, mas respeita `width`, `height`, `padding`, `margin` como bloco.
    

##### d) **Caixas flexíveis (`flex`)**

- Caixa que se comporta como **contêiner flexível**, distribuindo seus filhos com `display: flex`.
    
- Permite criar layouts responsivos facilmente.
    

##### e) **Caixa grid (`grid`)**

- Comporta-se como contêiner de grade, permitindo organização bidimensional de elementos com `display: grid`.
    

---

### Propriedade `display:`

Define **como um elemento será exibido** e como suas caixas serão tratadas.

#### Principais valores:

|Valor|Descrição|
|---|---|
|`block`|Elemento de bloco|
|`inline`|Elemento inline|
|`inline-block`|Combinação de inline e block|
|`flex`|Contêiner flexível (layout em linha ou coluna)|
|`grid`|Contêiner de grade (layout em linhas e colunas)|
|`none`|Elemento não será renderizado (fica invisível)|

#### Exemplos práticos:

```css
div {
  display: block;
}

span {
  display: inline;
}

button {
  display: inline-block;
}

.container {
  display: flex;
}

.grid-container {
  display: grid;
}

.hidden {
  display: none;
}
```

---

Quer que eu te faça um **esquema visual simples mostrando os tipos de caixas e como elas se comportam no layout?**  
Se quiser, é só dizer "**sim, esquema**".



1. Block-level: Sempre se inicia em uma nova linha e ocupa a largura total do elemento onde ele está contido.

Ex:<div>,<h1>,<p>.

É possível transformar block-level em inline com “display: inline”.

  

2. Inline-level: Se inicia na mesma linha e a largura é do tamanho do conteúdo

 Ex:<span>,<a>,<code>,<strong>,<button>,<sup>,<sub>.

É  possível transformar inline em block com “display: block”.

  

Tags dentro

- Block-level: Pode conter outros block-level e inline dentro
    
- Inline-level: Só pode conter outros inline-elements. Colocar uma <div> dentro de um <span> é inválido!
    

  

Largura e altura

- Block-level: Pode ter largura (width) e altura (height) definidas normalmente.
    
- Inline-level: Não respeita altura nem largura! Só muda isso se você transformar ele com display: block ou inline-block.
    

  

Margin e Padding

- Block-level: margin e padding funcionam em todas as direções.
    
- Inline-level: padding e margin horizontal funcionam, mas o vertical não.
    

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  