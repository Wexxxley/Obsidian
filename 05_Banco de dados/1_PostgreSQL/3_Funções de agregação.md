
#Concluded 

---
O nome funções de agregação vem do fato de que essas funções operam sobre um conjunto de valores para produzir um único resultado.<mark style="background: #ADCCFFA6;"> Elas condensam vários dados em um único valor.</mark>

As funções de agregação podem receber a cláusula **distinct**. O uso de distinct  permite que a agregação seja realizada apenas sobre valores distintos de uma determinada coluna. Isso é útil quando você deseja evitar que valores duplicados sejam considerados ao calcular somas, médias, contagens, etc.

### 1. Média

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfz41XvT-Yp7sKWt8bXBzSdeD79lfOotDGqHdaNHQ9yz62BNHThhlRUcHpOCSKlksGxulyZ2hypY8DMaeO3aDn9THCS23yUpvVuRCXxnnitJXsI54UYKUcInAV4JtShrgq38hhUwE9SZkBXKEwiNCAnhRdr?key=jqcuw0c7mMfsTTEWWceZSw)

---
### 2. Contar registros 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdYNnoI2a-FfMvwYKfikrucfm_I6AtZGaiSm9WZ1LaGqwdzCPH-w36oLIqXTGJBuAXsq0NtQ5klkr8_-fWHCLBMlCOBbiDOa_3revaFnFLcmxag9WvKz9AnG_Tml_JE7xFZ41dnuguQNnLoxWDY4pK3-okv?key=jqcuw0c7mMfsTTEWWceZSw)

---
### 3. Contar quantidade de valores não nulo

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfILJWeUqIwdEXL2pv_i2cRk-R6Q4Dif_MIlOoxHprcJrHMDnH8r0ziu4_TSkv-6xbA4L1zVX6BGzaKsqpWVFfJf_GEvkCiphMw42mMcNg1ZqUD47jR1HqXQtVUiy6q4nmqfDpKQlkv_i6asQDxuQqIWzA1?key=jqcuw0c7mMfsTTEWWceZSw) 

---
### 4. Valor máximo e valor mínimo

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUlAzMhuibbWlrVEPiTVPsFeRE1MttYU3UmlmCUCF6xU4N_JuCQLZMLIQ9IdOvArWmFERHH8Fkf-aRj1XStE0Zcfixr1_JVkM-zvUXnM3Hs0QSzX6zrr5167TVbIr9FEse3FN235FyXVYwXyvrUIE5z4NG?key=jqcuw0c7mMfsTTEWWceZSw)

---
### 5. Somatório

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdFY0RyzT7FhSzJ7JHovJDZOvxi9G4gXLEPytxHRdYzY25rnoRxVSXh6_oh0uP5wii7JxftEYFd6ncVpoQnhb8b2cJQzDOqaDClZgqoPBF5OntD_EJzRnDGVbcmSxy5ebpfiMUHJUfJpH50nKWlaXft9-aW?key=jqcuw0c7mMfsTTEWWceZSw)

---  
### 6. Group by

A cláusula Group by é usada para agrupar linhas que compartilham um valor comum e, em seguida, aplicar funções de agregação a cada grupo. É especialmente útil para realizar cálculos sobre grupos de registros.

**Valor de compra total feita por cada cliente.**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfeHCL4UmrWN3fhFpAgVFIT_ugf0rCRQmsBUQhnjoy_duCJnbDo8cm0ydvH5iUinKOcyoOkZGP-O3y2cKv92rdNKZhHLdmdSYo0VP7elu3WGFG6e4kpXsyxAYDjKriZhMj55xVNrQ0Mm9zxRb6Rkbwl7Syw?key=jqcuw0c7mMfsTTEWWceZSw)

---
### 7. Group by mais condição

**Agrupa pelo cliente, soma os valores, e apresenta os que são maiores que 700.**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXePzB6PWR6pdcIJaCSqJZd9buNolfU-jgR4mcUAr_Se5kvPyF2Ml5VmziGxS2zJX1IRNCzTkl0hTNV34lHgaBrcpbrKuWd8C7as5Dc18s3ynCVbeePwEDs36e2YYjs7qePY6Zl-YAHEEBhq6-LmRQGaOJcG?key=jqcuw0c7mMfsTTEWWceZSw)


---
### 8. Having
A cláusula HAVING é usada para filtrar os resultados de uma consulta após o agrupamento de dados realizado pelo GROUP BY. Ela permite definir condições sobre os grupos formados.

**WHERE x HAVING:**

- WHERE: Filtra linhas antes do agrupamento (filtra os dados brutos).    
- HAVING: Filtra os grupos após o agrupamento (filtra o resultado da agregação).

**Exibe o nome do usuário e número total de postagens de cada usuário.**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeIF1xm5yzEd2c-Uyrnw-mD_yhJX15oPaTlQkMIb-7XlwAoQdXjycyIyZA0uJT3rI9Zi6glknXU2Nb6E6dOZzEV4t3xDvPQu44wiAXTYf5-BgxpOP29ckOCMLy92o1A5_rsrqg6BAvppDdnwmL7lweQ0kHe?key=jqcuw0c7mMfsTTEWWceZSw)
