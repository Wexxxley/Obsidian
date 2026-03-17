
#Concluded 

---
### 1. Arquivos iniciais
![350](../attachments/Pasted%20image%2020260316081028.png)
1. **manifest**: O metadado do sistema. Ele define o pacote da aplicação, declara as permissões necessárias e etc...
2. **MainActivity**: classe controladora da tela principal. Ela é responsável por gerenciar o ciclo de vida da interface (instanciação, pausa, destruição).
3. **strings.xml:** Tabela de mapeamento de constantes do tipo `String`. Serve para centralizar textos, evitar o uso de strings literais no código e facilitar a internacionalização.
4. **colors.xml:** Permite a manutenção global da paleta de cores do app.
5. **exampleUnitTest e exampleInstrumentedTest:**
	- **Unit Test:** Testes que rodam na máquina de desenvolvimento. Servem para testar lógica pura que não depende de componentes do Android.
	- **Instrumented Test**: Testes que rodam em um dispositivo real ou emulador. Servem para testar integração com a interface ou funcionalidades de hardware.	    

---
### **2. Hierarquia de Classes**

Toda a interface do Android é construída como uma **árvore de componentes**. 
#### **1. View**
É a classe base para todos os componentes visuais. Tecnicamente, ela ocupa uma área retangular na tela e é responsável pelo desenho e pelo tratamento de eventos.

- **Exemplos:**    
    - `TextView`: Exibição de texto.
    - `Button`
    - `ImageView`
    - `EditText`: Input de dados via teclado.
#### **2. ViewGroup**
A classe ViewGroup é uma subclasse de View. Ela é uma classe abstrata que pode conter filhos. Atua como um gerenciador de layout. Ela não desenha conteúdo próprio, mas decide o tamanho e a posição de cada um dos seus elementos filhos.
    
- **Exemplos:**
    - `LinearLayout:` Organiza os filhos em uma única direção (horizontal ou vertical).
    - `ConstraintLayout`: Posiciona elementos através de restrições relativas entre eles ou com o pai.

Existem duas formas de instanciar esses objetos:
1. **Via XML:** Você define a hierarquia em arquivos .xml.
2. **Via Código:** Você instancia os objetos manualmente no seu arquivo java ou kotlin

![](../attachments/Pasted%20image%2020260316093445.png)

---
### 3. Padrões de escala

![](../attachments/Pasted%20image%2020260316093727.png)

