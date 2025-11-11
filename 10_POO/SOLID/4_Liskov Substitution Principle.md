
---

> [!NOTE]
> “Se S é uma subclasse de T, então objetos do tipo T podem ser substituídos por objetos do tipo S sem alterar o funcionamento do programa”.

Classes derivadas não devem invalidar funcionalidades da classe base.

No exemplo abaixo a classe abstrata Shape pode ser substituída por qualquer uma das subclasses. Elas estão implementando o método abstrato Área e todas precisam desta funcionalidade.

```java

public abstract class Shape {
    public abstract float area();
}

public class Rectangle extends Shape {
    private int width;
    private int height;

    @Override
    public float area() {
        return this.getWidth() * this.getHeight();
    }
}

public class Square extends Shape {
    private int side;

    @Override
    public float area() {
        return this.getSide() * this.getSide();
    }
}
```

O LSP evita heranças erradas que adicionam comportamentos inesperados. E se uma subclasse não consegue cumprir o contrato da classe base, a modelagem deve ser revisada.