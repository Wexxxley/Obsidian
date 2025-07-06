
---
# 1. Contato inicial

 **Criando tabela**  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_IEiul6F6a033IBxBnx5YPsznycH2lX4KDJ1y_I6imhAbLoolIjMhLyV4__-3Gy577_g3WtP8QxeKkP24JSrvaNCVvAIpS7PRQUm2mX1Vt8eABdQ6VfIUgwOZVot8XYpTJk-q0h7FD2FQx-lw5gzoNTBc?key=jqcuw0c7mMfsTTEWWceZSw)

---
## **1.1 Constraints**

 As constraints (restrições) são regras que você pode aplicar às suas tabelas para impor a integridade dos dados. 

**Null e not null**
-Null: Indica que pode ter um valor ou não.
-Not null: Cada registro deve ter um valor.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdCZY6aIm9dwfUAPZXZIPk-gPj3b4-kGr3_cW8Yk4p9et7ltbKLOYgYA7AHixBxJsO_Yf4frp1Vw9e4BPjaHIJW56cFXT2KSODUSHCAnnPSqJp01sGc1cQDyNY5gmKU_CdX03Yk--rz215JW46mXrUBQOUQ?key=jqcuw0c7mMfsTTEWWceZSw)

**Primary key e Unique**
 A restrição PRIMARY KEY é usada para identificar exclusivamente cada registro em uma tabela. Uma tabela tem que ter uma primary key, e ela deve garantir que todos os valores nela sejam exclusivos e não nulos. 

 A restrição unique é usada para garantir que todos os valores em uma coluna sejam únicos, o que significa que não pode haver duplicatas nesses valores.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAmAr71s7MUXiJcdrn5UYMC2uwVYMG02Ir8lySNFJqlg0wbmwxQXKPJO7tOwwFpGI6ao60M_PzyAbEngPbyD5J-QUCaN4TRKeVUvby17roNZRjmsfgH8bDClKTRef-fz3_AbXHSmIi3X7q78ypnxXmtDI?key=jqcuw0c7mMfsTTEWWceZSw)

**Default**
 Define um valor padrão para uma coluna caso o valor não seja especificado.
 ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdbDNUf1lTtbcWHKIC03erIedXsJZj9VX3XNGrjcMVYrdLdqdUEyf6bRxMxCVs3b4Zdd1I3ruglcL5i6WOWEGfg24Dr3e682NghpQZHGDUI-JkQFw2DrLP7sx14bkVPfFBxBeohqGv9Szo0sS2elkaj-PWK?key=jqcuw0c7mMfsTTEWWceZSw)

**Foreign key**
 Uma chave estrangeira (foreign key) estabelece uma relação entre duas tabelas e garante a integridade dos dados. Isso impede a criação de relações inconsistentes.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6VGHSoooo_zQG64VmnJxB0-dUSF2tdr0ZSkFWxSawv_GPuXY6MIJkA28uKWJpx-IS8uAiKEB8DIly0ufEsCwgnXeHBXu0kEs-jCcSwXP9eKKYx3Lw1v8cKzZAloumqY9YpRJjpYR3sOyJHL_DmkaFHb0?key=jqcuw0c7mMfsTTEWWceZSw)

___  
# 2. Consultas simples

Com o select é possível selecionar colunas específicas ou todas com ‘*’.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdDhyKukNZP5q6yxEhgJEzA3AudM1snWBq0eKx4K837JwDxahirNwzgHUyhWmuU_yDp3GdW3s4u9M4ofXSWLQ1cPPu6U4wHETiUoujffYFzUWvjmtXl4Z_VPOkWpfluuAmO4UWBo2I-Qn3Y5TFegR3RB8A?key=jqcuw0c7mMfsTTEWWceZSw)

É possível resumir várias colunas em apenas uma por meio de concatenação. “||”

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcZK6SRbFeoqYojlRhHfr1XViNsWNMSfivzhdLPDKNtZ3e1j31-q7FssCgO6-3XV6xvejBtpSb_y34qYN_3O0LspJ-8Z-rXasec-Mggm-mkBWoCe56vjgiNluw0ialRRo_V4REdvaPlzeF12Pkha0c6HRfA?key=jqcuw0c7mMfsTTEWWceZSw)

É possível limitar a quantidade de linhas

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdith03ZU7rCgdW_E2KC3ffxvrMFmF0-eB3rC4yUrrowAVdt3VAFl7ZLg-QbVGOUQiY9HjRbU3e-j3EoR3GIJ-4TwYNk0J2GUFzyVfGnPZJTnV9dJlQNBChWVzmUDaMpD_r7rDBGHJNQaraR200EhvQTQkm?key=jqcuw0c7mMfsTTEWWceZSw)

### Where

Com where é possível filtrar os dados com base em condições.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFudLeJ-9sCz5gHEfVMGs21YUodz0g_Y_qRSUZZNiMnhkDN6bZhuBDmJnlURAoQWnVCGa37nhwGXsMrV9oJy_3P-D7fBjziILLqKDeI1nU-JUvvZ2wJXxtIXQaaKhGM_sjm_DQzNYvr3aJxPCU?key=jqcuw0c7mMfsTTEWWceZSw)

### <Like

 O like é usado para encontrar valores que correspondam a um padrão específico em uma string. Existem dois caracteres especiais que podem ser usados para encontrar padrões:

  

1) %: Ex: 'C%' corresponderá a qualquer valor que comece com "C", como "Carlos".

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXez3BVWMmjkKD6csogQ_dZYtaSllmdYOc6j2MG1UpEyotqq3XxJcgQkpP1R9mGm867Y1aL_SPu54x2Z_aMsJjnhEJdGsygGbVsTTUnRAagESSNLTmANQr3rC7Mcav-VEu7lSeeXhHMxvuiVtpbzmhpDbVDt?key=jqcuw0c7mMfsTTEWWceZSw)

  

2) _  : Ex: 'C_' corresponde a valores de duas letras que comece com "C", como "CE".

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdc6k7Z_XXm5XOWs4QLDGi5PPd3rhytwue9yLTo6FtFGeBRQR1Sjl6Afiq5r3Ac2CehZ6zTBCKrjCUYEyy30u1kS0XeWulsemVKNUz0hsNfY2KIgv3wuzePV9mLvIzqQDGXPOifFIPLDWVEuJSIFVxiBVnr?key=jqcuw0c7mMfsTTEWWceZSw)

### <Between

Between é usado para selecionar valores dentro de um intervalo.

1) Uso com valores numéricos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcWWL-SguB9fQdxQ2XvpeqWnnETIjBWLjbnLG4C3JKXMIjp4dex1zRDlNpN0A_L_T8ph_R_9Uv5AG_r-FCEykFTXtDwztppKIk84DamhsN_N8zHqg7JDDKLwcbHz95MVTnaN8j_v2_UWOIWgbugqblhAIE?key=jqcuw0c7mMfsTTEWWceZSw)

  

2) Uso com Valores de Data e hora

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeh9xs0lCLnndLwPjm8dux7adhLnlmAHgxS_J9EMhYbwcqFybLEsr0X3d37LLfQOZDFgpE1jO7Q4uGI-eZcckbt9RPNTt9h9U67m0lRw_7_QfuDT96wAV7JhMy7y8wUqRJAnunhzjsSODVRaKmN3yjw9uo?key=jqcuw0c7mMfsTTEWWceZSw)

  

3) Uso com Valores de Texto (Ordem Alfabética)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeGCxLEFRrXvpzDwJzKoUOLAVCgVIGm5l4Qm6CVbMbcoi4jDA3gEKupVD6dQc865iC12222m3oczkKhqMYGtRaBWbP9BQ99qMTY4s9DwcaA0hJFzzqewzr-qvCcQugMFYYxdj2SLPnhpqxFI4CoVOpXeEY?key=jqcuw0c7mMfsTTEWWceZSw) 

  
  
  
  
  

### <Order by

O Order by é usado para ordenar os resultados com base em uma ou mais colunas.

  

1) Crescente 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdzBwBKxrplg2y2jeXFD2j39PDqCjzCRZDk43Wq1F_JLyYmed2kYPHTVvr7DbUXjI0TaNCGwuxwlX3vB2AAXvZal8XX24wG8a5s_6Ty9yzvneqY2gQXGRfedm58_Wt1jtz1QlMAOiVamzkzdE0Wot9wWv2U?key=jqcuw0c7mMfsTTEWWceZSw)

  

2) Decrescente 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5F77U2jz_sdkr5GVfR2wKgMSYwpiG1A554rKCLxJrpyVcFxUo0-4fhYu3AKmSWEIhu9KnzmTO0ql5S-oDzi1xpZmMnNXAd6L3pajzNGjrwZ7pnlMdYsniBw2iMenEcOKkxmLJhdFC9QQRYjgzijWtjwOO?key=jqcuw0c7mMfsTTEWWceZSw)

### <Alias

 Com o Alias é possível renomear uma coluna.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe0yntAYSu8WKfgzBpAAsRWkCCtNOAaqYIZf3zruUgbiFL3eqHJ6GzWSjiiUWyUr-w545zG1SZvDjTwCn0GGamLoVygVim-R4mvj1HjdCegKoiuhjSSHBFUNrEOI_Rf5yWvIOrWyYf3v6P0D41I5_Qvao8?key=jqcuw0c7mMfsTTEWWceZSw)

  

### <Tipos de dados SQL 

  

1. Inteiros

   - INT:  32 bits.

   - SMALLINT: 16 bits.

   - BIGINT: 64 bits.

2. Decimais e Numéricos

   - DECIMAL(p, s) Armazena números decimais com até ‘p’ dígitos,  dos quais ‘s’ podem estar à direita do ponto decimal. Por exemplo, 123.45.

   - NUMERIC(p, s) Similar ao `DECIMAL`.

   - FLOAT: Armazena números de ponto flutuante de precisão simples.

   - REAL: Armazena números de ponto flutuante de precisão simples.

3. Texto e Cadeias de Caracteres

   - CHAR(n): Armazena caracteres de comprimento fixo. Ex: usado para cpf

   - VARCHAR(n): Armazena caracteres de comprimento variável. 

   - TEXT: Armazena desde grandes volumes de texto até pequenos volume.

  4. Data e Hora:

   - DATE: Armazena apenas a data.

   - TIME: Armazena apenas o horário.

 5. Booleano

   - BOOLEAN: Armazena valores booleanos (0 ou 1).

___________________________________________________________________________

## 3. Fazendo atualizações de forma segura no database

### <Transações

-Beggin: Marca o início de uma sequência de operações que devem ser tratadas atomicamente. As transações garantem que todas as operações sejam executadas com sucesso ou que nenhuma delas seja executada.

-Rollback: Se ocorrer erro na transação, o rollback reverterá as alterações feitas. 

-Commit: Se a transação for concluída com sucesso, o commit confirma todas as alterações feitas dentro e as aplica permanentemente ao banco de dados. 

  

### <Update

 Update é usado para modificar os dados existentes em uma tabela.  É necessário tomar muito cuidado com esse comando. Por isso é interessante usar as transações para garantir a integridade dos dados.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5YzP533gaxVczBqjoSX-W2vHLfaXB_5v0VW-LhgdGiFpoGzRY3aQBzoypmxIv2G_zuBS3oJMvqKdY6VzZDR6gfRsHA1VnEJw_ByaATqYFmammyEkC5sGLRrVY3m8iVwoB5lanNlLoqqRWQ64dXG63zQ6L?key=jqcuw0c7mMfsTTEWWceZSw)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcIxp37RAgqWwZcil7LQV65tSAA4gnlgggnvbuUR6BwEC0xB2vV5xhJw_YSC24VVNsZLt2BBmdCOovdCiq5eezKLZBWNmVvOWLh4feDH18W3NLRIjSEtMT_8Dh_fctgOerUCIEEKOaDkjhzJ870jUxcd9UI?key=jqcuw0c7mMfsTTEWWceZSw)

 Você executa os updates, verifica se tudo está certo, em caso de erro executa o rollback, em caso de sucesso executa o commit.

  

### <Delete

 Delete é usado para remover registros da tabela. É necessário tomar muito cuidado com esse comando. Por isso, novamente, é interessante usar as transações para garantir a integridade dos dados.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfyVdYoMpyMQ4KggDj_U7YFq0gqkO2IFAxdP2hNUetEIfO29mCg9vFbmfz6n_G15aAS6mIVP0BFSBwkqUDpKbPMzHiJp1oRbRyy4viJ-zOXbYnTBUvUTuJsrFuFrVs0rfoajymX7X8IorIGSEd0A4dGK3Cp?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 4. Funções de agregação

 O nome funções de agregação vem do fato de que essas funções operam sobre um conjunto de valores para produzir um único resultado. Elas condensam vários dados em um único valor.

 As funções de agregação podem receber a cláusula distinct. O uso de distinct  permite que a agregação seja realizada apenas sobre valores distintos de uma determinada coluna. Isso é útil quando você deseja evitar que valores duplicados sejam considerados ao calcular somas, médias, contagens, etc.

### 1. Média

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfz41XvT-Yp7sKWt8bXBzSdeD79lfOotDGqHdaNHQ9yz62BNHThhlRUcHpOCSKlksGxulyZ2hypY8DMaeO3aDn9THCS23yUpvVuRCXxnnitJXsI54UYKUcInAV4JtShrgq38hhUwE9SZkBXKEwiNCAnhRdr?key=jqcuw0c7mMfsTTEWWceZSw)

### 2. Contar registros 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdYNnoI2a-FfMvwYKfikrucfm_I6AtZGaiSm9WZ1LaGqwdzCPH-w36oLIqXTGJBuAXsq0NtQ5klkr8_-fWHCLBMlCOBbiDOa_3revaFnFLcmxag9WvKz9AnG_Tml_JE7xFZ41dnuguQNnLoxWDY4pK3-okv?key=jqcuw0c7mMfsTTEWWceZSw)

### 3. Contar quantidade de valores não nulo

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfILJWeUqIwdEXL2pv_i2cRk-R6Q4Dif_MIlOoxHprcJrHMDnH8r0ziu4_TSkv-6xbA4L1zVX6BGzaKsqpWVFfJf_GEvkCiphMw42mMcNg1ZqUD47jR1HqXQtVUiy6q4nmqfDpKQlkv_i6asQDxuQqIWzA1?key=jqcuw0c7mMfsTTEWWceZSw) 

### 4. Valor máximo e valor mínimo

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUlAzMhuibbWlrVEPiTVPsFeRE1MttYU3UmlmCUCF6xU4N_JuCQLZMLIQ9IdOvArWmFERHH8Fkf-aRj1XStE0Zcfixr1_JVkM-zvUXnM3Hs0QSzX6zrr5167TVbIr9FEse3FN235FyXVYwXyvrUIE5z4NG?key=jqcuw0c7mMfsTTEWWceZSw)

### 5. Somatório

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFY0RyzT7FhSzJ7JHovJDZOvxi9G4gXLEPytxHRdYzY25rnoRxVSXh6_oh0uP5wii7JxftEYFd6ncVpoQnhb8b2cJQzDOqaDClZgqoPBF5OntD_EJzRnDGVbcmSxy5ebpfiMUHJUfJpH50nKWlaXft9-aW?key=jqcuw0c7mMfsTTEWWceZSw)

  
  

### 6. Group by

 A cláusula Group by é usada para agrupar linhas que compartilham um valor comum e, em seguida, aplicar funções de agregação a cada grupo. É especialmente útil para realizar cálculos sobre grupos de registros.

  

//Valor de compra total feita por cada cliente.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfeHCL4UmrWN3fhFpAgVFIT_ugf0rCRQmsBUQhnjoy_duCJnbDo8cm0ydvH5iUinKOcyoOkZGP-O3y2cKv92rdNKZhHLdmdSYo0VP7elu3WGFG6e4kpXsyxAYDjKriZhMj55xVNrQ0Mm9zxRb6Rkbwl7Syw?key=jqcuw0c7mMfsTTEWWceZSw)

### 7. Group by mais condição

//Agrupa pelo cliente, soma os valores, e apresenta os que são maiores que 700.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXePzB6PWR6pdcIJaCSqJZd9buNolfU-jgR4mcUAr_Se5kvPyF2Ml5VmziGxS2zJX1IRNCzTkl0hTNV34lHgaBrcpbrKuWd8C7as5Dc18s3ynCVbeePwEDs36e2YYjs7qePY6Zl-YAHEEBhq6-LmRQGaOJcG?key=jqcuw0c7mMfsTTEWWceZSw)

### <Having

 A cláusula HAVING é usada para filtrar os resultados de uma consulta após o agrupamento de dados realizado pelo GROUP BY. Ela permite definir condições sobre os grupos formados.

  

WHERE x HAVING:

- WHERE: Filtra linhas antes do agrupamento (filtra os dados brutos).
    
- HAVING: Filtra os grupos após o agrupamento (filtra o resultado da agregação).
    

  

Exemplos de agrupamento

  

// Exibe o nome do usuário e número total de postagens de cada usuário.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeIF1xm5yzEd2c-Uyrnw-mD_yhJX15oPaTlQkMIb-7XlwAoQdXjycyIyZA0uJT3rI9Zi6glknXU2Nb6E6dOZzEV4t3xDvPQu44wiAXTYf5-BgxpOP29ckOCMLy92o1A5_rsrqg6BAvppDdnwmL7lweQ0kHe?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 5. Subconsultas

 Uma consulta aninhada é uma consulta que é executada dentro de outra consulta. Ela é usada para calcular ou buscar um resultado que será utilizado na consulta externa.

  

Tipos de Subconsultas Aninhadas: Existem três principais tipos de retorno em uma consulta aninhada.

1. Subconsulta Escalar: Retorna um único valor.
    
2. Subconsulta de Única Linha: Retorna uma linha completa
    
3. Subconsulta de Tabela: Retorna várias linhas e várias colunas.
    

### <Any, some e all 

 Os operadores any, some e all são usados em conjunto com subconsultas e têm a função de realizar comparações entre valores de uma consulta externa e o conjunto de resultados de uma subconsulta.

1. Any e Some: Ambos operadores são equivalentes e são usados para comparar um valor com qualquer valor do conjunto retornado por uma subconsulta.
    
2. All: é usado para comparar um valor com todos os valores retornados por uma subconsulta. A comparação é verdadeira somente se o valor na consulta externa satisfizer a condição para todos os valores retornados.
    

### <Exists e not exists

 Os operadores EXISTS e NOT EXISTS são usados para testar a existência (ou não existência) de registros que atendem a uma condição em uma subconsulta. São úteis para consultas que precisam realizar operações baseadas na presença ou ausência de dados em outra tabela.

  

// Exibe usuário que não segue ninguém

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcc_Qroqc1llPjOljsjzY6-icpwE3feVVFHQnSviEL-MGWfpBUTl_bNELd8zx_kksv9sao7h0vVI_CNIlkwCjd5t0Lp93oxvXewtiqy_b5cL0CQ3rutxDX2sXGNUi5-cEg6bh1QVsQu9EHsiK7XE3QzI5g?key=jqcuw0c7mMfsTTEWWceZSw)

// Exibe data do pedido, valor  e a quantidade de produtos por pedido

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7g_U3o25ZD1YStGOy5ehcVSNTdVzkTQmP6ud_uh3DDgowWyqKg4OAZhH61eAppRSBJmUnnP5xTsIughZmCTGrYxc8T-pjTDfC4M_bPVWWLocD5n6cUrL5S-q5AnhQ9hLOJu_hj6eIdKnUcxSJHOE1Hcc?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 6. Alter table

1. Add column: Adiciona uma coluna a tabela

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTJnlLUCliOXchqxIth4h7qX5Q8ndmhYSVop1GDXzm835e4KFObm3xjIogHcpFf6cKHfvKEvmJLogRNq647QU5od5LNghAI6GAq-GjqFYiafuYvqKAWFM0tcV_ao0lsVQujnQyijOWK2m68weZfqr0K3bo?key=jqcuw0c7mMfsTTEWWceZSw)

2. Drop column: Deleta uma coluna da tabela.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0x0LNdj8GQVAHDGVNJw4PFgvTOhxcpA9fWtSL7oZDGcl-XM1bqR4IpaU1qzmktNqzVycHTXAuAyFdLIB3xiP9eEFjDHBB_d2KZCiPnfLC-V_HbfPByaU4hMHBcNlNwPb1vnJVgGDW7i52vuCw1FR2aFGp?key=jqcuw0c7mMfsTTEWWceZSw)

3. Alter column: Altera o tipo da coluna

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeCUpy4M79o0d3OG8TAl2KNXBChCpRxpw_LqKjMVbCp6wiOK_9nKEt8qA-FvGzoCJyZdTG1_a7oHZfiXexIQ7yyo2L3vuZC5F1sIKD67bDsy1sbk1oqAgrdDkVrIkZ36H26dEkR0jAIwngj3ygmuGXAZcoS?key=jqcuw0c7mMfsTTEWWceZSw)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcP7P-E1Tq8JYl8L-J-2w9JyH791h-Ej34FNAHblgS82MdGxfUo0f5-GGsqXQdwqhznUXQf7w-MUatFJBxWBeNOcg73VcuGpiNK_pYBqHkuYVtf-ZONXQdZgs0eXxVbfZhu7Rp0mLJTz8rmZfely13Mf7Km?key=jqcuw0c7mMfsTTEWWceZSw)4. Rename column: Renomeia uma coluna da tabela.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXekV7Bl3DHdwOxXJQUSUexl4ipjCmQ2rlHYZqOPIOdTLgNOOzJoW2C5fyOvcJviFr9wI0caGDMp38fsDaJnNXIsFEIXx5XEsF255M4tjDuA-hxOeihcBzwaQO6M6EtgeKHFLW8zFrITyfSWha9aELZ1VUk?key=jqcuw0c7mMfsTTEWWceZSw)

5. Add constraint: Adiciona uma chave estrangeira

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6VGHSoooo_zQG64VmnJxB0-dUSF2tdr0ZSkFWxSawv_GPuXY6MIJkA28uKWJpx-IS8uAiKEB8DIly0ufEsCwgnXeHBXu0kEs-jCcSwXP9eKKYx3Lw1v8cKzZAloumqY9YpRJjpYR3sOyJHL_DmkaFHb0?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 7. Join

 É usado para combinar duas ou mais tabelas com base em uma condição relacionada. Isso permite que você recupere dados de várias tabelas em uma única consulta.

  

1. Left join: Retorna todos os registros da tabela à esquerda e os registros correspondentes da tabela à direita, mesmo os que são nulos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPn3NC7nEwMjZ9vdO07ijlMQh6kuzfvj56i7m4M-u99ZSr4VTDarUFbycL2fLb8bMN2NWHX4sWBPxzJ6k-kOOBydV7otD8zQBwAqF8seH9r97Yy-SXgLSDvmdAYeiEUzSr7ojlm2WMKVQna6BD0GaMIIW4?key=jqcuw0c7mMfsTTEWWceZSw)

2. Inner Join: Retorna apenas os registros que têm correspondências em ambas as tabelas. Não retorna registros com valores nulos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfjpPUztMzxitKDtHwq-cM80DtCyBs_ZpLR0QT8q1x9zXY2mjy5cECbvduAEV81KrwDTr0ipuNFCnQQPZiIaG43amYpeNr2iP7_4DFZznTB6DkEwh53CJ8mgmJaSG2LgEhRgnzUKhWs5E35CZ7jjaVPDHfq?key=jqcuw0c7mMfsTTEWWceZSw) 

  

3. Mais exemplos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZQvz7VLsRw6_P4dpQd71Os3cdg0C7jEAI6UhJAfw3u_1SGZhWDicnpBcVLODttDN-LAU4as1dLjIsSAcJ31gr4hs2TCriA8RgghVihcy0nx7SGanYEhMSF9hkD4UUsh8bxcIQA1Fw3Btfm_HI8QrP8-g?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 8. Comandos adicionais

<Extract: Usado para extrair partes específicas de um valor de data ou hora. Ela pode ser útil para recuperar informações como ano, mês, dia e hora.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5TbsMHwREAnOoGBxS4RRpEkR0NmaPjBGKzlkcxtojlkGy90jsLNKEcAA1m1sg4cxh4BKCqtjFRLcNV20vT1ZsePV0bni5B7cR8TvlJ13Ja9897xyDmuDW5WUCHrDNtlzR4mX2hiM-tv2fjdEnaYtTkqA?key=jqcuw0c7mMfsTTEWWceZSw)

  
  

<Substring: usada para extrair uma substring de uma string da tabela

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdvbYh5WA8zGlVkUEWkfgSfVebzKeSGQoTHp8hLjmzDM2DOMBlMWKvz9US6h5B8QiOtdZAFKhLWWK7MSxZQNOXUj5ifzT3foM8eDNQkaUu2iM4pS6tMjHWnVcRhlacOVjwcuqaNmTICWcSnZ2Yf2KACUbBt?key=jqcuw0c7mMfsTTEWWceZSw)

  

<Upper e lower

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAsd-1xITHejOWHPapWxP57lY8pBGUU19iMcrvXhbOx7iFI_Hw6eQ-wjuJoNiQMH1eCIsOnqAlb8sQMxWG4qHwVcG_t6KncLf1kw_wON9G7aS0FuGaEQcMLcFec_BtQTjKTast4xNkQ593YhVgoE1jbx7V?key=jqcuw0c7mMfsTTEWWceZSw)

  

<Coalesce: cria mensagens personalizadas quando o valor é null

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2whR2jzvsNlkGx1nobm-LeMQdw9IxMsGjjTu5wvzX63DYecwCAGP7qntvx0Bpd0npt5S_uN1uGAM5V5FP8PukfUGBIuU-mzt9w1rJ6jKalODbXwxirG9BIIkm6ZntYWF4R7WlFqfBd3GksGavVpT9oQWu?key=jqcuw0c7mMfsTTEWWceZSw)

  
  
  
  
  
  
  

<Case: é uma forma condicional de controlar o fluxo de uma consulta SQL. Ela permite que você execute diferentes ações com base em diferentes condições.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXexdYQLPL8c_WRTEBu98CV3rTAyvNXxSxgsi_84aPf6HxCDkto9dxzOPyKqYLi3TZp53i7dtr6mfklp816SIHwpOVUPCMkZlG1HZn9uAkXQPN1Dx7GSmjXXLhCsJop5McuMjxSuab8g5h2Rm4KgeGSOo3Y?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 9. View

 Uma view é como uma tabela virtual. Ela não armazena dados, mas sim uma consulta que é executada quando a view é acessada. A view simplifica consultas complexas e reutilização de consultas.

- As views permitem que você salve consultas SQL complexas com múltiplas junções, subconsultas ou filtros. Assim, em vez de escrever a consulta completa todas as vezes, você pode consultar diretamente a view.
    
- Se a lógica da consulta precisar ser alterada, você altera a view uma vez, e todos que a utilizam verão as mudanças automaticamente.
    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmSd68X3f8fcbY0Z17wvI1f6Gb0ppRMkf8Y_TEXyEpBb1BucAIyC_H29YfH8nj_zBPu27bTKopunMhsA-gXT_tHrRI14D8fYvmPTJkAGnf7YJB9JNQxJEOgotis_sXmgEM803DZXFE3p5PEOwLJBeUImm6?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 10. Campo autoincremento

 O tipo SERIAL no PostgreSQL é utilizado para gerar automaticamente valores incrementais em uma coluna, geralmente utilizado para criar chaves primárias. Ele simplifica o processo de criação de IDs sequenciais sem que o desenvolvedor precise inserir esses valores manualmente.

  

Usando serial

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeQGOTTjkymL8zvmbOgwmETGBU_TzY8B9gAATaaJ0Hvbi_TSIx89LYtcl95aJTFpPfuY04qT9vz1vd1kH6N22sUkpqbN7gXFpoOfhuQj9slrVQ_MrmGS-i8FUgYzaVFaCMzgf6dARFQaXNv5ycMr5TRnpU?key=jqcuw0c7mMfsTTEWWceZSw)

  

Como funciona o SERIAL

 Internamente, quando você define uma coluna como SERIAL, o PostgreSQL cria uma sequência associada a essa coluna. A cada inserção, o próximo valor da sequência é atribuído automaticamente à coluna.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHFaNIjPFdw5klrE1AGPg__MIdQagkH5uup9VGV8a196gyN7xz_nxz4wZBoz8xDUGcR_CmRIj8goGixMmPRPwfOrdQpqCFaypBI39gAtynGSTWPIriIMlv7MVvBK5ars9jy8OaCLjtzPtI56fE8YKeCGgj?key=jqcuw0c7mMfsTTEWWceZSw)

  

Variantes de SERIAL

- SERIAL: Um inteiro de 32 bits
    
- BIGSERIAL: Um inteiro de 64 bits
    
- SMALLSERIAL: Um inteiro de 16 bits
    

  

Cuidados necessários

- Reinicialização de Sequências: Se os registros forem deletados, a sequência continuará a gerar IDs a partir do último valor, deixando "lacunas". Se você quiser ajustar a sequência, é necessário usar o comando ALTER SEQUENCE.
    
- Overflow: O tipo SERIAL é um inteiro de 32 bits que pode gerar até 2,1 bilhões de valores. Se você precisar de mais, deve usar BIGSERIAL.
    
- Inserções Manuais: É possível inserir valores manualmente em colunas SERIAL, o que pode gerar inconsistências.
    
- Remoção da Tabela: Quando uma tabela que usa SERIAL é excluída, a sequência associada não é excluída. Se você remover uma tabela e quiser excluir a sequência associada, isso precisa ser feito manualmente.
    

Usando serial em tabelas já existentes

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVif04WOyi1WhggLniwn9EHBd6IROFIhW8oYb5UBstXMgnz-GExdSst_QatEqI-dpN7ptvQt2SXYC1bSRnmN3ENX5Lrqa25DGyhCPefgadYRqpZjKeRixB8lv-n5Pfic4oc-j2QqZnypwZkpIJjfwwAMuV?key=jqcuw0c7mMfsTTEWWceZSw)

  

Campo default

 Como mostrado no exemplo anterior é possível definir um valor padrão para cada coluna caso um valor não seja passado.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfOSuXIolkoR8QrdrQKUn8sI5ptImxyTh3h_fSZvvzGao7RtLzNxY1BuQlnydn9myf42GJq7cgC6JNhFgnymBPbUarkDOeTpPoOpnMsvPrwHf4mkVi_M-pOIsMfLpx2WTmqX0N-4nJckW3eR21gRPl4_XQK?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 11. Índices

 Índices são estruturas que aceleram consultas, facilitando a busca em tabelas. Os índices são recomendados em tabelas com muitos valores que precisam ser buscados com frequência. Sem a utilização de índices, quando é feita uma busca, é percorrido por todos os dados da sua tabela e isso é bastante ineficiente.

  

- Duas principais estruturas de dados são utilizadas para melhorar o desempenho de busca: árvores b e tabelas hash.
    
- Índices ocupam mais espaço em disco e gera um custo de inserção maior visto que os índices precisam ser atualizados.
    

  

Definindo um índice para o atributo nome de cliente.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcr4OEKf0WYfGbFltmB1AqWFV_Vr64jXR4R33-r28S3O9sQhwHRRpFoftn8zNrUIFbkrQZ12QqvTu18loxc3V8A3Yn6lsOe5OLxqVurBhW07AjZD2WO5FUt1D-e2B4HLDS1H5GrpXoYJsnj_E_v7EIFweo?key=jqcuw0c7mMfsTTEWWceZSw)

  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

# Tópicos Especiais

___________________________________________________________________________

## 1. Funções

 Funções são blocos de código que podem ser executados de forma repetida e reutilizável. Elas permitem encapsular operações frequentemente repetidas.

 Ao criar funções, é possível usar diferentes linguagens. Essas linguagens permitem que você crie funções que executam operações mais complexas que apenas SQL. O PostgreSQL suporta algumas linguagens, como:

1. PL/pgSQL: É a linguagem procedural nativa do PostgreSQL, baseada em SQL, mas com estruturas adicionais, como loops, condições, e variáveis.
    
2.  PL/Python: Quando você precisa de funcionalidades avançadas de uma linguagem de alto nível, como manipulação de dados complexos ou integração com bibliotecas externas do Python.
    

  

Exemplo 1:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZXAgLBWGIFupe1Y0yoM2jM5DdZIqKjqeE4fpIQ14JDvQXg8w8c-PwQbwvGoSIPd8OP_IAVpmNnqnVO5NY4-lHU6W0fmE-JLgXTNH9y8otI_ORgstp_7kzznfHG-928hc3VJSsknigeDV-PN-riOCxk9N4?key=jqcuw0c7mMfsTTEWWceZSw)

 Neste exemplo, foi criado um função para converter um float em uma string com formato de moeda. Para utilizar, basta usar em um select.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZiIaE28g7xIPaglVOIpuZtsfF2pWUNXG4ENbKWuMNc_BckFqBjK4qIsFPuGdfom1_nVazppMLIeiBWOR6Ao1jIRhm9fcASPX5l33UM3HGuj3llBnpMfxLHMAxKOPl4c7r9uLArgP_YkqiMormzzYK4N7h?key=jqcuw0c7mMfsTTEWWceZSw)

Exemplo 2:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-79RNfzQ1aLZO08mVKgcD--EQkAImoagCEDt2Bg4ivtmOmAuDq5P7sqkfGuNojtD0c0ir9YednBKn_hUIL2NO201eUpKbfPvEPSzClnA3s0z7FyNBfIJVtLex1aLBcNZFzf-i-ljYb7r9P8PepPUoWco?key=jqcuw0c7mMfsTTEWWceZSw)

 Neste exemplo, foi criado uma função que retorna o nome do cliente pelo id.

Declare: usado para declarar variáveis que serão utilizadas no bloco de código. 

Into: utilizado para atribuir o resultado de uma consulta a uma variável declarada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeQUfz0UqgbZlt9pDbKAgDv0D4L9jaR8kQ8ktVfAQPKLsg7xCqm_VDx-v8HB46fAW37YDAjaicZeZ6EinPHKcxbaigrwr6m7VA9lybxvpPr8xIYfAqDibQsk2UDQdXmxTyfssE-GuX2ggKNNOhSsvOyxg3E?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 2. Stored Procedures

 É uma ferramenta que permite encapsular lógica de negócios e manipulação de dados. Aqui estão algumas situações em que é vantajoso utilizá-la:

1. Quando é preciso realizar uma série de operações de manipulação de dados (inserções, atualizações, exclusões) em um único comando. 
    
2. Quando você deseja isolar a lógica de negócios do código do aplicativo. Isso ajuda a manter a lógica centralizada no banco de dados.
    
3. Quando você precisa garantir que uma série de operações sejam concluídas com sucesso ou não sejam aplicadas (rollback) em caso de erro.
    

  

Exemplo 1:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfc4O-iIBGy5k9Sg2S-5HI7CmIfru8TSlAcMunCvEifAizjMsuZkFhOL7ckasYQJVtivnFvn9CTADF1VbaTomlSsOkDn2Sx9tVDr4u79Tlmgsp07VlRv31KMa3wB_d_Pbbu7E5vguLLEa1oewV_WNdQNeE?key=jqcuw0c7mMfsTTEWWceZSw)

Foi criado um procedimento para facilitar a criação de um bairro. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeaHajy3ULUSrXS52UPOYggFLgJQnajjoXp9qtadAXGkHbT88Wh3g6jcU4Lu-kqkSyYvX0f7-rPrXLk-zhUD18Ctpo5Owg_CweTbbu61cz3NhxxdU0C_GZrwwNr8FA1x_YI2Q0bcWp7m8mmN0cywBWEBvom?key=jqcuw0c7mMfsTTEWWceZSw)

  

Exemplo 2:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdAWv20y__ot7JcIKoFgHjrY6m-MWdecfC2YlsaB5KoKlAVMsX2kBwQGUnQHl0-S1e5Dr4Gn3TmAeKBsB6GT7aDpnD7TJsHTqwBlS49lSUsPMNSeArybnx6vJoatdmR0A8-wr0kDxkkLegiYQh2zu4U-ggq?key=jqcuw0c7mMfsTTEWWceZSw)

Foi criado uma procedure para reajustar o preço dos produtos. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYQikBOhxuP4GvsdEc7ELYc-0mrypvNZaZsBinv4W8KnlcjJ5A9i3TRKw_BQuabYumU91JnS64Xi_ew8GqMgov0sLU5wTnREw8qpc2zSXkgzGs8uxftrHbwAVvLfwkvjizQegcqz8JfU4Ky4A7IrRyDPI?key=jqcuw0c7mMfsTTEWWceZSw)

  

Exemplo 3:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZRsILz72NDQb-0FYmm8qDWS-xKpB60M-XyUdZ6gPgkDJZMROl9MGsSjF01MKYC7T0dM9ghHx8B4JgB4AJ6QvaRXbpnbUzg8T4hIWF49yqHBN5EcRXxCdgqrLWhz4iYCFxZD1zCoeoltpMk-j71bz5I_5i?key=jqcuw0c7mMfsTTEWWceZSw)

Foi criado um procedimento para facilitar a exclusão de um produto.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcUHMaNKYl3hyAtwzz6G5k33RGOY2mHJkQRhR37cbf5dDrXMHBoMVhcMjUJ68E4rshmXHkIKT1mpT-eHBK9dYGTtRukZbwB69XlCm8tZAJX62NXYdG3hxQoK_-eE-I1HpaLc2nX3LZ2lM3AnziMRaRW5E0?key=jqcuw0c7mMfsTTEWWceZSw)

  
  

___________________________________________________________________________

## 3. Triggers

 Triggers são procedimentos automáticos que são executados em resposta a certos eventos em uma tabela. Esses eventos podem ser operações de inserção, atualização ou deleção de dados. As triggers são úteis para manter a integridade dos dados e implementar regras de negócio automáticas.

  

1. Eventos que Disparam a Trigger:
    

- INSERT: A trigger é disparada quando uma nova linha é inserida na tabela.
    
- UPDATE: A trigger é disparada quando uma linha existente é atualizada.    
    
- DELETE: A trigger é disparada quando uma linha é excluída da tabela.
    

2. Momento de Execução:
    

- BEFORE: A trigger é executada antes da operação (insert, update ou delete) ocorrer. Isso permite que você modifique ou valide os dados antes de salvar.
    
- AFTER: A trigger é executada após a operação. Isso é útil para ações complementares, como o registro em logs.
    

3. ROW vs. STATEMENT:
    

- ROW: A trigger é executada para cada linha afetada pela operação. Por exemplo, se um UPDATE alterar 10 linhas, a trigger será executada 10 vezes.
    
- STATEMENT: A trigger é executada uma vez por operação. Ou seja, seja lá quantas linhas forem afetadas, a trigger será disparada uma vez.
    

4. NEW e OLD: 
    

- Refere-se ao novo valor de um registro. É utilizado nas operações de INSERT e UPDATE para acessar os valores que estão sendo gravados ou modificados.
    
- Refere-se ao valor antigo do registro. É usado nas operações de UPDATE e DELETE para acessar os valores antes da modificação ou remoção.
    

  

Exemplo 1:

Foi criada uma nova tabela para log de bairro.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZyIAr_gUe7mfgjTTS9ocsbM7xRXwGBQ4JM-L0OhdN3Lsg0fPu3INxcpJFM3MI-erWFn3hj4FOIyqgmjR0Dq93ig5dBtatmQz2jhTT4Z3gFgy1ihC7JBa3qWR_KcLCRYWcCs6l587XSs6KiX4DXN8pgiJg?key=jqcuw0c7mMfsTTEWWceZSw)

 Uma tabela com sufixo "auditoria" é uma tabela dedicada ao registro de mudanças ou eventos que ocorrem em outra tabela principal. Esse tipo de tabela é utilizado para manter um histórico das alterações feitas em registros importantes, permitindo que você rastreie quem fez a mudança, o que foi alterado e quando.

  

 Uma tabela de auditoria geralmente é preenchida automaticamente por triggers que são disparadas ao ser realizado uma operação na tabela principal. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcbuQ4AJWbuvbVYSp-CeOuOuJ5Rdw0uXhRcC3gJXwYz-SpVSHh5JFlRPEXVFfZUhXbtFWKnfmhbDELfwR3vBSmtucqB8hvQDzAPjRaKUuXEoY12DeqC9_MBoggTKXzaL7FyVBbplYZzBTUbakdRldT0-3ko?key=jqcuw0c7mMfsTTEWWceZSw)

 Primeiro foi criado uma função que insere uma tupla em bairro_auditoria.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfIvQItCtnODX70F293TUOvbFmdgDwAIN4Ai-oFLvSxK9SdfmyupycNsNPMWHb0GFkgndCM6dtwNLSuDs8WnUCzhHRbeaCN0CToqx5iIy0nCCYOfTqTz9v3DRI0wynHj5vzrrmtrKUXsTed-yja6EAOUEVk?key=jqcuw0c7mMfsTTEWWceZSw)

 Uma trigger foi criada, toda vez que for feito uma inserção em bairro é chamado a função bairro_log

**