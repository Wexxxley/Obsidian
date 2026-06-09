
#Concluded 

---
### **1. SharedPreferences e DataStore** 

É um framework para armazenar pequenas quantidades de dados primitivos. Os dados são salvos em um arquivo XML no diretório privado do aplicativo. 
- **Uso:** Configurações de usuário, flags de status e pontuações em jogos.
- **Limitação:** Não deve ser usado para dados grandes ou complexos, pois a leitura/escrita do XML pode bloquear a thread principal se o arquivo for muito pesado.  

O DataStore foi desenvolvida para substituir a SharedPreferences. Projetada para armazenar conjunto de dados simples do tipo chave valor.
![](../../../../attachments/Pasted%20image%2020260609074243.png)

- **Preferences DataStore:** Funciona armazenando dados soltos no formato de chave e valor. É a abordagem mais simples, ideal para configurações básicas (como salvar a preferência do usuário por tema claro ou escuro).
- **Proto DataStore:** Em vez de salvar valores soltos, ele permite salvar objetos complexos (como uma classe Usuario). Exige a definição de um esquema (um arquivo de contrato informando a estrutura dos dados) prévio.
![](../../../../attachments/Pasted%20image%2020260609074347.png)
### **2. Armazenamento Interno**

Refere-se ao sistema de arquivos privado do aplicativo no disco rígido do dispositivo.
- **Funcionamento:** Arquivos salvos aqui são acessíveis apenas pelo seu aplicativo. O sistema operacional garante o isolamento de processos.
- **Cenário de uso:** Logs internos ou pequenas imagens que não devem ser visíveis na galeria do usuário.
- **Segurança:** Os dados são removidos automaticamente quando o usuário desinstala o aplicativo

### **3. Armazenamento Externo**

Espaço de armazenamento que pode ser acessado pelo usuário e por outros aplicativos (respeitando as permissões do sistema).
- **Funcionamento:** Inclui pastas públicas como _Downloads_.
- **Cenário de uso:** salvar documentos, imagens.
- **Scoped Storage:** Em versões modernas do Android, o acesso é restrito para proteger a privacidade, exigindo o uso da **MediaStore API** ou do **System Picker**.

### **4. Banco de Dados SQLite**

O Android traz nativamente o motor de banco de dados SQLite, que é um banco de dados relacional leve e sem servidor.
- **Funcionamento:** Armazena dados em tabelas estruturadas com suporte a SQL
- **Cenário de uso:** Aplicativos que gerenciam grandes listas de itens relacionados, como um catálogo de produtos.

### **5. Room Persistence Library**

Atualmente, a recomendação oficial do Google não é usar o SQLite puro, mas sim o **Room**. O Room é uma camada de abstração (ORM - Object-Relational Mapping) sobre o SQLite. Ele mapeia objetos Kotlin diretamente para tabelas do banco.


