

---
## **1. Formulários**

 O elemento form é usado para criar formulários interativos onde os usuários podem inserir e enviar informações para um servidor.

Um formulário básico contém campos de entrada input, etiquetas label, botões button e outros elementos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfM-CzBbmBMx-NoFAHHzLRG0_ko3ywR48HqBrG8qUfueoLvjAPsR3iTvjR2U3BTM7jMqhzN_VOC5vgKQLusrjL1ETtL9udQ1_icAj5Ftk0GD6guzDxNQPRRFbfh-wbhrVttb-XpAQ?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeJ0C7wlvNOM-J5Xk7rOTCTbj47Yc-UnoH9eE7DSzCdHpAtC5sgWtN2bR5MsUZwc5nVDXPOHwMhMpZX39adNNDB9Sxmmj-CfRfm2tWt9TJk639ZQNaxwJdmPxYyhdUuUDrYIFBQdA?key=VYJVAqKhTdZyHt8enJbiwA)

Explicação dos Atributos do form

- **action**: Define para onde os dados serão enviados.
- **method**: Define o método HTTP usado para enviar os dados.
- **GET**: Anexa os dados na URL
- **POST**: Envia os dados de forma mais segura no corpo da requisição.
- **Name**: atributo utilizado no input para pegar o valor no servidor.
- **for**: usado na label para questões semânticas

---
### **1.1 Principais Elementos de um Formulário**

a) input: O input pode ter diferentes tipos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcwy6kj47fZkKQWJxIvWXgi_gtdpzOyma-lckTVAk9cJW_7LVQpogE_dtgabsL1DXQIqP9CYiqbXjbG0l_Aah2R5lPxO7tpG3XY2h7MUKJt4vG09r39A9dZZXDKaV0LTMisxpXCXg?key=VYJVAqKhTdZyHt8enJbiwA)

b) Seleção de Opções (select e option): O select cria uma lista de opções.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdL0h7ZvaDav33gkyc0AjiCI3-kCS6i_SXgTcpj9obCvc4CbhEe197JiLMGJZN6x1uDqe1X7U0FWW83kKm2gnqyi9vRJRn4uF64cj8Y3uf7twdKFI34jMUtWI2Tf6LyvRB85nSJ?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfuaU9lwFIlHF7qxtYsjeGArqgWn1G1SWJJF2RdgagiNCX8ooTFB_MP5uyCeWbwkWYaW4YgtcB27xZKJGiAun2dp3499Zhv6F8A0hIk4f3m__SHVGcQ33fVCbGnLjymTsnoA42Eow?key=VYJVAqKhTdZyHt8enJbiwA)

O selected deixa uma opção marcada caso o usuário não selecione nada.

É possível também selecionar mais de uma opção com multiple.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfMUntZSPx0YXQjzUnPBL5agFLxrirElQZdtonq3Tvltv6ai6CasOFhSGfsls_eElzwT7k6bUn06xaxtuhT8ly0tJ67V8dokTYH_0RV2bmayQptFDLYSZuDCaE1-jJzRck-zwJB?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcKfA8gRap4UP85RW485ly-j5T5H9E8Z5Ily4867_S_SZURnyX5VfuUpvH3DSmOpi1vh3KESCmJ-jSYxM4gP8jOoAZDUluvF1A8lppBShG45rUj6pfSpAR1jzXRlqCufFNQ4lxJsQ?key=VYJVAqKhTdZyHt8enJbiwA)

c) Área de Texto (textarea): permite inserir textos longos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdbF3PWiVtHqJtTkUbOaVqbAL-V1aspsRQbe4he-LAXLmcNR6R9IfCtZ3AocQ22uX40LOCIs3Qq3mKqLn2sDa_I-fg2OT5AibYhVdOp9dSWci6XMedfcsIp1VLUtFz79921QyPHbQ?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf2jylvXvp7oEADH0G5vh-djs0pTUfaNrB9MtnjB4A5XPGRntshnJ7be9IWkynPtc6dD-4ZeC-SXyUJvR0NUpahhcrRuqDxOA6mVmgzjNYbuLsNQ04NOFA7bZPN7yCM1ASI6mxiQA?key=VYJVAqKhTdZyHt8enJbiwA)

  

d) Datalist: O datalist fornece uma lista de sugestões pré-definidas para um campo de entrada. Ele não restringe a entrada do usuário, apenas sugere opções para facilitar a digitação.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcZ9KU2WSdo2QKnpeIHouXDxUFEHNltr3kdaqDg2_VSr-fylg-_IJxocSBZ6gx5QlsSBaSJYZPQVOu8P3qMT22M4LPFyHCrl4DL9jzrfwb2ktCM_wRKo0DaoVKdmM_MuGDU3AvSBQ?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPpG89s07k-XzMmcuXklwvxtokt1CENLsHCXrSYLLCsE4Vw_Viid2FEOYih5gpc-BV9MUHsngkbzWsSTVqinaholf674h6XoceJKrv28BOo_pxYgoNN876x9VIYNfAMkq9adKIqw?key=VYJVAqKhTdZyHt8enJbiwA)

e) radio: usado em formulários quando queremos que o usuário escolha apenas uma opção dentro de um conjunto.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctdF2yka2khddtaZRFxd4PrRiBUGKPUmoamCJQfbet3_Q4Y2PtZwkwyJWukZpgyyy1J_XuYPACJUCnTAjNmFy1ZMqRyNhN60UuYRK3mLv4lpxJ2Ti0tNUch5KzPvhP5uqgTKtyfw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcrLLmH0zRB-9FTdQa7Okek5EzzMLljoTn0fj_9vdo_PZJ4KH071oBwsub0x4_xNqhj7Zd82leIFSL8O4XXVZ9Ow1oT_zs4pGzDfT4oA4dyg-ea8cjkuY9c4aic1Kygx12XlNDN?key=VYJVAqKhTdZyHt8enJbiwA)

f) checkbox: usado em formulários quando queremos que o usuário escolha mais de uma opção dentro de um conjunto.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc3U5UsZ7-8RfJJcyopS1SWaBpHQ-5RW6-zngxRZ3ntfwVl51oxtIqvjnf8lgneCBGduqbYvRRPZr6nzYUjNsEObh_euv1j0UUwwB3ubEwUGZmN5gV7sR27PqvXniR1sI9RJMUFuw?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZYiYPuC12N96z19F0BqwunZMGMizUOHXOcjrCAN4qYqTuEGCDvH-Yf9MrSmWnAPHEXeyDEczMhwU4DQ6hL9oLMYmHQgANIwVvlgWLho3y9PYY_IM-whDoQsS2y02H6PHqBQJ0lg?key=VYJVAqKhTdZyHt8enJbiwA)

g) input de date

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfP_7UpoLhYeSCvi4ATS_IAlLCBReY7iI0tTHDmgUGR7PRn52OynYfDCwk3CGSLCbxknrzmjxZ4GvC3NLMinIGEUU2uime3qVQCM9xiXKPMRxN2HdiI1CFM8iv4Zicizjt0gDu9_g?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXekiTlzSDyvaQab4cr5Qd3Iwmd7flLKFHwNHzFLcuJJ-Umkn0yhuBpwYsvVT-VZYB0DCnEUr1WoT77fX6xMUEp88QNg3I9w_eEUwUOJvpWuAujRHLKRqMw_tIPGmF0Y4snnlb5KfA?key=VYJVAqKhTdZyHt8enJbiwA)

g) input de arquivo

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd45mgYvC1VXmLrsoVUBw8nrjYEyg4_r0v4M4PQuIJVKXtVoXAs4-VGXzmuWirgigNwQm27KDwv5JDoiwKgzCcZ7dAPWm6ERC0Rb9VuTTYiOZcLlJGq0LhzKEYg97ZYkXEnCAUPkA?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdWFASmQuIvmush_qBAkEzWNlRjPtGX4BEF3orBlIFxIj5RR3hR3RY7SOxabSg6DfbkOe_kpHnuwetDf1_vEde377fLrbr-uKQnOIErU0exsDNKKmWtB1CEYqSNMK5U1EFnMRpjbA?key=VYJVAqKhTdZyHt8enJbiwA)

H)Placeholder: O atributo placeholder é usado dentro de elementos <input> e textarea para exibir um texto de dica antes do usuário digitar algo. Esse texto desaparece quando o campo recebe um valor.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdGxxqOHPuVOqXurosAecGe3vSPYauMpmuTmwJXQIUAo0a-TYLtff5rp6hwri5OZ2KEW_LRRhMUrqte7YkD_OomqPJMthriWWb6SSgpUwBz_mLBPnMOErgtdAoyoBXq_eJyFHUx-Q?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSS8BjWpsotV8rtSb1rt0PpqNufGwF-QMjuKlVO_Vor6uFa8UfqHULAwjWKtKJLrXg6lacy5PDjLF6B4Q7Jpgq1CL4mWslIkhkndnYnFKY3AiNIIB1BS8LQLqKCGJDgu5jE5JA?key=VYJVAqKhTdZyHt8enJbiwA)

e) Botões (button e input type="submit/reset"): Os botões servem para enviar ou resetar os dados do formulário.

<button type="submit">Enviar</button>

<input type=”submit”>

<button type="reset">Limpar</button>

<input type=”reset”>

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcP4hH_ortDP0U9B0wdI3mRCfOvqPcnejMuh7vdd3oEVO_rS_vc7YOdf0rExYxot5-tPkaLew8p28Hvxb1bV3VeNpl6tt--xICLCbPGIky8kjT9XYx9qZyWkhahuLY--jUEN2ZqBg?key=VYJVAqKhTdZyHt8enJbiwA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfMJ12vgjITPhU5oAa9MR2BWG3oSyk7hoO83Ty9H8DQ0VxfvnyZ8IdKu6KH7A96tQIv7T4ptR0Uzl56agchx8-eZE7l3UJcJKONZ33RFGRqYgLgUvgXMykAesS7Vxzj5Bwvb71s?key=VYJVAqKhTdZyHt8enJbiwA)

---
### **1.2 Validação de Formulário**

Podemos usar atributos para validar os campos antes do envio.

- required: Campo obrigatório.
- maxlength: Número máximo de caracteres.
- min e max: Define limites para números e datas.
- pattern: Expressão regular para validar formatos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcymqgu0ILOk6koC9A6HstjGPDSzdjlt_5__CgI-brLQFpstvFvPtQqQpp3hycIQ25bIa6omwoY8kcUnZypltD5Hj5q7emH1jqNDHZDznIlQBB5QwnqBGMAgomLq3wW2xCoHviT?key=VYJVAqKhTdZyHt8enJbiwA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeOIDkjiqnnX83qt_PoBjVTc0XZXi1ZIp-O_31zEkxM7wPhmOI1l5ttbuUaCifCKJMW8ad1g1yyfRCNtaphAH9D78tgU2zRafunpep-BXpOIjCc6iqCeTgav2_-osZbAUEjrNDXWQ?key=VYJVAqKhTdZyHt8enJbiwA)

  