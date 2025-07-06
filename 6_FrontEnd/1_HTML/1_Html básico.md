Status: #Concluded 

---

Html é a linguagem de ==marcação== usada para estruturar páginas web, criando elementos de texto, inserindo imagens, listas, tabelas, ou seja, é responsável pelo conteúdo do site.

**Tags**: Servem para indicar um tipo específico de estrutura na página. São usadas também para que o navegador consiga diferenciar os elementos do site. O que é um parágrafo, um título, subtítulo etc. Uma tag geralmente é composta por:
- Tag de abertura
- Conteúdo
- Tag de fechamento

---
# **1. Iniciando**

No vscode, existe um atalho para configurações iniciais, que é o atalho ‘!’.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcxdfXBONlVJwf4esB9VIkOuRa74oHTofhrQ0QoTIcAl9W2ci3q-Yp4Xvg6iV5AoMM1l80mgDJc9RE0YiMsCiDo9P5zTzfWNMio147AvK_bml9roowRYhS5RqB6Oe2bpxapUN_P-Q?key=VYJVAqKhTdZyHt8enJbiwA)

___
# **2. Títulos e atributos de tag**

Títulos em html possuem 6 níveis. `<H1>, ..., <H6>`. Essas tags não se preocupam com a forma dos títulos, mas sim com o sentido. 

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfpuiFlvHtVNxdD3UM6g4YLpOX9tn51wfbiZ8wC5tDtuJJMbDp9KeOHTFLobiVywTXjmTmYHav9JLIksdyqvQqhzp7llZ5Ru_gxX2Q9ZJBaDNo52njKOl9kl87JiLMZOYo96fNk3A?key=VYJVAqKhTdZyHt8enJbiwA)

**Atributos**
Atributos são utilizados para adicionar funcionalidades às tags. 
> [!NOTE]
> Ex: a tag `<a>` é utilizada para nos direcionar a uma nova página ou site. E o endereço é adicionado em um atributo. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9CH49oL40UiGm3UITOoyINBpPr8hJbIu42Xns26FQBOj6K42FrmJKE9obsGjwfYcoKW6ZEZLlFOZYCEDSYaQ_A_oSTcmIMrQC941QTGBYyArV9FhEcubEMpZG24PYAKpHAu3Mdg?key=VYJVAqKhTdZyHt8enJbiwA)

---
# **3. Link**

**Link externo:** Se seu link leva para outro site recomenda-se abrir uma nova aba.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOOr839rfiCq44TC7Y_g6qm5fF_fJpawlaIo_jLPfuTxIEfQWbHAl1dtMpqU8rVKrTQqLN2aaYsL5zyIHGnSAUkQ_SA5Jd27QaEtW8UT38lzrKDP3KbZC0B0i6t3Pe9EQG2KwaJw?key=VYJVAqKhTdZyHt8enJbiwA)

**Link Interno**: Quando seu link é do seu site não se cria uma nova aba.
- Na página principal: ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdrj8PTKmRLixCrIpvGUoz1oqxFead7HqM1f0smgxE2xFeJ24qLHUuFQD8rBNgcp91XYw9RMpTLvB45ytRpdYRm9AuRE46VDRe4lbRIw6k6PCKGknDimO20nwoOjeBFb4XyN_Yb?key=VYJVAqKhTdZyHt8enJbiwA)
- Na página secundária: ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd8N0FKulg5AdD9fDjsJzNp7dSEK0u0kF55VIGNzZDpmEnfv9JXCaenVeHnqkCGNiy-aMqG54EqslUMGE6ypbhQ6z8oxYVY0srajzN4P8PObCCUKvPKfQymSAZqyDRBQNJzB_Wy?key=VYJVAqKhTdZyHt8enJbiwA)

 O **Atributo target** Suporta “ _blank” que vai abrir o link em uma nova janela em branco e “_self” vai abrir o link na janela atual (padrão). 

O **Atributo rel** indica qual é a natureza de destino do link.

1. **next** indica que o link é para a próxima parte do site .
2. **prev** indica que o link é para a parte anterior do site atual.
3. **external** indica que é um link para um site externo.

___
# **4. Imagem**

Obs: normalmente é colocado as imagens em uma pasta img ou assets.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczRCsCFPRr0NbCsIMT9NPpR4C9y6Fa-ou4pfPgPzhwO2iU8oi7mkNGapyyj-OqAUd85sMvGMheFrjOtc3l2SVV6kfCxnsh_H3AHJmw1mP0YRgNaBurP3bbIrCcO6_KUdV8WiHE1w?key=VYJVAqKhTdZyHt8enJbiwA)

**src**: caminho da imagem.

**alt**: texto que descreve a imagem para fins de acessibilidade. 

___
# **5. Listas**

**Lista ordenada**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSycmZrRa3b-ccA8udwgfSkpmCyPfDTyhI-0szikNQK5p0mT9TlSBJCsmwOyr1nzNMb_bpWuGgcQtRa68MpYMV9bohiX4ihIdqWIvvRcIPbaOHy3nCOCTkkBJ5eX831lzrUmsQVQ?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXesEgpQuOg24WXTYcPQ6E-UmADGxQABAlfrBqN4RwO1FiBfNLx5Uc9wuYb1Qyitpr914B62UDMXUDzCvUlMXUDqBdZc7L5Q_6N1hUzMrK-TOxP_UvUhprtHUo1nHf37kfCTfotz?key=VYJVAqKhTdZyHt8enJbiwA)

`<ol>` - ordered list
`<li>` - list item 

**Lista não ordenada**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfg5EeC0DuXh-mX43eD9_inA9i0wt8oKdLJ1HgQz6A2IM4i8ZO0Kd_HIjtRzlN667eW0z-bGY8478G2FeQBrWkqADOoff53Zqs8rfLdyt6-rZol7se29iXb6_9bJ-3QAtF8KUSWzQ?key=VYJVAqKhTdZyHt8enJbiwA) ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUDoGGnQFDwNXhRU_HduM0x8kMWKMY3zX6241SrFNFPuItN-rEkTaayVb7FMhZmpy3D-bs_yHG618Ku8tYo_uQmRkpFMWykXfDamDhXU-eHmQfgxzpgn6MOnosJqnYtwJ5XwXAfA?key=VYJVAqKhTdZyHt8enJbiwA)

`<ul>` - unordered list
___
# 6. Tabelas

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOgQ67sw761N9ILprWOxLOAnZYESusLHIeSDdCpxUTPz42NouT5CkG4udXiZtzEasq4tW9Xsv8Q9atAknZngPiLn-l8oYpZ2JX6suvixt3nt4JAvHB-BRIfFPfX8ojaJIbdpheig?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfCtQhvLv19OU41B-S3hD4s2sFUEOdpj3LJVIZ5fjk-PSJB5A31iMmxgLhz1t-I7JxZl6omQ8_hdspsh1V512rxJVlZBQu6jYeyVWvqvpJJN8AYZ-IDG-7nKjQUUaLXa6CoxBdR1g?key=VYJVAqKhTdZyHt8enJbiwA)

`<table>`: Cria a tabela.

``<tr>``: table row

``<th>``: table header

``<td>``: table data

``<caption>``: Adiciona um título descritivo para a tabela.

``<thead>, <tbody>, <tfoot>``: Servem para organizar visual e semanticamente a tabela em: Cabeçalho, Corpo, Rodapé. 

``<colgroup> e <col>``: Servem para aplicar estilos ou configurações em colunas inteiras, sem precisar repetir nas células.  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9xQIUmmBaWPpvNIG0sKoeX2-TE3_BGvZTilVq-lT_lXfYcBW2Kxq3_4QXQOcVeUUrdb55b8TRlz7fRnAE8zPGIXYFH1-ZkOC_w8BTkDEId4xV12PtSpxew5VhsxfyUbS3lj7t0g?key=VYJVAqKhTdZyHt8enJbiwA)

Para mudar a estilisação das linhas usamos ``tr:nth-child``

![Pasted image 20250506072646](../../attachments/Pasted%20image%2020250506072646.png)

Com ``colspan`` eu consigo unir colunas de uma linha.

![Pasted image 20250506072825](../../attachments/Pasted%20image%2020250506072825.png)

![Pasted image 20250506072723](../../attachments/Pasted%20image%2020250506072723.png)

___
# **7. Formatação de texto e citações**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfKE3lGHi0HHeMWCOiGQCLLgL7GPH2z5bS616fEIzqpDclZ4MP8rOJ7dSlxf238QOFoE5Yx683uBNkv9ydqdYo6l6DUjZZ35b0d6GbfEwwz-g3Bq2biNSrDeIUxZK6lFHoqGTn-Qw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf87MuJNRFOjO-4XtqJg9mA3qRSRZ5OiWmP4cQOd8ftBp2IByq1jxMO0W3Q4JHsNVYWSh_TfxjOFYb2evZCWfz3BVigZ0ioP0iJGEvD_cbqsUWrO4Q-2ZOXlXusyaxJ0L3o96rJ4g?key=VYJVAqKhTdZyHt8enJbiwA)

- ``<blockquote>``: Usada para citações longas, geralmente de outra fonte. 
- ``<q>``: Usada para citações curtas.
- ``<abbr>``: Usada para abreviações ou siglas, com explicação completa. 
- ``<address>``: Usada para informações de contato, como nome, email, endereço, etc.
- ``<cite>``: Usada para referenciar o título de uma obra (livro, site, filme, música, etc).
- ``<pre>``: Usada para mostrar texto com formatação preservada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXedaI0YsDGd_XCax5WqfXc6jM3lCit9dvcRm5BZVBp7QpMiRqFhb0FdX9eTCXrr1yPD_Z9dDDckbXXOIxgpuyAyOCQqFRM8CZT5YyaglZDpoSJxH0Th8XhBae1u2qtWRZqUExetNQ?key=VYJVAqKhTdZyHt8enJbiwA)

  
