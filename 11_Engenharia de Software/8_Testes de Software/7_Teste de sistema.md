

---
- São testes que simulam o uso de um sistema por um **usuário real**, interagindo com ele através de sua interface (geralmente a interface gráfica ou interface de linha de comando) .
    
- O objetivo é validar o comportamento completo do sistema, de ponta a ponta (_end-to-end_), verificando se todas as partes integradas funcionam como esperado do ponto de vista do usuário .
    

**Características:**

- **Ponta-a-Ponta (End-to-End):** Exercitam o sistema inteiro, desde a camada de interface até as camadas de lógica de negócio e banco de dados, em um ambiente o mais próximo possível do de produção.
    
- **Mais Caros e Lentos:** Demandam maior esforço para implementação e levam mais tempo para executar do que testes de unidade ou integração .
    
- **Menos Numerosos:** Pelo seu custo e lentidão, representam a menor proporção de testes na pirâmide.
    
- **Frágeis:** Podem ser "quebradiços", pois pequenas alterações na interface do usuário (ex: mudar o nome de um botão, alterar um layout) podem quebrar o teste, mesmo que a lógica de negócio subjacente não tenha mudado.
    
- **Dificuldade de Localização de Falhas:** Quando um teste de sistema falha, pode ser mais difícil localizar a unidade de código exata que causou o problema, pois a falha pode estar em qualquer ponto da cadeia de execução (interface, lógica, banco de dados) .
    

**Exemplo 1: Teste de Sistemas Web (com Selenium)**

- **Ferramenta:** Selenium é um framework popular para automatizar testes de sistemas Web .
    
- **Como Funciona:** Permite criar programas (robôs) que controlam um navegador real (como Firefox, Chrome), simulando ações de um usuário: abrir páginas, preencher formulários, clicar em botões, e verificar (com asserts) os resultados exibidos na tela .
    
- **Exemplo de Código:** O livro mostra um exemplo de código Java usando Selenium que:
    
    1. Abre um navegador Firefox (`new FirefoxDriver()`).
        
    2. Navega para "[http://www.google.com](http://www.google.com)".
        
    3. Encontra o campo de pesquisa (pelo nome "q").
        
    4. Digita "software" no campo.
        
    5. Submete o formulário (como dar "Enter").
        
    6. Espera até que o título da página de resultados comece com "software" (com um timeout) .
        
    7. Imprime o título da página no console (para verificação).
        
    8. Fecha o navegador.
        
- **Complexidade:** Testes de interface são mais complexos de escrever do que testes de unidade (a API do Selenium é mais complexa que a do JUnit) e precisam lidar com questões como _timeouts_ (esperar a página carregar) .
    

**Exemplo 2: Teste de um Compilador**

- A interface de um compilador geralmente não é gráfica, mas sim arquivos de entrada e saída.
    
- Um teste de sistema para um compilador envolveria :
    
    1. Criar um conjunto de programas na linguagem-fonte (ex: Linguagem X) que exercitem diversos aspectos da linguagem.
        
    2. Para cada programa P, definir dados de entrada e a saída esperada (ex: uma lista de strings) .
        
    3. O teste automatizado: a. Chama o compilador C para compilar o programa P. b. Executa o resultado da compilação com os dados de entrada definidos. c. Verifica (com `assert`) se a saída produzida é idêntica à saída esperada.
        
- Este é um teste de sistema porque exercita todas as funcionalidades do compilador (análise léxica, sintática, semântica, geração de código) de forma integrada.