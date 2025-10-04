
> [!NOTE]
> "Classes não devem ser forçadas a implementar métodos que não usam."
> 

O ISP diz que uma classe não deve ser forçada a implementar métodos que ela não utiliza. Isso significa que devemos criar interfaces mais específicas e enxutas, em vez de uma única interface gigante que obrigue as classes a implementar métodos irrelevantes para elas.

No exemplo temos a interface `Employee`.

```java
public interface IEmployee {
    String getName();
    void setName(String name);

    void calculateSalary();
    void calculateBenefits();
}
```

``FullTimeEmployee`` utiliza e precisa de todos os métodos estabelecidos.

``` java
public class FullTimeEmployee implements IEmployee {
    private String name;

    @Override
    public String getName() {
        return name;
    }
    @Override
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public void calculateSalary() {
        System.out.println("Calculando salário");
    }
    @Override
    public void calculateBenefits() {
        System.out.println("Calculando benefícios");
    }
}

```

``ContractEmployee`` não recebe benefícios, então não deveria ser preciso implementar o método ``calculateBenefits``.

```java
// Classe não deveria precisar de benefícios, mas é obrigada pela interface
public class ContractEmployee implements IEmployee {
    private String name;

    @Override
    public String getName() {
        return name;
    }
    @Override
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public void calculateSalary() {
        System.out.println("Calculando salário");
    }
    @Override
    public void calculateBenefits() {
        throw new UnsupportedOperationException("Sem benefícios");
    }
}
```

Para corrigir, podemos criar interfaces para FullTimeEmployee e ContractEmployee, para que essas classes não tenham que implementar métodos desnecessários.

```java

public interface IEmployee {
    String getName();
    void setName(String name);
    void calculateSalary();
}

public interface IFullTimeEmployee extends IEmployee {
    void calculateBenefits();
}

public interface IContractEmployee extends IEmployee {
}

// Classe FullTimeEmployee (CLT)
public class FullTimeEmployee implements IFullTimeEmployee {
    private String name;

    @Override
    public String getName() {
        return name;
    }
    @Override
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public void calculateSalary() {
        System.out.println("Calculando salário");
    }
    @Override
    public void calculateBenefits() {
        System.out.println("Calculando benefícios");
    }
}

// Classe ContractEmployee (terceirizado)
public class ContractEmployee implements IContractEmployee {
    private String name;

    @Override
    public String getName() {
        return name;
    }
    @Override
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public void calculateSalary() {
        System.out.println("Calculando salário");
    }
}

```