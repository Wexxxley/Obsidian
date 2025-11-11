
#Concluded 

---

Existem duas formas principais de se conectar a um repositório no GitHub:

1. **HTTPS:** É a forma mais simples. Você usa a URL. Ao fazer `push` ou `pull`, o GitHub pedirá seu nome de usuário e senha (ou um token de acesso).
    
2. **SSH:** É um método mais seguro e conveniente. Você gera um par de "chaves" criptográficas no seu computador.    
    - A **chave pública** (`id_rsa.pub`) você envia para o GitHub e a adiciona nas suas configurações.
    - A **chave privada** (`id_rsa`) fica segura **apenas** no seu computador e você **nunca** deve compartilhá-la.

**Por que usar SSH?** A grande vantagem é que, uma vez configurado, você não precisa digitar seu usuário e senha toda vez que quiser enviar suas mudanças.

**Como configurar o SSH:**
1. **Gerar as chaves:** No seu terminal, rode o comando `ssh-keygen`. Você pode adicionar uma "passphrase" (uma senha para a chave) para segurança extra.
2. **Encontrar as chaves:** As chaves são geralmente salvas na sua pasta de usuário, em um diretório oculto chamado `.ssh`.
3. **Copie a chave PÚBLICA**
4. **Adicionar ao GitHub:**
    - Vá em "Settings" no seu perfil do GitHub.
    - Clique em "SSH and GPG Keys".
    - Clique em "New SSH Key".
    - Dê um título (ex: "Meu Notebook de Trabalho") e cole a chave pública que você copiou.

---

