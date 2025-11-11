
#Concluded 

---
### 1.  Histórico de commits (git log)

Lista todos os commits feitos, começando pelo mais recente.
	
- **ID do Commit (hash):** Um código longo e único para cada commit 
- **Author:** Quem fez o commit (nome e email).
- **Date:** Quando o commit foi feito.
- **Mensagem do Commit:** A descrição que você escreveu.

![](../attachments/Pasted%20image%2020251111154931.png)

- **`git log --oneline`**: Mostra uma versão compacta do seu histórico, com apenas os primeiros 7 caracteres do ID do commit e a mensagem, tudo em uma linha por commit.    

---
### 2. Ignorando Arquivos (.gitignore)

Quase todo projeto tem arquivos ou pastas que você **NÃO quer** salvar no Git. O arquivo `.gitignore` é um arquivo de texto simples onde você lista os nomes desses arquivos e pastas.

- **Por que ignorar arquivos?**
    
    1. **Segurança:** Arquivos de configuração (como `.env` ou `config.php`) que contêm senhas de banco de dados, chaves de API ou outras informações sensíveis **NUNCA** devem ir para o repositório.
        
    2. **Arquivos Gerados:** Pastas que são geradas automaticamente, como `node_modules` (em projetos Node.js). Elas podem ser muito grandes e não são código-fonte real.
        
    3. **Arquivos de Ambiente:** Arquivos específicos do seu computador ou sistema operacional que não são relevantes para outros desenvolvedores.

- **Como usar?**    
    1. Crie um arquivo na raiz do seu projeto chamado exatamente `.gitignore`.
    2. Dentro dele, liste o que você quer ignorar.
    - **Ignorar um arquivo específico:** `config.php`.
    - **Ignorar uma pasta inteira:** `node_modules/`.

- **.gitignore pronto**
    - Você não precisa criar esse arquivo do zero. Existem geradores para isso.
    - O livro recomenda o site **gitignore.io**. https://www.toptal.com/developers/gitignore/
    - Nesse site, você pode simplesmente digitar as tecnologias do seu projeto e ele gera um arquivo `.gitignore` completo e recomendado para essa combinação.