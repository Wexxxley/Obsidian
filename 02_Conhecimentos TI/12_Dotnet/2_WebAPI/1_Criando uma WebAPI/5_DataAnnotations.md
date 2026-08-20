
---
### **1. Data Annotations**
Data Annotations é um conjunto de atributos que você pode aplicar a classes e membros de classes para configurar o comportamento no EF Core. Esses atributos são muito úteis para definir regras de validação e restrições de banco de dados.

São necessários esses dois Usings

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcC99CazaPcldcjQg2q9zjTKSJ-22xhAUChI4HZ0AAA9j5gQBbYpYeq9Xz_XMx1_002YG-D_HmdFlcPe7Esgn-3P7TVImb3l4xpqQBjKvNxaOG4idiaLSbjNtN2ZUI_pI8Dnt-7HIubkFb0Ba4bwCoCE0iI?key=SZHaDLu24DLXyFgiFaRNLA)

Principais atributos: 

1. **Key:** Indica que a propriedade é a chave primária da entidade.
2. **ForeignKey:** Indica que a propriedade é uma chave estrangeira.
3. **Required**: Específica que é not null
4. **Table(”name”):** Especifica o nome da tabela para qual a classe deve ser mapeada.
5. **Column(TypeName = "decimal(10,2)"):** especifica o tipo usado no database.
6. **MaxLength e MinLenght:** Especifica o tamanho máximo e mínimo de uma string.
7. **StringLenght:** usado para validar o tamanho máx e mín de uma string.
8. **EmailAddress:** Valida se a propriedade contém um formato de e-mail.
9. **Phone:** Valida se a propriedade contém formato de número de telefone.
10. **Url:** Valida se a propriedade contém um formato de URL válido.
11. **CreditCard:** Valida se contém um número de cartão de crédito.
12. **Range(min,max):** Define o intervalo máximo e mínimo de valores permitido para um campo numérico. Usado para validação.

Assim ficou as classes com Data Annotations

![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeX5IcCT-NurpUJH5gbpaO2y5ls6Yw2nolx7cPHiXk7aURyUJ064vbxuyYLhjGrFSP4raJBfVz0_FN805EZhw5RptkWpeXw0N7qiQRYmHUd9uXzbmFsT9mg3vFssiKnQAYSZKm44RENE8JdSSQD_xsJaEc?key=SZHaDLu24DLXyFgiFaRNLA)

![700](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe7ZoBirCkc0QH8DyroUEESQoE-h2X6nPl5AVQaSQhEHNB90gT29cWcIF1MBKDrmjWKijX29s45Nr24XhazfC6jF2qNesR7Mth1HQGwJv22-yx5tOmz9ZQ94aBCKzBiS9R0mb6yeFG5XBae4NyoJAR2Wglo?key=SZHaDLu24DLXyFgiFaRNLA)

Após essas mudanças, basta adicionar uma migração e atualizar o database.