
#Concluded 

___
Um banco de dados é uma coleção de dados persistentes que é gerenciada e utilizada para suportar operações. Os bancos de dados são projetados para armazenar informações relevantes para sistemas. 

**SGBD (Sistema de Gerenciamento de Banco de Dados):** É um software que auxilia na criação, manutenção e utilização de bancos de dados fornecendo uma interface entre o usuário e os dados armazenados. Como: Oracle, SQL Server, PostgreSQL, MySQL.
  
**Banco de dados relacional:**  armazenam dados em tabelas com linhas e colunas que se relacionam entre si.

___
### **1. Linguagens do SGDB**

**SQL (Structured Query Language):** SQL é a linguagem padrão para consultas, manipulação e administração de bancos de dados relacionais. 

1. **DDL (Data Definition Language):** Parte do SQL que permite definir a estrutura do database.
2. **DML (Data Manipulation Language)**: parte do SQL usada para manipular dados em tabelas. 

---
### **2. Criando uma tabela**  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_IEiul6F6a033IBxBnx5YPsznycH2lX4KDJ1y_I6imhAbLoolIjMhLyV4__-3Gy577_g3WtP8QxeKkP24JSrvaNCVvAIpS7PRQUm2mX1Vt8eABdQ6VfIUgwOZVot8XYpTJk-q0h7FD2FQx-lw5gzoNTBc?key=jqcuw0c7mMfsTTEWWceZSw)

---
### **3. Constraints**

As constraints (restrições) são regras que você pode aplicar às suas tabelas para impor a integridade dos dados. 

**Null e not null**
- Null: Indica que pode ter um valor ou não.
- Not null: Cada registro deve ter um valor.
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdCZY6aIm9dwfUAPZXZIPk-gPj3b4-kGr3_cW8Yk4p9et7ltbKLOYgYA7AHixBxJsO_Yf4frp1Vw9e4BPjaHIJW56cFXT2KSODUSHCAnnPSqJp01sGc1cQDyNY5gmKU_CdX03Yk--rz215JW46mXrUBQOUQ?key=jqcuw0c7mMfsTTEWWceZSw)

**Primary key e Unique** 
- A restrição PRIMARY KEY é usada para identificar exclusivamente cada registro em uma tabela. Uma tabela tem que ter uma primary key, e ela deve garantir que todos os valores nela sejam exclusivos e não nulos. 
	
- A restrição unique é usada para garantir que todos os valores em uma coluna sejam únicos, o que significa que não pode haver duplicatas nesses valores.
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAmAr71s7MUXiJcdrn5UYMC2uwVYMG02Ir8lySNFJqlg0wbmwxQXKPJO7tOwwFpGI6ao60M_PzyAbEngPbyD5J-QUCaN4TRKeVUvby17roNZRjmsfgH8bDClKTRef-fz3_AbXHSmIi3X7q78ypnxXmtDI?key=jqcuw0c7mMfsTTEWWceZSw)

**Default**: Define um valor padrão para uma coluna caso o valor não seja especificado.
	 ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdbDNUf1lTtbcWHKIC03erIedXsJZj9VX3XNGrjcMVYrdLdqdUEyf6bRxMxCVs3b4Zdd1I3ruglcL5i6WOWEGfg24Dr3e682NghpQZHGDUI-JkQFw2DrLP7sx14bkVPfFBxBeohqGv9Szo0sS2elkaj-PWK?key=jqcuw0c7mMfsTTEWWceZSw)

**Foreign key**: Uma chave estrangeira (foreign key) estabelece uma relação entre duas tabelas e garante a integridade dos dados. Isso impede a criação de relações inconsistentes.
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6VGHSoooo_zQG64VmnJxB0-dUSF2tdr0ZSkFWxSawv_GPuXY6MIJkA28uKWJpx-IS8uAiKEB8DIly0ufEsCwgnXeHBXu0kEs-jCcSwXP9eKKYx3Lw1v8cKzZAloumqY9YpRJjpYR3sOyJHL_DmkaFHb0?key=jqcuw0c7mMfsTTEWWceZSw)

---
### **4. Tipos de dados SQL** 

**Inteiros**
   - INT:  32 bits.
   - SMALLINT: 16 bits.
   - BIGINT: 64 bits.

**Decimais e Numéricos**
   - DECIMAL(p, s) Armazena números decimais com até ‘p’ dígitos,  dos quais ‘s’ podem estar à direita do ponto decimal. Por exemplo, 123.45.
   - NUMERIC(p, s) Similar ao `DECIMAL`.
   - FLOAT: Armazena números de ponto flutuante de precisão simples.
   - REAL: Armazena números de ponto flutuante de precisão simples.

**Texto e Cadeias de Caracteres**
   - CHAR(n): Armazena caracteres de comprimento fixo. Ex: usado para cpf
   - VARCHAR(n): Armazena caracteres de comprimento variável. 
   - TEXT: Armazena desde grandes volumes de texto até pequenos volume.

 **Data e Hora:**
   - DATE: Armazena apenas a data.
   - TIME: Armazena apenas o horário.

 **Booleano**
   - BOOLEAN: Armazena valores booleanos (0 ou 1).

---