

---
#### **1. Abertura**
**(Tempo estimado: 1 min)**

- "Olá a todos. Me chamo Wesley e, juntamente com meu colega George, desenvolvemos o projeo intitulado **'Ferramenta para Extração e Visualização de Dados Parlamentares'**.

- Este projeto apresenta uma prova de conceito (POC) de uma arquitetura de software integrada, distribuída como um aplicativo, projetada para simplificar a coleta, tratamento, armazenamento e a análise de dados abertos da Câmara dos Deputados do Brasil.
#### **2. A Problematização**
**(Tempo estimado: 2 min)**

- Vivemos hoje numa era de 'dilúvio de dados'. Embora a transparência governamental seja essencial e existam portais como o da Câmara dos Deputados que oferecem um volume massivo de informações, existem barreiras:
    
    - A mera existência do dado não garante transparência.
    - Para o cidadão comum, e até para jornalistas, os dados estão fragmentados em formatos heterogêneos como JSON, XML e CSV.
    - As infomações estão separadas em locais e com métodos de acesso diferentes.
    - Sem conhecimento em programação para consumir APIs complexas, o cidadão não consegue transformar esses dados em informação útil. É aqui que nosso trabalho atua.

#### **3. Simplificação e Automação**
**(Tempo estimado: 1 min)**

- Nós criamos uma ferramenta que automatiza o processo de ETL (_Extract, Transform, Load_), entregando ao usuário final gráficos prontos e, ao pesquisador, um banco de dados limpo e estruturado."

#### **4. Demonstração Prática**
**(Tempo estimado: 2 min)**

- Vou demonstrar a execução da ferramenta agora. Como se trata de uma Prova de Conceito, focamos na facilidade de distribuição. O usuário seleciona o ano desejado — vamos usar 2012 como exemplo — e inicia o processamento.

#### **5. Detalhes da Arquitetura**
**(Tempo estimado: 1.5 min)**

1. Temos um **Módulo de Coleta** em Python que faz o trabalho pesado de buscar dados na API da Câmara.
	
2. Esses dados são limpos e salvos em um banco **SQLite** local. Escolhemos SQLite pela portabilidade, pois não exige que o usuário instale um servidor de banco de dados complexo.
	
3. Por fim, uma API Local leve serve esses dados para a interface que acabamos de ver. Essa separação permite que, no futuro, a interface mude sem quebrar a coleta de dados.


#### **6. Modelo de Dados**
**(Tempo estimado: 1 min)**

- **Visual:** Diagrama do Banco (Figura 2) ou Print do Gráfico (Figura 4).
    
- **Fala Sugerida:** "O resultado para o cidadão comum são visualizações imediatas, como o gráfico de 'Top Deputados por Gasto' que vimos18181818.
    
- Porém, o maior valor para pesquisadores e jornalistas está no **Banco de Dados**. Entregamos tabelas relacionais prontas — ligando Deputados, Partidos, Despesas e Votos 191919191919191919— eliminando a etapa custosa de limpeza de dados para quem quer fazer análises mais profundas com ferramentas de Business Intelligence (BI)20202020."
    

#### **Slide 7: Conclusão e Trabalhos Futuros**

**(Tempo estimado: 1.5 min)**

- **Fala Sugerida:** "Concluindo, esta Prova de Conceito valida que é possível encapsular a engenharia de dados em uma ferramenta acessível21.
    
- Nós reduzimos a barreira técnica inicial para o controle social22.
    
- **Limitações e Futuro:** Como limitações, o uso do SQLite pode ser um gargalo para volumes massivos de dados históricos23.
    
- Como trabalhos futuros, planejamos conectar essa API local diretamente a ferramentas de BI (como PowerBI ou Metabase), permitindo que o usuário crie seus próprios relatórios dinâmicos, superando a rigidez do dashboard estático atual24.
    
- Obrigado pela atenção."
    

---

### Dicas Adicionais para a Apresentação:

1. **Durante a Demo:** Se o processamento demorar um pouco mais que o esperado (falha de rede, etc.), tenha o "Slide 5 (Arquitetura)" na manga para explicar _enquanto_ o software roda, para não ficar em silêncio.
    
2. **Sobre o Público:** Lembre-se que é um evento universitário. Enfatize que o código é aberto (Open Source) e está no GitHub, convidando a colaboração acadêmica25252525.
    
3. **Termos Técnicos:** Ao falar "ETL" ou "Idempotência", explique brevemente ou use o contexto para deixar claro, garantindo que todos na sala entendam, mesmo quem não é de Computação.