

---

### 1. Formas de armazenamento usadas

1. **Banco de Dados Relacional (Room)**: O Room é uma camada de abstração (Object-Relational Mapping) sobre o SQLite. Mapeia objetos Kotlin para tabelas do banco.

  Esta é a base do sistema, responsável por armazenar todos os dados estruturados do negócio (entidades e seus relacionamentos).

   * Tecnologia: Jetpack Room (uma camada de abstração sobre o SQLite).
   * Nome do Banco: anotasmart_database
   * Arquivo de Configuração/Definição: app/src/main/java/com/anotasmart/database/AppDatabase.kt
   * Entidades (Tabelas):
       * Category, Product, Client, Sale, SaleItem, Installment, Expense, CartItemEntity
   * Mecanismo de Acesso: O projeto utiliza DAOs (Data Access Objects) para operações de leitura, escrita e exclusão. Cada DAO é definido em app/src/main/java/com/anotasmart/database/dao/ (ex: ProductDao.kt, SaleDao.kt).
   * Destaque: O uso de @TypeConverters em AppDatabase.kt permite armazenar tipos personalizados (como Enums) no banco de dados de forma transparente.

  ---

  2. Preferências do Usuário (Jetpack DataStore)
  Utilizado para armazenar configurações simples e pequenas informações de estado do usuário, substituindo o antigo SharedPreferences. É uma solução assíncrona e segura para threads.

   * Tecnologia: Jetpack Preferences DataStore.
   * Nome do Arquivo: user_settings (armazenado internamente pela biblioteca).
   * Arquivos Relevantes:
       * app/src/main/java/com/anotasmart/data/preferences/UserPreferencesRepository.kt: Centraliza a lógica de leitura e escrita.
       * app/src/main/java/com/anotasmart/data/preferences/UserPreferences.kt: Data class que modela os dados salvos (nome do usuário, nome da empresa, chave PIX, tema, etc.).

  ---

  3. Armazenamento de Arquivos (Sistema de Arquivos Interno)
  Utilizado para persistir arquivos binários pesados, como imagens de perfil, produtos e serviços. O banco de dados armazena apenas o caminho (path) do arquivo como uma string.

   * Tecnologia: API de armazenamento interno do Android (context.filesDir).
   * Gerenciamento: Centralizado no objeto ImageUtils.kt.
   * Arquivo de Controle: app/src/main/java/com/anotasmart/utils/ImageUtils.kt.
   * Diretórios (definidos em ImageDirectory no arquivo Enums.kt):
       * clients/ (para fotos de clientes)
       * products/ (para fotos de produtos)
       * services/ (para fotos de serviços)
       * profile/ (para foto de perfil do usuário)
   * Destaque: O utilitário ImageUtils gerencia a compressão, salvamento, criação de nomes únicos (UUID) e deleção de arquivos, garantindo que o armazenamento interno seja mantido limpo.

  ---

  Resumo para a sua apresentação

  ┌────────────────────────┬───────────────────────┬──────────────────────────────────┬──────────────────────────────┐
  │ Forma de Armazenamento │ Tecnologia            │ Finalidade                       │ Arquivo Principal            │
  ├────────────────────────┼───────────────────────┼──────────────────────────────────┼──────────────────────────────┤
  │ Banco de Dados         │ Room                  │ Dados estruturados e complexos   │ AppDatabase.kt               │
  │ Configurações          │ DataStore             │ Preferências e estado do app     │ UserPreferencesRepository.kt │
  │ Arquivos               │ Armazenamento Interno │ Imagens (Perfil, Produtos, etc.) │ ImageUtils.kt                │
  └────────────────────────┴───────────────────────┴──────────────────────────────────┴──────────────────────────────┘

  Deseja que eu aprofunde a explicação em algum desses pilares ou que eu prepare um resumo textual específico para algum slide?

