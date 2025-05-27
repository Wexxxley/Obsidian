
Status: #Concluded 

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

 O **box-sizing** é uma propriedade que define como o navegador deve calcular o tamanho total de um elemento. Ele determina se o padding e a borda são incluídos no tamanho total ou não.

1. **content-box (padrão):** Apenas o conteúdo é contabilizado no valor de width e height. O padding e a borda não são incluídos e aumentam o tamanho total.
2. **border-box:** Inclui o padding e a borda no valor definido de width e height. O border-box é amplamente preferido porque simplifica o cálculo do tamanho total.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc0NcGl7Wa9At1ZqTxb0j_xaA_mt1wb1vIFBD_OFSdcnqzahQyEpkeEEbuK0BQ6l5j1N8vmMhu90Y57SqKPpi7XLf53FymykgY0g17P_QdJgne__0vIEpkgf5pizgX4YyYYwoTarw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc4Q0fdqyGtk2HWaboYQSMaEnGbQlRgZRd38M7gJjxrblgVwGP-iccZRJA1-ESoh2m0FF62ygQwsjB7hPBjPX-Ncmu-aRK8Dr491iVHmSasqPeZUugbhR1sziueKv2F358URUyd2g?key=VYJVAqKhTdZyHt8enJbiwA)

Quando você for começar a mecher no estilo de uma pagina é interessante zerar esses valores.
![[Pasted image 20250522174655.png]]

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
# **4. Tipos de caixa**

O **comportamento visual das caixas** depende do valor da propriedade `display`. Por padrão, existem dois tipos principais: block e inline.
#### **a) Caixa de bloco (`block`)**
- Ocupa toda a largura disponível (por padrão).
- Quebra linha antes e depois.
- Permite definir largura (`width`) e altura (`height`).
**Exemplos de elementos que usam display block: `<div>`, `<p>`, `<h1>`, `<section>`.
#### b) Caixa inline (`inline`)**
- Ocupa apenas o espaço necessário ao conteúdo.
- Não quebra linha antes ou depois.
- Ignora `width` e `height`.
- Apenas aceita `padding` e `margin`.
**Exemplos de elementos que usam display inline: `<span>`, `<a>`, `<strong>`.
#### c) Caixa inline-block (`inline-block`)**
- Não quebra linha automaticamente, mas respeita `width`, `height`, `padding`, `margin` como bloco.
#### **d) Caixas flexíveis (`flex`)**
- Caixa que se comporta como **contêiner flexível**, distribuindo seus filhos com `display: flex`.
- Permite criar layouts responsivos facilmente.
[[4_Flexbox]]

---
# **5. Propriedade `display:`**
Define **como um elemento será exibido** e como suas caixas serão tratadas.

| Valor          | Descrição                                      |
| -------------- | ---------------------------------------------- |
| `block`        | Elemento de bloco                              |
| `inline`       | Elemento inline                                |
| `inline-block` | Combinação de inline e block                   |
| `flex`         | Contêiner flexível                             |
| `none`         | Elemento não será renderizado (fica invisível) |

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
.hidden {
  display: none;
}
```

---
# 6. Mais sobre largura e altura 

- `min-height: 70vh;` significa que o elemento terá pelo menos 70% da altura da janela de visualização. Se o conteúdo for maior que 70vh, o elemento cresce para acomodar o conteúdo.
- Se o conteúdo for menor, o elemento nunca ficará menor que 70vh.

**Derivados:**

- `height`: Define a altura exata do elemento. O elemento terá sempre essa altura, a menos que o conteúdo force um aumento (dependendo do overflow).
- `max-height`: Define a altura máxima. O elemento nunca ficará maior que esse valor, mesmo que o conteúdo seja maior (pode causar rolagem interna se o overflow permitir).

**Resumo:**

- `min-height`: altura mínima.
- `height`: altura fixa.
- `max-height`: altura máxim