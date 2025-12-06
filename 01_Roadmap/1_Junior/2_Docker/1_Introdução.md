


---

O Docker é uma plataforma para executar aplicações em unidades leves chamadas **containers**. Você junta a aplicação com todas as suas dependências, permitindo que ela rode da mesma maneira em qualquer lugar, no seu pc, no data center ou cloud.

#### 1. Construção de novas aplicações Cloud-Native

Para projetos novos, o padrão moderno é a arquitetura de **microserviços**:

- Cada componente roda em seu próprio container.
    
- Cada container pode usar a tecnologia que for melhor para ele (um em Java, outro em Node.js, banco de dados em outro).
    
- **Vantagem para o Dev:** O desenvolvedor não precisa instalar mil ferramentas na máquina. Basta ter o Docker, clonar o código e rodar um comando para subir todo o ambiente complexo.

#### 4. Inovação Técnica (Serverless e além)

O Docker permite consistência. Você pode usar containers para rodar desde monolitos .NET antigos até apps Go modernos e funções Serverless no mesmo cluster11.

- **Sobre Serverless:** Por baixo dos panos, serviços como AWS Lambda usam containers. Usar Docker permite que você rode arquiteturas Serverless no seu próprio data center ou evite ficar preso a um único provedor de nuvem, usando frameworks open source12.
    

#### 5. Transformação Digital com DevOps

Este ponto é crucial para sua área de interesse. O maior problema em TI muitas vezes não é técnico, mas cultural: a barreira entre **Dev** (desenvolvimento) e **Ops** (operações)13.

- **O problema:** Devs usam um conjunto de ferramentas; Ops usam outro. Isso gera falhas na hora do deploy.
    
- **A solução Docker:** O Docker funciona como uma linguagem comum. Ambos os times trabalham com os mesmos artefatos (`Dockerfiles` e `docker-compose.yml`). Isso facilita a automação, CI/CD e a cultura de responsabilidade compartilhada14.
    

---

### Resumo Visual da Seção 1.1

|**Cenário**|**Problema Anterior**|**Solução com Docker**|
|---|---|---|
|**Nuvem**|Escolha difícil entre VMs caras ou PaaS restritivo.|Portabilidade total com baixo custo.|
|**Legado**|Monolitos difíceis de alterar e arriscados de reescrever.|"Containerizar" o monolito e criar novos recursos como microserviços ao redor dele.|
|**Novos Apps**|Ambientes de desenvolvimento complexos e difíceis de configurar.|`git clone` + `docker run` sobe a arquitetura inteira.|
|**DevOps**|Times isolados (silos) usando ferramentas diferentes.|Uma ferramenta e formato único para Dev e Ops.|

---

Próximo passo:

Você gostaria que eu continuasse com o resumo do Capítulo 1.2 em diante, onde o livro aborda a configuração do ambiente, ou quer pular direto para o Capítulo 2, onde começamos a rodar os primeiros containers na prática?