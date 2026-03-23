

---
### **1. SharedPreferences**

É um framework para armazenar pequenas quantidades de dados primitivos. Os dados são salvos em um arquivo XML no diretório privado do aplicativo. 
- **Uso:** Configurações de usuário (tema claro), flags de status e pontuações em jogos.
- **Limitação:** Não deve ser usado para dados grandes ou complexos, pois a leitura/escrita do XML pode bloquear a thread principal se o arquivo for muito pesado.  

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


---
## 6. DataStore (Jetpack)

O **Jetpack DataStore** é o sucessor moderno das SharedPreferences.

- **Funcionamento:** Baseado em **Kotlin Coroutines** e **Flow**, ele armazena dados de forma totalmente assíncrona, consistente e transacional.
    
- **Tipos:**
    
    - **Preferences DataStore:** Similar às SharedPreferences (chave-valor).
        
    - **Proto DataStore:** Armazena objetos customizados usando _Protocol Buffers_ (mais rápido e tipado).
        
- **Cenário de uso:** Substituição das SharedPreferences em apps novos que exigem alta performance e segurança contra corrupção de dados.
    

---

## Resumo de Escolha Técnica:

|**Tipo de Dado**|**Volume**|**Recomendação**|
|---|---|---|
|Configurações simples|Baixo|**SharedPreferences** ou **DataStore**|
|Documentos/Mídia|Alto|**External Storage** (MediaStore)|
|Dados Relacionais|Médio/Alto|**Room (SQLite)**|
|Cache temporário|Médio|**Internal Storage** (Cache folder)|

**Gostaria que eu explicasse como implementar o código para salvar um valor simples usando SharedPreferences ou prefere ver como o Room organiza as tabelas?**