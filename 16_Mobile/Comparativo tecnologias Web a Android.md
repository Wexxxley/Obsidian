

---
### **1. React (Web)**

O React é uma biblioteca JavaScript, desenvolvida pela Meta, focada na criação de interfaces de usuário para aplicações web.

- **Paradigma Declarativo:** Diferente do modelo imperativo, no React você descreve o estado da interface e a biblioteca se encarrega de atualizar os elementos necessários.
- **Virtual DOM:** O React utiliza uma representação na memória do DOM real. Quando ocorre uma mudança de estado, ele compara o Virtual DOM com a versão anterior e aplica apenas as alterações mínimas necessárias no navegador.
- **Componentes:** A interface é dividida em pequenas peças independentes e reutilizáveis, que facilitam a manutenção e a escalabilidade de sistemas complexos.

---
### **2. Jetpack Compose (Android Nativo)**

O Jetpack Compose é o kit de ferramentas moderno do Google para construir UI nativa no Android, substituindo o antigo sistema de layouts em XML.

- **Nativo:** Ele é construído inteiramente em Kotlin. Ao contrário de tecnologias híbridas, o Compose interage diretamente com as APIs do SO Android.
- **Recomposition:** É o processo análogo ao _re-render_ do React. Quando os dados de entrada de uma função `@Composable` mudam, o framework executa novamente apenas as funções que dependem daqueles dados, ignorando as partes da UI que não sofreram alteração.

---
### **3. Ionic (Web e Mobile)**

O Ionic é um framework que permite o desenvolvimento de aplicativos multiplataforma (iOS, Android e Web) utilizando tecnologias web (HTML, CSS e JavaScript).

- **WebView:** Diferente do Jetpack Compose, um aplicativo Ionic não é "nativo" no sentido de renderização. Ele roda dentro de uma **WebView** (um navegador interno simplificado) dentro do aplicativo móvel.
- **Capacitor:** O Ionic utiliza o Capacitor como uma camada de ponte. Isso permite que o código JS acesse funcionalidades nativas do hardware, como câmera e GPS.
- **Agnóstico de Framework:** O Ionic pode ser utilizado com React, Angular, Vue ou até mesmo JavaScript puro. Ele fornece uma vasta biblioteca de componentes de UI que imitam visualmente o comportamento do iOS e do Android.
- **Write Once, Run Anywhere:** A principal vantagem é a economia de recursos, já que um único código-fonte atende à web e às lojas de aplicativos, embora com um custo de performance ligeiramente superior em comparação ao nativo puro.

---


### Linguagem de Programação

- **React:** JavaScript ou TypeScript.
    
- **Jetpack Compose:** Kotlin.
    
- **Ionic:** JavaScript ou TypeScript (independente de usar React, Angular ou Vue).
