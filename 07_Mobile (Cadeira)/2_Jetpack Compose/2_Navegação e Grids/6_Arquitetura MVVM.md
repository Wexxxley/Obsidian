
#Concluded 

---
![](../../../attachments/Pasted%20image%2020260506152250.png)

A arquitetura **MVVM (Model-View-ViewModel)** é um padrão de projetos mobile. Seu objetivo principal é isolar a interface gráfica do usuário das regras de negócios e da lógica de acesso a dados.

### **1. UI Layer**

A UI Layer é responsável por exibir os dados do aplicativo na tela e atuar como o ponto principal de interação com o usuário. 
- **UI Elements (View):** Correspondem aos componentes visuais renderizados na tela. A função dos elementos de UI é formatar, exibir dados e capturar os eventos de entrada do usuário.
- **State Holders (ViewModel):** São os componentes responsáveis por gerenciar e manter o estado dos dados que serão exibidos pelos UI Elements. Eles processam as intenções do usuário capturadas pela View e interagem com as camadas subjacentes para atualizar as informações. A ViewModel no android é projetado para sobreviver a mudanças de configuração, preservando os dados em memória sem a necessidade de recarregá-los.
### **2. Domain Layer**

O Domain Layer é encarregado de encapsular a lógica de negócios complexa do aplicativo ou lógicas que precisam ser reutilizadas por múltiplos State Holders.

Geralmente é implementada através de classes chamadas de Use Cases. Cada Caso de Uso deve ter uma responsabilidade única e bem definida, recebendo dados das camadas inferiores, aplicando as regras matemáticas ou de negócios necessárias e retornando o resultado formatado para a UI Layer.
### **3. Data Layer**

A Data Layer corresponde ao "Model" no acrônimo MVVM. É a estrutura responsável por conter a lógica central dos dados da aplicação, determinando como eles são criados, armazenados, recuperados e atualizados.
- **Repositories:** São classes que atuam como mediadoras centralizadas para o acesso a dados. Um Repositório oculta os detalhes técnicos de como e de onde os dados são obtidos. Ele expõe métodos limpos para as camadas superiores consumirem,
- **Data Sources:** Um único Repositório pode coordenar múltiplas Fontes de Dados. Por exemplo, pode existir um Data Source remoto (que realiza requisições HTTP para uma API na internet) e um Data Source local (que realiza operações de banco de dados interno no dispositivo, como o SQLite).

