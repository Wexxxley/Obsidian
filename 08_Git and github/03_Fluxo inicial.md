
#Concluded 

---
### **1. Inicializando um Projeto (git init)**

1. Primeiro, você cria uma pasta para o seu projeto e entra nela.
    - `mkdir novo-projeto`
    - `cd novo-projeto`
        
2. Dentro da pasta, você executa o comando git init. Esse comando "inicializa" um repositório Git vazio. Ele cria a pasta oculta `.git` .
    - `git init`
        

---
### **2. Adicionando Mudanças (git add)** 

Para dizer ao Git "comece a rastrear este arquivo" usamos o `git add`. Este processo é chamado de **Staging**.

- Para adicionar múltiplos arquivos de uma vez: 
	- `git add arquivo1.html arquivo2.css`.
        
- Para adicionar TODOS os arquivos modificados no diretório atual :
    - `git add .`

---
### **3. Salvando as Mudanças (git commit)** 

Um commit cria um checkpoint permanente do seu projeto. Você só faz o commit das mudanças que estão na área de staging.

 - `git commit -m "Sua mensagem de commit aqui"`

----
### **4. Padrão de nomeação de commits**

-  **feat:** Utilizado para a introdução de uma nova funcionalidade.
    - `feat: cria entidade Installment e gerador de parcelas`
        
- **fix:** Utilizado para a correção de um bug.
    - `fix: resolve erro no cálculo do custo médio ponderado`
        
- **refactor:** Utilizado na refatoração do codigo, focando apenas em melhorar a legibilidade ou arquitetura.
    - `refactor: move lógica de divisão de valores para a Controller`
        
- **test:** Utilizado para a criação de testes automatizados ausentes ou correção de testes.
    - `test: adiciona testes unitários para o gerador de UUIDs`
        
- **docs:** Utilizado para modificações que afetam exclusivamente a documentação.
    - `docs: atualiza documento de requisitos e diagramas do banco`
        
- **chore:** Utilizado para configurações build tools ou gerenciadores de dependências que não afetam o código de produção diretamente.
    - `chore: atualiza dependências do KSP e Room no build.gradle`
        
- **style:** Utilizado para mudanças de formatação e estilo que não afetam a lógica de execução (indentação, remoção de importações, padronização de aspas).
    - `style: padroniza nomenclatura e remove imports não utilizados nos DAOs`
        
- **perf:** Utilizado para alterações de código focadas na melhoria de desempenho.
    - `perf: implementa paginação com limit e offset na lista de clientes`
        
- **revert:** Utilizado exclusivamente para identificar a reversão de um commit anterior.
    - `revert: desfaz commit de paginação no histórico de vendas``
