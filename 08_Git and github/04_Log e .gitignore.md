
#Concluded 

---
### **1.  Histórico de commits (git log)**
Lista todos os commits feitos, começando pelo mais recente.
![](../attachments/Pasted%20image%2020251111154931.png)

- **`git log --oneline`**: Mostra uma versão compacta do seu histórico.    

---
### **2. Ignorando Arquivos (.gitignore)**

Quase todo projeto tem arquivos ou pastas que você não quer salvar no Git. O arquivo `.gitignore` é um arquivo de texto onde você lista os nomes desses arquivos e pastas.

- **Por que ignorar arquivos?**
    1. **Segurança:** Arquivos de configuração (como `.env`) que contêm senhas de banco de dados ou outras informações sensíveis nunca devem ir para o rep.
    2. **Arquivos Gerados:** Pastas que são geradas automaticamente, como `node_modules`. Elas podem ser muito grandes e não são código-fonte real.
    3. **Arquivos de Ambiente:** Arquivos específicos do seu computador ou sistema operacional que não são relevantes para outros desenvolvedores.

- **Como usar?**    
    1. Crie um arquivo na raiz do seu projeto chamado exatamente `.gitignore`.
    2. Dentro dele, liste o que você quer ignorar.
    3. Ignorar um arquivo específico: `config.php`.
    4. Ignorar uma pasta inteira: `node_modules/`.

- **.gitignore pronto**
    - Existem geradores para isso. O livro recomenda o site gitignore.io. 
    - https://www.toptal.com/developers/gitignore/

