
---
DTO é um padrão de design utilizado para transferir dados entre diferentes camadas de uma aplicação. O principal objetivo de um DTO é encapsular os dados e reduzir a complexidade das interações.

### **1. Exemplo de DTO**
 Considere essa classe anêmica de curso. Nele temos diversas propriedades, mas nem todas devem ser mostradas a um cliente.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcw_u4B-OoGrAIUQjKhLFDjVTPNyddrFzNbxszX9im_LWdwElhspLx3yA6YE0Jgya5BONWWkIeKlCXFZ9hkqUzQpZthNARBjbh4htGcm24uuIGCrGy43PCya71k4Q6NEn8SqoBDf_RYfXNXfOOJVMD23qSY?key=SZHaDLu24DLXyFgiFaRNLA)

Portanto, foi criada a classe CursoDTO. Nela temos só as informações mais importantes.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfvJwX-LjW6aHZfYcTxWbwQErRNaPR2iqhf2Fj8CoOA-cC8rsWlSubqZYVmhckbmRxYzCh3acgy10MkxwbGHoiqpC7Hh8Y1UD_76zG-kipprDtMtolR3g46mn2z96ZHpLektpkjnn8Z_XodH7PCH26NQt0?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **2. Mapeamento automático**
Para passar de um curso para um cursoDTO você pode fazer isso manualmente, mas adiciona código excessivo a seus métodos. Assim sendo, é interessante ter possibilidades de mapeamento automático. Duas alternativas são interessantes:
1. Criar uma classe estática com métodos de extensão para fazer a conversão.
2. Utilizar o pacote AutoMapper

No geral é mais simples utilizar o AutoMapper, mas dependendo da complexidade dos seus modelos, a abordagem por método de extensão pode ser recomendada.

#### **2.1 AutoMapper**
1. Instale o pacote com : ``dotnet add package AutoMapper``
2. Crie uma classe Responsável por mapear as entidades. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6q_EGNJ-kqVV9ioaPbnM5VYPQCZ1KgCtvKoEZsmWOSwLMRXkiEREQgf6cOCdbTgQ6o441OHGtJTXkpaUiWF9TaaJlj5iUtSxVe4Q0zTWsDOln59VtCgbFNQeCuTUeAEiC8Fu_gkhN-rURaLBwVQ4QR1iO?key=SZHaDLu24DLXyFgiFaRNLA)
Com ReverseMap CursoRequest pode ser mapeado para Curso.
3. Adicione ao contêiner.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc8mtqaPxKHNnL5xiPFJJ0ny-v52u2HiEnS_FG6MUAC5yruujXarklxzF8KhVEpUUFmnfP2jZUn7p2c1sxw5GHpUWJnToe3ZrmkCHW6PuXbgLtdGR3UoI621mUpmHV5GndsH2BRiESXpYqMG0hX1kVsYIJP?key=SZHaDLu24DLXyFgiFaRNLA)
4. Faça a injeção de dependência na Controller.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfW85l_qpjEfKDq2ZhdHN01le2ODsYWN_CC599gnHFZkNntNzE0d0aNm0_oymMBBBTD5xKcjLiQejGqQjGP1MttSCtEfvq3xBdMrDJMf5KpX2VjqWbNyxY5kX8BKAuoUmSnPF3VZI73JtCfRv__1uRu8RL4?key=SZHaDLu24DLXyFgiFaRNLA)
5. Nova abordagem x Antiga abordagem.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKOgn6QL0pX4BU_7CB0Dai9bcu7Tb0PYmX-MH8alnpkiFAKJzbx5xcszP45boDPPSklKDTh0d9u4grPeKEAdmYIv8ZwOdWB_h4wIMDqfvYzMp-7oCS095CjpMSTDgctGwmNtmb8IkDolkia_oMjd_DM9ME?key=SZHaDLu24DLXyFgiFaRNLA)

#### **2.2 Criar sua própria classe** 