

---
### **1. Application**

A classe Application é o primeiro componente que o Android inicia. Ela é o lugar ideal para manter o Singleton do Banco de Dados e do Repositório, garantindo que eles vivam enquanto o app estiver aberto.

 **by lazy:** adia a criação do objeto até o momento em que ele é solicitado pela primeira vez. Se o app abrir e não precisar do banco imediatamente, ele não gastará memória ou processamento para criá-lo.

![](../../../attachments/Pasted%20image%2020260331100237.png)
![](../../../attachments/Pasted%20image%2020260331100251.png)

---
### **2. ViewModel**

Ele atua como o "gerente" dos dados: ele não sabe como o banco de dados funciona (quem sabe é o Repository), mas ele sabe **como** e **quando** entregar esses dados para a tela.
- Se o usuário girar o celular, a `Activity` é destruída e recriada. Se os dados estivessem na Activity, eles sumiriam. O ViewModel permanece na memória durante essas mudanças, mantendo os dados intactos.    
- Ele filtra e prepara os dados do Repositório para que a UI apenas precise "ler e mostrar".


O repositório nos entrega um Flow. No Jetpack Compose, preferimos o StateFlow:
- **Flow:** Só funciona quando alguém está ouvindo. Se duas telas ouvirem, o banco de dados é consultado duas vezes.
- **StateFlow:** Ele mantém o último valor em memória. Se a tela girar, o StateFlow entrega o último valor instantaneamente, sem precisar perguntar ao banco de dados de novo.


**StateIn**:
- Usamos o `viewModelScope`. Quando o usuário sai da tela e o ViewModel é descartado, todas as buscas no banco param automaticamente.
- Usamos `SharingStarted.WhileSubscribed(5000)`. Isso significa: "Se ninguém estiver olhando para a tela por mais de 5 segundos, pare de buscar dados no banco.
- Como o banco demora alguns milissegundos para responder, o StateFlow precisa de um valor inicial (geralmente uma lista vazia).

![](../../../attachments/Pasted%20image%2020260331133114.png)
