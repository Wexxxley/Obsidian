
#Concluded 

---

São testes que simulam o uso de um sistema por um **usuário real**, interagindo com ele através de sua interface (geralmente a interface gráfica ou interface de linha de comando) . O objetivo é validar o comportamento completo do sistema, de ponta a ponta, verificando se todas as partes integradas funcionam como esperado do ponto de vista do usuário .

- **Mais Caros e Lentos:** Demandam maior esforço para implementação e levam mais tempo para executar do que testes de unidade ou integração .
- **Menos Numerosos:** Pelo seu custo e lentidão, representam a menor proporção de testes na pirâmide.
- **Frágeis:** Podem ser "quebradiços", pois pequenas alterações na interface do usuário (ex: mudar o nome de um botão, alterar um layout) podem quebrar o teste.
- **Dificuldade de Localização de Falhas:** Quando um teste de sistema falha, pode ser mais difícil localizar a unidade de código exata que causou o problema, pois a falha pode estar em qualquer ponto da cadeia de execução (interface, lógica, banco de dados) .    

---
### **Teste de Sistemas Web (com Selenium)**

- **Ferramenta:** Selenium é um framework popular para automatizar testes de sistemas Web .
- Ele permite criar programas que controlam um navegador real, simulando ações de um usuário: abrir páginas, preencher formulários, clicar em botões e etc.
