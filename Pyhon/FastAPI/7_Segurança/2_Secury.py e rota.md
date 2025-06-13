
---

``pip install pwdlib[argon2]
``
Foi criado um arquivo **security.py**
![[Pasted image 20250613141031.png]]
- Foi importado`PasswordHash` que é usada para **hashing de senhas** de forma segura.
- `PasswordHash.recommended()`esse comando cria uma instância de `PasswordHash` com **configurações recomendadas**.
- `def get_password_hash`: recebe uma senha em texto plano e retorna uma **versão criptografada (hash)** dela.
- `def verigy_password`: Compara uma senha em texto plano com a senha criptografada que foi salva anteriormente.

---
### **Sobre hash**
Hash é uma **função matemática** que transforma uma entrada em uma **sequência fixa de caracteres**, chamada de **hash**.

- **Unidirecional**: não dá para voltar ao valor original.
- **Mesmo input → mesmo output**.
- **Pequena mudança no input → hash totalmente diferente**.
- **Impossível descobrir a senha original a partir do hash** (se a função for segura).
- Normalmente usado em senhas, você **não salva a senha**, salva o **hash**. Quando o usuário digita a senha, você **gera o hash** e **compara** com o salvo.

**Mesmo os desenvolvedores** não devem ver as senhas dos usuários. Salvando apenas o **hash**, ninguém consegue saber qual é a senha original.

---
Agora no post é salvo com hash a senha. Mudanças no update também são necessárias.
![[Pasted image 20250613143949.png]]

