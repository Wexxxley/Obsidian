
#Concluded 

---
### **1. Introdução às CSS**

CSS significa **Folhas de Estilo em Cascata**. As CSS descrevem como os elementos HTML devem ser exibidos na tela. 

Existem 3 formas de aplicar estilos:
1. **Inline**: O estilo é mudado na mesma linha do html.
2. **Internal**: O estilo é alterado na  head com a tag style.
3. **External**(recomendado): Um novo arquivo é criado.
	![](../../attachments/Pasted%20image%2020260503120005.png)

---
### **2. Seletores**

Os seletores CSS são usados para selecionar os elementos html que você deseja estilizar. Podemos dividir os seletores CSS em cinco categorias:  
1. **Seletores simples**: selecionam elementos com base no nome, id ou classe  
2. **Seletores combinadores**: selecionam elementos com base em uma relação entre eles 
3. **Pseudo-classes**: selecionam elementos com base em um determinado estado  
4. **Pseudo-elementos**: selecionam e estilizam uma parte de um elemento  
5. **Seletores de atributo**: selecionam elementos com base em um atributo ou valor.

**1. Seletores simples**
![](../../attachments/Pasted%20image%2020260503120426.png)

**2. Seletores combinadores**
![Pasted image 20250512153555](../../attachments/Pasted%20image%2020250512153555.png)
Todos os p dentro de uma div.
![Pasted image 20250512153702](../../attachments/Pasted%20image%2020250512153702.png)
Todos os p filhos diretos de uma div.
![Pasted image 20250512153719](../../attachments/Pasted%20image%2020250512153719.png)
Seleciona o p que vem imediatamente depois de um h1
![Pasted image 20250512153729](../../attachments/Pasted%20image%2020250512153729.png)
Seleciona todos os p que vem apos um h1.

**Mais exemplos** 
![Pasted image 20250512152603](../../attachments/Pasted%20image%2020250512152603.png)
Aplica o estilo nos paragrafos com a classe center

![Pasted image 20250512153107](../../attachments/Pasted%20image%2020250512153107.png)
Aplica o estilo nos paragrafos com o id center

![Pasted image 20250512152706](../../attachments/Pasted%20image%2020250512152706.png)
Seletor universal

![Pasted image 20250512152754](../../attachments/Pasted%20image%2020250512152754.png)
Seletores agrupados

**Seletores de atributo**
![Pasted image 20250512154609](../../attachments/Pasted%20image%2020250512154609.png)
Seleciona a que tenha o atributo target

![Pasted image 20250512154753](../../attachments/Pasted%20image%2020250512154753.png)
Seleciona a com o valor blank no target

---
## **2.1 Pseudo-classes**

 Uma pseudo-classe especifica algum estado especial de um elemento.

- :**hover**: faz com que quando o mouse é passado por cima novos elementos surjam.
- :**visited**: se o link já foi visitado um novo estilo pode ser adicionado.
- :**active**: se algo for ativado (link, botão) um novo estilo é adicionado.
- :**focus** é usado para estilizar um elemento quando ele está em foco, ou seja, quando está selecionado ou ativo para interação. Comumente aplicado a elementos, como campos de formulário, botões e links.
- obs: **“transition duration: 1s;”** define o tempo para fazer a alteração.  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6G4y0VSZUSbxDEjMJP_CqYJJwX5l9V-FqG-GsO9eozMfxmj5avcblJ0e-y3aO0xMj_gsQbrJLEaB7ZawwEIpTuj5OCuUFjTRby1k2G1wIDL8bEYid5jN6NiRS4b-RAfg8uqIehw?key=VYJVAqKhTdZyHt8enJbiwA)

---
## **2.2 Pseudo elemento**

Os pseudo-elementos permitem estilizar pedaços específico de um elemento.

**First-letter** modifica a primeira letra.

![Pasted image 20250512160202](../../attachments/Pasted%20image%2020250512160202.png)

![Pasted image 20250512160218](../../attachments/Pasted%20image%2020250512160218.png)

**marker** modifica o marcador de listas.

![Pasted image 20250512160457](../../attachments/Pasted%20image%2020250512160457.png)  

![Pasted image 20250512160509](../../attachments/Pasted%20image%2020250512160509.png)

**selection** modifica quando você seleciona o conteúdo com o mouse

![Pasted image 20250512160626](../../attachments/Pasted%20image%2020250512160626.png)

Existem tambem: o before, after, first-line
  
  
  
  
  
  
  

___________________________________________________________________________

### 3.2 Cores

Existem várias formas de representar cores no css:

1. Nome: forma limitada.

2. Rgb: as cores serão formadas por red,green and blue em uma escala de 0-255.

Existe também o rgba que terá um outro número de 0-1 que indica a transparência.

3. Hexadecimal: o valor rgb será convertido em hexadecimal (maneira mais usada).

4. hsl: matiz luminosidade e saturação

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvhhLRL93j2KYnvR5s0DVmIhhqakGUFSzIbmJMSR-03iI81anmrFbOms7nmj7F2ZseTu1ctvILoqbbmrTDY3vI5ZXFOj2iWLA89CluMb1ORW8Lyy1jAu0P-q0PvhuNB5vOX7f5Kn4ID1zvgP5OBd0oeIuD?key=VYJVAqKhTdZyHt8enJbiwA)

___________________________________________________________________________

#### 3.2.1 Círculo cromático

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe_clegEc-inj3WbcsKRoEMM22VUKr0gpUVem4MjNgrdufZqX9jh0HD3Mb6yTUJslVhwIkS93mg2djwE8pJz76fNL9icj_Tsbhs0ZXln8F02jioRSvU-qojjAlXHAUUSckhXSsNCkEaSZk5k9LENO8gLIrw?key=VYJVAqKhTdZyHt8enJbiwA)

Cores primárias: Azul, amarelo e vermelho

Cores secundárias: Junção entre cores primárias. Laranja, verde e violeta

Cores terciárias: Vindas da junção entre cor primária e secundária.

  

1. TEMPERATURA

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0XahoPdBjwEspX8dE-H907sfo0KV58r6o7Cp_HTTN9zK3XYLTTA3VXuGVVSTPqx1YeLyqrCxnqFNq74gAaWA-Zl3hSzyVw6qqpKF0CqZAu_D3RJlZzVWm_Kd9sKd4E450SYM7og2RrasOJSxBjQCoG_8?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdTt0pIklntC5ZuAY-R5jTpbKNgqWpInThBJy6-4yEZDZl7I_UaFrHdcJkGkZ1DdCiUFRW8ev5PNfz3PGeTABRN1vSKtSUq9LlWFjzHvLQ_C6lmBpK2I6Wf-YfAqwupUydMLI2AlGmqxbDn-MNp0QtNIgM0?key=VYJVAqKhTdZyHt8enJbiwA)  

  

2. CORES COMPLEMENTARES

 São cores que apresentam o maior contraste entre si. Elas estão localizadas nos lados opostos do círculo cromático.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeiUefZC_VFTXNmLYE0acqiipFRHTHcEOy16Va8ON3OIv3gQ3vazq6ZEG5_dFEGTPOAH1_3tVXO3skxwQcfmmUdEYj_Nf-apgbZxlFmvf1PE23ZyXBt4nT1Hf4DPVEaPLF07cpRRT7fadi1EiVh4wv6b5HF?key=VYJVAqKhTdZyHt8enJbiwA)  

  

3. CORES ANÁLOGAS

 Cores análogas possuem baixo contraste, criando uma harmonia entre elas. São as cores vizinhas do círculo cromático.

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdk47cZpAsb-otM2viIXcNd15eyPWTxzT4uK7CpawEBG_A8B2cC9UfFfBPsLLBKWeowDfW6GBHFuCVT1agS1tt8YOk4CeaFW_uMoSimkKKlX-MWNO0_9t16g0lJB6aUilzbIAWyVOssgfMy1jRlUGEbkKA?key=VYJVAqKhTdZyHt8enJbiwA)  

4. CORES ANÁLOGAS RELACIONAIS

 Nessa, mantemos a harmonia, mas com um pouco mais de contraste

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc_B2Ub1uQ5ILodQeWdmREnLHcYUf4YmuZOq9J9EYynNJXlSxllChystnaeJanIpcCj5Eddkta5e7ha7ZyoBK7FFc3nCYTa8D5lmTvf2E84ufbRA0rxtnVURlyc_OdkMt9DvX7c4osbBJIDkWgeu9He3yPa?key=VYJVAqKhTdZyHt8enJbiwA)  

  

5. CORES ANÁLOGAS E UMA COMPLEMENTAR

  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcliS83dRPSNSnwmXcXNUJkokxyMgGQOPnZ1fykFjiB9QsFHndviM9o70Q4C1SsvNP2pZdmkXE4PQv4TVALR6827IBfqLISK1meBwXf7Kuas61xuIhAyikW59GfVU8D4M1SaJwhpKgdzGOSw35uDRxLCZ6t?key=VYJVAqKhTdZyHt8enJbiwA)  

6. CORES INTERCALADAS

  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcsn4wsxa3zTwpGnGch-gcPH0bqMY1duI_m96p9a-8D-uzstrMPQjRPa8BDwBQ6cV0fP3-D2GOIyXuBdzvkVf0hqo5VlonFMQgAfwwhfrM1iZ6I-jC9oEfxMZjoJLbs0OIeQu7GlVCgvneGSnt1SQUpE0aM?key=VYJVAqKhTdZyHt8enJbiwA)  

7. CORES TRIÁDICAS

Gera um triângulo equilátero e garante riqueza de cores.

  
  
  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDqmU-7gX23jRdTd4io7WPJIaV0PT8-BCX4fISeM1RBcqTDk3NLm2Esnyts-W2LO9_vRmnkDOF88O-px_DD-vmTaVZmEqidqAPHI4_NRrWi_JSO2yr2LGLAXQP42X3QvEVguKIz1bFgqy-0VyXm_0UZ3jv?key=VYJVAqKhTdZyHt8enJbiwA)

8. MONOCROMÁTICA

 Uma só cor é utilizada. O que muda é a saturação e o brilho. Essa combinação gera pouco contraste, mas gera degradê.

  

___________________________________________________________________________

#### 3.2.2 Paleta de cores

Normalmente uma paleta possui de 3 a 5 cores (desconsiderando preto e branco).

  

Adobe color: [Adobe Color](https://color.adobe.com)

Com essa ferramenta é possível criar paletas, extrair paleta de imagens, extrair gradiente de imagens, explorar paleta entre outras coisas.

Coolors: [Coolors](https://coolors.co)

É possível criar paletas e ver tendências

Paletton: [Paletton](https://paletton.com/)

Com essa ferramenta você pode criar paletas e ele te mostra como ficaria um site com a paleta escolhida.

#### 3.2.3 Criando gradiente em css

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdm5eMQecnZkkDcHp6uMMx3v9qnXZFMyv9smuzjmupyepL_zDsJ7iCxGs8TG4hqlJZq_Gn92YEkR2yCz-mm7mNuVEV1DPWQClLIKET-_grKRa4C_LYek87T2BPq1oD4RerUWnHlHCCkwvm5-yEcg2CUD0aN?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdR-Z1nmBv3ET_UHTEbweOGbbI1IzvJnVXkfJqm_RODBAP7bYB4cy4XDNptCdi-J0-sOR_DMpsg_JaZbL7O4k4szKtNd3WtavLZhYaSjE2tgUEDdNFLB2BEzVZalJi_ZkAplwBxLcIEjNQu0UDzAL-KEyY?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  
  
  

___________________________________________________________________________

#### 3.2.4 Background color and image

 Você coloca uma cor de fundo com a propriedade background-color. Se quiser opacidade usa-se opacity.

 A propriedade opacity altera a transparência de todo o elemento no qual ele está, incluindo textos. Se você quiser alterar a opacidade somente de uma cor, é necessário usar o RGBA.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc_Cv-wtHMCdGarI6lrBca8XvejfTyERrJa-Q0Flqgml2TdDcDilbRAddmZkc0jrHY2lY49cfAKtgEnineVhA5OzrGuiZMTrwVpk1i7SZTKxmUxEX6s6zyzroo10zIjUbRpSY-oeQ?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJlMWEm8iG6wpJ4351rxZWRQvQDwRkkxOStSsXHJiCB_a6gUuSYof-llkUScoRwsEMgM81D6kCgfhEGVLSR7eNDi-vFhjU7xco4kygBf-OTa_fDTis7VCR97J-QGTx-OqjSXkXZA?key=VYJVAqKhTdZyHt8enJbiwA)

  

 Com a prop background-image é possível colocar uma imagem de fundo.

Como estamos dentro de pasta CSS, utilizamos “..” para voltar e “/” para acessar a pasta de imagens.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXehmXH7DS9cQcN0SIix2OOsLLy9hGxP9d80LgzC5QjGUhjOaN2Crz75SPbXXl-oxoDdghURlPiB5pOakb1ziea2QCsBSIlvBZ3M_Rd0t5xByZnAZHmJYGK1LQhIabpgHHq-vEU3TQ?key=VYJVAqKhTdZyHt8enJbiwA)

  

Ponto de referência: É possível mudar o ponto de referência da imagem no fundo  com a propriedade “background-position: coluna(left, center, right) linha(top, center, bottom)”.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9UKX_oksGewm2S33uiAEgRoftO-RwXPj9XHPen_arYP0YC3CeqwoKztaXtOHXmv55AM2FY7MoKLhwUEw-dac_blH3BTrZeczsgZLVm9MmFJ8I1e54JofIzmsPfquttbp_rhcepjXfCLr4gpXRpqOvKrdG?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVY0EYvLSB7l1F4cqFiOlRR0-2VPzWANsQzHrf5WluufLisU-gzWL2GBN0VvGTSpV6obsm4MIWONkWZJvecpwpVMRTH0oDdAfndS50LPpgRjVJIkPlHOgdYD0GxXBJwirrKzfMxb40ui4LDWIP-8ZLzXs?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  
  

Sem centralizar.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6leh_wZT0UdpLYNXj5Ny54VjgmmUu5F2_vTUCQaC4SrRn7aCetfKVd0ejBSTIiIak7dv9sHeAPzFrIVVUr-AZ1TP-X0G5XkwZod1i9RP0Lwb6hyqcEiPIZIPeHZc4s9r1ishj?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc8Dmqd0e3GdMKcbUuegdJorSSDDhh0H7lKcetlj0QqQ4aqsi0Ji0nLwaD_WccNqeBEeZoaOz9ILcN3MLuyeNddiAZsTt3MX76RsB7gYliL-wKlxq0IlxlM7cscLlPs1IJBg7fJ9g?key=VYJVAqKhTdZyHt8enJbiwA)

Com centralização, background-position: center;

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdp9eKbAR-GhCgbVmzeMXZ6Nhv_suwzzqwpgbnKrpSye7umVYL5syXQ9DVt0Thw4w3HwkgvSqg62TF-hGx-iMvdlCdedrsWPnTja9C4OzyA4ElcyjW0FDvpy2t9CEcZFRwvBhpS4g?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf8Pv5bTANYcifwBXmRGbDVhph718C8cSCyUuh0RIWUeAcUCupzA3gaUL1xJI-t6w74aMttFBCHzYVjjnoTuo7fj8i9WjCJLlRUNxvgObQcyFergTR5EfB7Qlz08wNosjkRquiv8w?key=VYJVAqKhTdZyHt8enJbiwA)

Background-size: cover redimensiona a imagem para cobrir todo o elemento mantendo proporção.

-auto: tamanho original(padrão)

-width e height: você escolhe os pixels ocupados ou a porcentagem 

-cover: a imagem fica sendo totalmente exibida e sem faixas, mas cortes são feitos.

-contain: a imagem fica totalmente exibida mas com faixas horizontais ou laterais.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdtI8FZ881oKsWJsl7s7V4YHHIS6JN1dlpeVZ4eIm32adSPLCSF1qbpOKXKujQKc0KBN7xi1XBqr5QbBWB2OwR8bxFc7xueMPwE2bKU-h072-sl5zk-Wf0s2-YSi9gEnJrF81YJuw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfpcPLT0OuzTTVCBcOHtNk4PiMgz5jxANDfuYOtf8N2EaWkzYp2dcg64Rt01elkSfpkPeVLp4YF7uXzlaQPI99IWHl1ou3YwJHYC581d9pToGGpbHqePp_7HLxvbNEbGaJm84Q0Ug?key=VYJVAqKhTdZyHt8enJbiwA)

Attachment: Background-attachment aceita os valores:

-scroll: a imagem rola junto com o conteúdo(padrão).

-fixed: a imagem fica fixa.

___________________________________________________________________________

### 3.3 Tipografia

Normalmente um site tem cerca de 3-4 fontes e é preciso escolhê-las muito bem.

#### 3.3.1 Tipos de fontes

1. Fonte serifada: As serifas têm a capacidade de guiar nossos olhos graças aos pequenos prolongamentos que elas criam e fazem as letras “se juntarem” em palavras. É recomendada para textos impressos e textos web longos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcoACe3LlU9MrHj5BKxFAMyau58W0XL4WoCG7qZjbhEifjpbTEu0wE5hsuN5OKJ_KlP3jty2rg7cVDRDBgkzxrUw1zldht-EKC9P9h6dlcMD5rNdMHn151NjrOVPuW2DCLXpVTHpg?key=VYJVAqKhTdZyHt8enJbiwA)

2. Fonte não serifada: São ótimas para a exibição em telas/monitores pois transmitem a sensação de limpeza, clareza e organização.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcSCjLXrfrvkno8g-ENO84KAunbdjdznore9NnFlPORIRbLsSn8MB4K3hCKywvIvJl4SJNaobDmIm3twZw1ZjKIwJwz3vSSl_eFmzEEIdEBtZtV6CLfQ5ACLNC3rkceh9r12PoAog?key=VYJVAqKhTdZyHt8enJbiwA)

3. Fonte monoespaçada: O espaço horizontal ocupado por cada letra é a mesma. Usamos muito esse tipo de fonte para representar comandos de linguagens de programação de computadores.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfbXPhSWlezG4WJTFroHkshM5MN8y4NNdcy0n5OxIBQ-fuEcT6WXdriGPpoFodXWXvO_xSayKVyeub8a2Ja-v0GiMpfEA9BmfFshIopmMnovHfPAF6yLqDAiY223ya0j7dm8-fy?key=VYJVAqKhTdZyHt8enJbiwA)

4. Fonte script: são aquelas que tentam imitar a escrita humana. Seu uso deve ser bem controlado e jamais será aplicado a textos muito longos, pois causam cansaço visual e tornam-se difíceis de ler.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewR7Kmjn50SEU5SVmAvAOv7tOhthwOVIb9Gms1NcXH63_bd13jCf7JFfTEeGxP2a1HxR6UqJM0N1Io-Tzy1mKAKvu_J9Hb8F1wPmTiOuQSFaHoO3PpQ3P3VU_beWney5EdkTXhyA?key=VYJVAqKhTdZyHt8enJbiwA)

4. Fontes display: São fontes com bastante efeitos visuais, enfeitadas. Também são chamadas de fontes comemorativas e algumas delas sequer representam letras, podendo ser desenhos de animais, objetos, pessoas, etc. Essas fontes também são recomendadas para criar títulos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc2ptd67hf_ZG_oZue9_aD7583Y-jO1YeQy0osZWuA1Nu6X7pYTIx1uDQ0Qw0qYoNEpPBINKixpPxjmB2ba1WV8kwwxyStRzi-qX4A5fVc2J4BuqxW7q4d2H0QsOvaNkaW5mJiwXg?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  
  
  

Qual fonte escolher para seu site? 

 É necessário ter em mente que computadores, celulares, tablets, e até TV´s vão utilizar o seu site e nem todos os dispositivos irão ter a fonte que você escolheu.

 Por isso, existem combinações de fontes web seguras. Digamos que temos, arial, times, verdana. O navegador vai tentar encontrar a fonte por ordem de prioridade

 Você também pode colocar somente o tipo de fonte que você quer e o navegador escolhe. Pode ser: Cursive, fantasy, monospace, sans-serif e serif.

#### 3.3.2 Modificando as fontes

1. Tamanho de fonte: Recomenda-se usar duas medidas para as fontes, o px(pixel) e em(relativo ao tamanho natural da fonte) Dessas duas, a mais recomendada é o em.

-16px = tamanho padrão

-1em = tamanho padrão

2. Peso e estilo da fonte: Com “fonte-weight:” você pode alterar o peso da fonte(se ela tiver). Fontes simples como arial, verdana e times não possuem peso.

=>Com “fonte-style:” você altera o estilo como, por exemplo, itálico.

  

3. Simplificando configuração de fonte 

=>Sequencia: font-style -> font-weight -> font-size -> font-family;

Não precisa ter todas as propriedades, mas a sequência deve ser seguida;

Simplificando: font: italic lighter 30px Georgia

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrJ1EnDXjtXL0iBGCoDoBrbzJzjnAjoYj-5iX1OfW2fITdICpyPoZfq1xhlM2PLrNXoJ3Z8c-l0esJqwYAZPlfJ5LxnMhjdAgryeKwEMCjN-_4klJlfalKZFUFycbMIXa44iOdJA?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeuZcEAthoeKs-sU3wxdzpE6U2cuhJscn4hGsStc_ZWfPOpDns2RX1YmNzOIuyxd-p2iffu_T9Kqo2Sj_EWw5ei7oQ6WYSxI5f9uUNxVZ32TZO1aDtCRHw-vbsQlIhmlTyFkGv40g?key=VYJVAqKhTdZyHt8enJbiwA)___________________________________________________________________________

#### 3.3.2 Importando fontes

 Quando um usuário entrar no seu site com fontes importadas o navegador vai importar a fonte do local de origem. Para importar, basta ir em dos sites a seguir, escolher a fonte e copiar o código de importação. Lembrando que @import é uma regra e deve estar nas primeiras linhas do css.

  

Google fonts: [Browse Fonts - Google Fonts](https://fonts.google.com/)

CDN fonts: [CDNFonts: Free Desktop & WebFonts [BETA]](https://www.cdnfonts.com/)

DaFont: [DaFont - Baixar fontes](https://www.dafont.com/pt/)

  
  

Baixando fontes: Quando você baixa uma fonte, tem dois formatos comuns, o opentype(otf) e o truetype(ttf). Existem navegadores que funcionam melhor com otf e outros com ttf então é recomendado colocar os dois tipos.

Para incluir a fonte baixada é utilizado a regra @font-face

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXepacokA9ro7skjjlUJoXIpQw-gPeSW1IB5iw5siMKt14nj6lltIAY1zLzCJxUGmjxjb4Y2I-cHObsX2_d1Z7EARQDyTsHEe7uc1zPVrmXtmvWK2NdQVdTAu7Qre4CqvjpyPeI1N0m9WJHBrbirtginB_Nm?key=VYJVAqKhTdZyHt8enJbiwA)

  

Encontrar fontes de sites: Extensão Font Ninja

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdav_IgttV8It3RgKYL34vyrUDdCUNQw1_BkF3b1ywEWlEG_K6B_X-35wVFa3xoJ7tU7pIQyyFbU_LRwaUbg8MQIk2nLdmHgpkyHgcKCzhmc7P83wLwqYovCcSEKa9gYKRuJRvCrQ?key=VYJVAqKhTdZyHt8enJbiwA)

  

Encontrar fontes de fotos: Font Finder: [Font Finder 🔎 by What Font Is](https://www.whatfontis.com/)

___________________________________________________________________________

#### 3.3.4 Configurando texto

1. Alinhamento: Para alinhar é utilizado text-align com center, right ou left.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOALL4ui9dBcfCOHfHhagcY9W-EzaS31ZsGc3Nr5bKOOwfaFs1WcqBnjTzAFLJc1aF9RwdO-nCq7T6snGKBn1dPPZhdmBk744MwpELGWkiEXroBRHap30gHYpwcD8MaT7adaEqeQ?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcgdb41KbSeSVJ3UXZ-dHx3NlsOQbmvHTtnXmLHPs9zQwTdzW5S0b9J6HqQkm8AAsemJGDjhtsRO6UAkPwhxdOR4elXhLjeuSog3GBIalhRI0rYS60v51phBWvUIg1f9bQTaS2g4Q?key=VYJVAqKhTdZyHt8enJbiwA)

=>justify

=>right

=>left

2. Text-decoration: é possível adicionar decorações ao texto.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe4X25S2njXF289-E9BURb9ptVp_giQB_wib3Sink994pE1_YbCF22bvNf0nQ702pjObQgwTw5_4H13YtiM9yYuXqp6bwdAuB1W0PNGhwV2GSv4H7ObyTuABBSYTiNXOGuVDwHTYQ?key=VYJVAqKhTdZyHt8enJbiwA)

=>Com “text-decoration: underline” é possível sublinhar textos.

=>Com “text-decoration: line-through” é possível riscar a linha.

    
  

3. Letter spacing: é possível alterar o espaçamento entre letras.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXequ79pCsvlzjFm_rRV_tS5ghul58DMHaQD2HM89FXl3YmycFgU04UFjnfc9rtLKfZ9g0pzLmTbgcCfDlJnP-o4t0sL9CS8mA_xFdliqkt1DXYbkj6Kx1-dXWui7WOHHfeLW979?key=VYJVAqKhTdZyHt8enJbiwA)

4. Espaçamento entre linhas

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdazhHt_4isfo_Sp5fTtdwDYmn_bO3PqhNMT_WYD14k_NWmT525t7oV2VLoOzm3Dmrz9QiS8yW0jQGYe4EvzctcyD91JedI2MeKX_iqAaDq2KppVbmro88-917cZJPV5uzXeGYr?key=VYJVAqKhTdZyHt8enJbiwA)

5. Text transform: Recomenda-se não colocar textos em maiúsculos no html. isso é deixado para o css.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdroxP0Ua5Vej1VNi6TK_lXl5Rh_q0a4fX2Cu1KXRPT1QSILe3q9upTxTe2FnxiEZCW9Wo-1MBVcU9U-IQlBqE-iNJrJc_3bj0rHyLrzS6YIT7px2bh0E6rCqThwN4yN3RuMWV5HA?key=VYJVAqKhTdZyHt8enJbiwA)

6. Indentação:Com”text-identi” é possível identar o começo dos textos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXftRYE6GUltjUA3r5813zCXksxhAjEUnKeX92Z-3YSPMm-7g06sV_0y-_VRteZ-Yn0bsYjUiBprt0Ba6-qSrbyOFf3FzUf-2UXKDmC8T_MH8hOO9JxnZ5aL0w6hxgeEH08i1fpb?key=VYJVAqKhTdZyHt8enJbiwA)


___________________________________________________________________________

## Responsividade

 Um site responsivo é capaz de adaptar o tamanho dos seus componentes para manter um site visível para diferentes formas e tamanhos de telas.

  

Main

 Você deve criar um tamanho máximo e um mínimo para a leitura do seu conteúdo. Isso é feito com “max-width: ” e “min-width: ”

Image

-Você pode colocar a imagem com 100% de largura com “width: 100%” assim ela se adapta a sua caixa responsiva.

-Você pode usar duas/três versões de uma imagem. Uma para telas maiores e outra para menores. 

Video

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfB75moWQ8VYejHVFDewtOsl1ACHYVqeJyuuVROlXtUE07RtxymSkwuoFUAa3mrDhU3nY63okKNzvBpNP-U46slZDOcLuNgwOP5W_t0rSsnsgblLzf0WTSsXQXuTWIH7LG1rz9SnVA-HOvn_QWm3dql1NaK?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  
  
  
  
  
  
  
  
  
  
  
  

## Centralizando elementos

Centralizado horizontalmente e verticalmente: Esse método funciona para centralizar somente na vertical ou horizontal também.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXCxNdnL-lu-7y9luu6LxzrsNAG-bD2t2eElWFzkuMELisTbQkd38oqPZ_UDPUWkAUOEEkQdeWB5YKUpdrdYQV4fFLu-dRv7rNNCLD2Gv4-3FUwmso0N6I0II-mdhIQ7TsU8-Q?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcd4nHiDgYRzKNf8RxYd61jmpTTWfek_QEhkaw8AlXZV1_V8H2ooo3UQdjHlhuWgICP2hu4aA5Kj2msRJevCyEFbjuX5fm95uHYvKUyPMy0I2Utk9S_LRen7VNFXc8qDkR6gzSOJw?key=VYJVAqKhTdZyHt8enJbiwA)

 O pai tem que ser relative, do contrário, o elemento vai ficar absoluto em relação a toda a tela.

  

Centralizando horizontalmente

Basta definir as margens laterais como automáticas e o elemento precisa ser do tipo block-level.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfx--wC2Vb4WQKwA2p2qku8ZDfn6EDJkFwTypr_bz7tcyB5Cc6zkt697xm-hcAA_coiBnZzmHrnBc7EFFMjnE4LWhSbnekSoK0fd1Oip-RKJpNLdoZkWUnJbYA-6EaDs9wKmpXW?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdaYeqeCgu2Y1DOGFM6M_jWD0N-lrUflhmuXfZhGzqvsv4UIRS1ayV-K1mmSqGElfkXqNxUicf0xS_65wlCFgYXc-0GjqGGy-O25-hyrXp0v_K9vz_MXX4_M9DISxyMmZHjQZgbpw?key=VYJVAqKhTdZyHt8enJbiwA)

  

Centralizando com display flex

 O display flex é uma propriedade CSS que define um container flexível. Ele permite que os elementos dentro desse container sejam distribuídos de forma eficiente, independente do seu tamanho, com a possibilidade de alinhar, justificar e distribuir o espaço entre os itens de maneira mais controlada e responsiva.

  

1. flex-direction: Define a direção principal do layout (se os itens serão organizados em linha ou coluna).
    

- row (padrão): Alinha os itens na horizontal (linha).
    
- column: Alinha os itens na vertical (coluna).
    

3. justify-content: Alinha os itens no eixo principal (horizontal).
    

- flex-start: Alinha os itens ao início.
    
- flex-end: Alinha os itens ao final.
    
- center: Centraliza os itens.
    
- space-between: Distribui os itens com o maior espaço possível
    

5. align-items: Alinha os itens no eixo vertical.
    

- flex-start: Alinha os itens no topo.
    
- flex-end: Alinha os itens na parte inferior.
    
- center: Alinha os itens no centro.
    
- baseline: Alinha os itens pela linha de base do texto.

    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdiaJChqtOZHEh0xDWpLSFJYC6V-sZY-yeYEGN2gIXlkj8wjQ3Ae_eF4tA50P-I6eS2LqZUBKl1Q4wMoMfb_-gYbB9j0WdWn14N_NYOvOTyfYIewDa67ESu63XeyM_Qw8DDJy5B?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcd4nHiDgYRzKNf8RxYd61jmpTTWfek_QEhkaw8AlXZV1_V8H2ooo3UQdjHlhuWgICP2hu4aA5Kj2msRJevCyEFbjuX5fm95uHYvKUyPMy0I2Utk9S_LRen7VNFXc8qDkR6gzSOJw?key=VYJVAqKhTdZyHt8enJbiwA)

  

<CONFIGURAÇÕES GLOBAIS

 Serve para editar todos os elementos do arquivo de uma só vez. É muito útil, por exemplo, para retirar configurações padrões dos elementos, o que acaba atrapalhando a edição.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdAORZpj0_HMq-Hgko4zsNDkDC2urc5kPfRQ36D7x0OM3JucgHXVnAXFV8iSbryWJMtGtjLWldvQupsoLfuRX8b00_Wt_G8Er-ah4SxyEqwQhCn8jv454B58GdliulM2uFqHiJJng?key=VYJVAqKhTdZyHt8enJbiwA)

  
  
  
  
  

<VARIÁVEIS

 As variáveis recebem valores como, cores, fontes, etc. São muito úteis para editar seu estilo futuramente. 

obs: É preciso que estejam dentro da pseudo-classe :root{ }

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcF2vzNrIrOtVjtA21Pyj91eSSfU3XfSGmI3W6w7kf1O5XBn3veFLt3cpY80zZkqwjEQXzqjGY1OSwnTNpv76k1sXOIld1Nd85pGxs2D1NXS007GnhWE6nYa_rTGc8W_G28XZij1izpClNY-jMEU4zDTWuj?key=VYJVAqKhTdZyHt8enJbiwA)

<PASSO A PASSO PARA UM BOM PROJETO

1° Escolha uma paleta de cores condizente com a marca/intenção/nicho…

2° Escolha algumas fontes condizentes com a intenção

3° Crie um Wireframe (protótipo da página de um site, uma espécie de rascunho)

4° Crie variáveis para cores e fontes

5° Crie configurações globais para retirar margin e padding iniciais

  

[https://www.siteinspire.com](https://www.siteinspire.com)

https://onepagelove.com/topology

**