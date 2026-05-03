
#Concluded 

---
Html é a linguagem de marcação usada para estruturar páginas web, criando elementos de texto, inserindo imagens, listas, tabelas, ou seja, é responsável pelo conteúdo do site.

**Tags**: Servem para indicar um tipo específico de estrutura na página. São usadas também para que o navegador consiga diferenciar os elementos do site. O que é um parágrafo, um título, subtítulo etc. 

---
### **1. Iniciando**
No vscode, existe um atalho para configurações iniciais, que é o atalho ‘!’.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcxdfXBONlVJwf4esB9VIkOuRa74oHTofhrQ0QoTIcAl9W2ci3q-Yp4Xvg6iV5AoMM1l80mgDJc9RE0YiMsCiDo9P5zTzfWNMio147AvK_bml9roowRYhS5RqB6Oe2bpxapUN_P-Q?key=VYJVAqKhTdZyHt8enJbiwA)

___
### **2. Títulos e atributos de tag**
Títulos em html possuem 6 níveis. `<H1>, ..., <H6>`. Essas tags não se preocupam com a forma dos títulos, mas sim com o sentido. 
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfpuiFlvHtVNxdD3UM6g4YLpOX9tn51wfbiZ8wC5tDtuJJMbDp9KeOHTFLobiVywTXjmTmYHav9JLIksdyqvQqhzp7llZ5Ru_gxX2Q9ZJBaDNo52njKOl9kl87JiLMZOYo96fNk3A?key=VYJVAqKhTdZyHt8enJbiwA)

**Atributos**
Atributos são utilizados para adicionar funcionalidades às tags. 
> [!NOTE]
> Ex: a tag `<a>` é utilizada para nos direcionar a uma nova página ou site. E o endereço é adicionado em um atributo. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9CH49oL40UiGm3UITOoyINBpPr8hJbIu42Xns26FQBOj6K42FrmJKE9obsGjwfYcoKW6ZEZLlFOZYCEDSYaQ_A_oSTcmIMrQC941QTGBYyArV9FhEcubEMpZG24PYAKpHAu3Mdg?key=VYJVAqKhTdZyHt8enJbiwA)

---
### **3. Link**

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
### **4. Imagem**

Obs: normalmente é colocado as imagens em uma pasta img ou assets.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczRCsCFPRr0NbCsIMT9NPpR4C9y6Fa-ou4pfPgPzhwO2iU8oi7mkNGapyyj-OqAUd85sMvGMheFrjOtc3l2SVV6kfCxnsh_H3AHJmw1mP0YRgNaBurP3bbIrCcO6_KUdV8WiHE1w?key=VYJVAqKhTdZyHt8enJbiwA)
**src**: caminho da imagem.
**alt**: texto que descreve a imagem para fins de acessibilidade. 

___
### **5. Favicon e emoji**

Emoji: Para inserir emojis você utiliza &#xCODE; O código do emoji você encontra no [https://emojipedia.org](https://emojipedia.org)
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfjIKoibxtw5TGTAHW2TPgCc7vsN0KnzvDOlmtWNJXi3Z8uXiS0HF7faSqfu_qi6_rLextDFS3PWr3ULYLD_pkYfWD981OoDWJdlFQieBSp4aN92VBkv7sNDUgXdKRpGOfux1a9?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-UCv_AuDCK46ytyBBVWXdQ-I8iope9rNmiXu8LNY2yOTOWWu8t58f3FtL_vm4Uf8FSCkZLBOIiTpymVg8B0a4Yl_YUupZYRxyz4geS0Wbo_JXEpMaqz7d1Fiwx-1SWkPkWD2exA?key=VYJVAqKhTdZyHt8enJbiwA)

___
### **6. Formatação de texto e citações**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfKE3lGHi0HHeMWCOiGQCLLgL7GPH2z5bS616fEIzqpDclZ4MP8rOJ7dSlxf238QOFoE5Yx683uBNkv9ydqdYo6l6DUjZZ35b0d6GbfEwwz-g3Bq2biNSrDeIUxZK6lFHoqGTn-Qw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf87MuJNRFOjO-4XtqJg9mA3qRSRZ5OiWmP4cQOd8ftBp2IByq1jxMO0W3Q4JHsNVYWSh_TfxjOFYb2evZCWfz3BVigZ0ioP0iJGEvD_cbqsUWrO4Q-2ZOXlXusyaxJ0L3o96rJ4g?key=VYJVAqKhTdZyHt8enJbiwA)

- ``<blockquote>``: Usada para citações longas, geralmente de outra fonte. 
- ``<q>``: Usada para citações curtas.
- ``<abbr>``: Usada para abreviações ou siglas, com explicação completa. 
- ``<address>``: Usada para informações de contato, como nome, email, endereço, etc.
- ``<cite>``: Usada para referenciar o título de uma obra (livro, site, filme, música, etc).
- ``<pre>``: Usada para mostrar texto com formatação preservada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXedaI0YsDGd_XCax5WqfXc6jM3lCit9dvcRm5BZVBp7QpMiRqFhb0FdX9eTCXrr1yPD_Z9dDDckbXXOIxgpuyAyOCQqFRM8CZT5YyaglZDpoSJxH0Th8XhBae1u2qtWRZqUExetNQ?key=VYJVAqKhTdZyHt8enJbiwA)

  

