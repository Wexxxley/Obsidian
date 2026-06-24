

---

### 1. Formas de armazenamento usadas

1. **Banco de Dados Relacional (Room)**: O Room é uma camada de abstração (Object-Relational Mapping) sobre o SQLite. Mapeia objetos Kotlin para tabelas do banco.
	- Base do sistema, responsável por armazenar todos os dados estruturados do negócio.
	- O projeto utiliza DAOs (Data Access Objects) para operações de leitura, escrita e exclusão.

2. **Preferências do Usuário (Jetpack DataStore)**: Chave valor, assíncrono.
	- UserPreferences Data class que modela os dados salvos.
	- UserPreferencesRepository Centraliza a lógica de leitura e escrita.
		![](../../attachments/Pasted%20image%2020260624134019.png)

  3. **Sistema de Arquivos Interno**: Usado para armazenar arquivos binários. Como imagens de perfil, produtos e serviços. O banco de dados armazena apenas o caminho do arquivo.
	- API de armazenamento interno do Android (context.filesDir).
	- Centralizado no objeto ImageUtils.kt. ImageUtils gerencia a compressão, salvamento, criação de nomes únicos (UUID) e deleção de arquivos, garantindo que o armazenamento interno seja mantido limpo.

**AppDatabase**
![400](../../attachments/Pasted%20image%2020260624131936.png)
**from**: Recebem o Enum, extrai a string e armazena no db
**to:** Recupera o texto armazenado. Utiliza a valueOf para instanciar o enum na memória.

![400](../../attachments/Pasted%20image%2020260624133059.png)
- **companion object** implementa o padrão **Singleton**. Garante que apenas uma única instância do banco de dados (AppDatabase) seja criada e mantida na memória durante todo o ciclo de vida do aplicativo.
- O bloco **synchronized(this)** atua como um mecanismo de bloqueio para garantir segurança em operações simultâneas. 
