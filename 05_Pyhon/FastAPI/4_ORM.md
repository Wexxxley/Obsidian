
---

ORM (Object Relational Mapping) é uma camada que permite conectar a programação orientada a objetos com bancos de dados relacionais, abstraindo os comandos SQL subjacentes. Vamos utilizar o ORM SqlModel.

### **1. Principais recursos**
- O ORM permite mapear classes e modelos de forma a realizar operações no banco de dados. 
- O ORM traduz automaticamente as instruções SQL para refletir as mudanças no banco de dados, e transforma os dados recuperados do banco em objetos.

![Pasted image 20250610151959](../../attachments/Pasted%20image%2020250610151959.png)

1. Ao importa tudo isso no seu`database.py`, você está garantindo que o **SQLModel** consiga mapear todas as suas classes de modelo para as respectivas tabelas no banco de dados.
2. **Engine**: O motor de conexão com o banco de dados
3. **DATABASE_URL**: Define a string de conexão com o seu banco de dados. É uma prática recomendada carregar isso de variáveis de ambiente
4. **create_db_and_tables:** função para criar as tabelas pelo primeira vez (chamada na main)

---
### **2. Criando modelos**

**Relacionamento 1:N**

![Pasted image 20250522155121](../../attachments/Pasted%20image%2020250522155121.png)

![Pasted image 20250522155137](../../attachments/Pasted%20image%2020250522155137.png)

Na main é criado o banco ao iniciar, mas so é criado a tabela uma vez.

![Pasted image 20250522154841](../../attachments/Pasted%20image%2020250522154841.png)

### **Exemplo de get**

![Pasted image 20250610154252](../../attachments/Pasted%20image%2020250610154252.png)

### **Exemplo de get all**

![Pasted image 20250610154327](../../attachments/Pasted%20image%2020250610154327.png)

### **Exemplo de get quantity**

![Pasted image 20250610154400](../../attachments/Pasted%20image%2020250610154400.png)

### **Exemplo de post**

![Pasted image 20250610154429](../../attachments/Pasted%20image%2020250610154429.png)

### **Exemplo de put**

![Pasted image 20250610154517](../../attachments/Pasted%20image%2020250610154517.png)

### **Exemplo de delete**

![Pasted image 20250610154543](../../attachments/Pasted%20image%2020250610154543.png)

