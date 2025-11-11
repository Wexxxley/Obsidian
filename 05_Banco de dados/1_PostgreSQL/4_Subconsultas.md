
#Concluded 

---
Uma consulta aninhada é uma consulta que é executada dentro de outra consulta. Ela é usada para calcular ou buscar um resultado que será utilizado na consulta externa.

Tipos de Subconsultas Aninhadas: 
1. **Subconsulta Escalar:** Retorna um único valor.    
2. **Subconsulta de Única Linha:** Retorna uma linha completa
3. **Subconsulta de Tabela:** Retorna várias linhas e várias colunas.

---
### 1. Any, some e all 

 Os operadores any, some e all são usados em conjunto com subconsultas e têm a função de realizar comparações entre valores de uma consulta externa e o conjunto de resultados de uma subconsulta.

1. Any e Some: Ambos operadores são equivalentes e são usados para comparar um valor com qualquer valor do conjunto retornado por uma subconsulta.
    
2. All: é usado para comparar um valor com todos os valores retornados por uma subconsulta. A comparação é verdadeira somente se o valor na consulta externa satisfizer a condição para todos os valores retornados.

---
### 2. Exists e not exists

 Os operadores EXISTS e NOT EXISTS são usados para testar a existência (ou não existência) de registros que atendem a uma condição em uma subconsulta. São úteis para consultas que precisam realizar operações baseadas na presença ou ausência de dados em outra tabela.

**Exibe usuário que não segue ninguém**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcc_Qroqc1llPjOljsjzY6-icpwE3feVVFHQnSviEL-MGWfpBUTl_bNELd8zx_kksv9sao7h0vVI_CNIlkwCjd5t0Lp93oxvXewtiqy_b5cL0CQ3rutxDX2sXGNUi5-cEg6bh1QVsQu9EHsiK7XE3QzI5g?key=jqcuw0c7mMfsTTEWWceZSw)

**Exibe data do pedido, valor  e a quantidade de produtos por pedido**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7g_U3o25ZD1YStGOy5ehcVSNTdVzkTQmP6ud_uh3DDgowWyqKg4OAZhH61eAppRSBJmUnnP5xTsIughZmCTGrYxc8T-pjTDfC4M_bPVWWLocD5n6cUrL5S-q5AnhQ9hLOJu_hj6eIdKnUcxSJHOE1Hcc?key=jqcuw0c7mMfsTTEWWceZSw)



