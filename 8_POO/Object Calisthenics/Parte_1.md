A principal motivação para o **Object Calisthenics** é aplicar alguns princípios do **SOLID.** Basicamente são um conjunto de **boas práticas** para aumentar a qualidade do seu código. O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código orientado a objetos de melhor qualidade.
#### **1. Use apenas um nível de indentação por método**
- **Por quê?** Força a extração de lógica complexa para novos métodos menores e com nomes claros. Isso resulta em funções focadas e mais fáceis de ler.
#### **2. Evite a palavra-chave `else`**
 - **Por quê?** Incentiva o uso de padrões como **retornos antecipados**. O código resultante geralmente é mais linear e direto ao ponto.

##### **Exemplos abrangendo regras 1 e 2:**

Código antes
```java
public boolean podeAcessarAntes(Usuario usuario) {
    if (usuario != null) {
        if (usuario.getIdade() >= 18) {
            if (usuario.isAtivo()) {
                return true;
            } else {
                // else aninhado
                System.out.println("Erro: Usuário inativo.");
                return false;
            }
        } else {
            // else aninhado
            System.out.println("Erro: Usuário menor de idade.");
            return false;
        }
    } else {
        // else principal
        System.out.println("Erro: Usuário não encontrado.");
        return false;
    }
}
```

Código refatorado
```java
public boolean podeAcessarDepois(Usuario usuario) {
    if (usuario == null) {
        System.out.println("Erro: Usuário não encontrado.");
        return false;
    }

    if (usuario.getIdade() < 18) {
        System.out.println("Erro: Usuário menor de idade.");
        return false;
    }

    if (!usuario.isAtivo()) {
        System.out.println("Erro: Usuário inativo.");
        return false;
    }

    // Se passou por todas as verificações, o acesso é permitido.
    return true;
}
```