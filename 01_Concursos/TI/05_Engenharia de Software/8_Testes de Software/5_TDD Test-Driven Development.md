
#Concluded 

---

O TDD (Desenvolvimento Dirigido por Testes) é uma das práticas de programação propostas originalmente por Extreme Programming (XP) .

### **1. O ciclo TDD/Red-Green-Refactor**

1. **RED:** Comece escrevendo um teste automatizado para uma pequena funcionalidade que você deseja implementar. O objetivo é definir o que você quer implementar. 
        
2. **GREEN:** Escreva o código de produção **mais simples possível** para fazer o teste passar.
        
3. **REFACTOR:** Com o teste passando, olhe para o código e veja se há oportunidades de melhorá-lo: remover duplicação, melhorar nomes, simplificar a lógica e etc. Execute os testes novamente após a refatoração para garantir que nada foi quebrado. Após refatorar, o ciclo recomeça: escreve-se um novo teste que falha para a próxima pequena funcionalidade.

![450](../../../../attachments/Pasted%20image%2020251027144219.png)

---

### **2. Objetivos Principais do TDD:** 

TDD não é apenas sobre testar, mas também sobre design e disciplina. Seus principais objetivos são:

1. **Garantir que os Testes Sejam Escritos:** Ao tornar a escrita do teste a _primeira_ atividade, TDD evita que os testes sejam esquecidos ou deixados para depois .
    
2. **Promover Código com Alta Testabilidade:** Como o desenvolvedor escreve o teste _antes_ do código, ele naturalmente pensa em como tornar o código testável desde o início. 
    
3. **Melhorar o Design do Código:** Ao escrever o teste primeiro, o desenvolvedor se coloca na posição de _usuário_ da classe/método que será implementado. Isso o incentiva a pensar na interface da classe, buscando simplicidade, nomes claros, poucos parâmetros. 


