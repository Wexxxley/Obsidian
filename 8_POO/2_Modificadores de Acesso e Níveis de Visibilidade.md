
#Concluded 

---

Os **modificadores de acesso** são palavras-chave usadas para definir o nível de acesso a uma classe, atributo ou método. Embora existam apenas 3 modificadores explícitos (`private`, `protected`, `public`), eles dão origem a **4 níveis de visibilidade** diferentes.

| Visibilidade  | Modificador | Acessibilidade                                         |
| ------------- | ----------- | ------------------------------------------------------ |
| **Private**   | `private`   | Apenas dentro da **própria classe** onde foi definido. |
| **Default**   | (Nenhum)    | Classes dentro do mesmo **pacote**.                    |
| **Protected** | `protected` | Classes **dentro do mesmo pacote OU subclasses**       |
| **Public**    | `public`    | Qualquer classe em qualquer lugar.                     |

![](attachments/Pasted%20image%2020250917180449.png)

---
## **Encapsulamento e a Importância dos Modificadores**

Encapsulamento é o princípio de agrupar atributos e os métodos em uma única unidade (a classe), ao mesmo tempo em que se **restringe o acesso direto** a alguns dos componentes da classe. 

Pense nisso como colocar sua classe em uma interface simples, na qual você consegue ver o lado de fora e pode interagir com ele através de botões (métodos públicos), mas não vê o que está dentro (os atributos e métodos privados).

![500](attachments/1_GrarH2XqRi5iLw--RI5NMQ.png)

1. **Segurança e Consistência dos Dados** 
	- Em vez de permitir a modificação direta, você força o acesso através de métodos, onde você pode adicionar **regras de validação** antes de permitir uma mudança. 
	- Exemplo: Garantir que a idade nunca seja negativa.
        
2. **Ocultação de Implementação**
    - Se você decidir mudar algo na sua classe, algum lógica de negócio, ou até mesmo refatorar todo o código, as classes que usam sua classe não precisarão ser alteradas, desde que você mantenha a **interface pública** identica.

---
## **Getters e Setters**

- Os getters permitem que outras classes **leiam** o valor de um atributo privado. Geralmente começam com `get` seguido do nome do atributo (ex: `getNome()`).

- Permitem que outras classes **alterem** o valor de um atributo privado, mas de forma controlada. Geralmente começam com `set` seguido do nome do atributo(`setNome(String novoNome)`).
    
- **Importância:** É aqui que você aplica as **regras de validação** do encapsulamento.
    
- **Exemplo:**
    
    Java
    
    ```
    public void setIdade(int novaIdade) {
        if (novaIdade >= 0) { // Validação! O core do encapsulamento.
            this.idade = novaIdade;
        } else {
            // Lançar um erro ou ignorar a mudança
        }
    }
    ```
    

Ao usar `private` para atributos e `public` para _getters_ e _setters_, você garante que o acesso aos dados da sua classe é sempre mediado por regras, protegendo a integridade do seu objeto.


