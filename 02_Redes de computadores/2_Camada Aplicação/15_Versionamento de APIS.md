
#Concluded 

---
O versionamento de APIs é a prática de gerenciar de maneira transparente as alterações em sua API. Você está entregando dados para o público de algum modo e precisa comunicar quando muda a maneira como os dados são entregues.

**Contrato de dados:** Um contrato de dados é um acordo sobre o modo e o conteúdo geral dos dados de solicitação e/ou resposta.
```json
{
  "dados": [
    {
      "id": 1,
      "nome": "Produto 1"
    },
    {
      "id": 2,
      "nome": "Produto 2"
    }
  ]
}
```
- A propriedade `dados` poderia ter sido chamada de `body`. A propriedade `id` de cada produto, por sua vez, poderia ter sido um GUID em vez de um número inteiro. 

- Essas mudanças aparentemente sutis teriam criado um acordo diferente, um contrato diferente, em relação ao "formato" no qual os dados são apresentados. 

### **Gerenciamento de alterações da API**

Nunca é sábio forçar os consumidores de uma API a fazer uma mudança. Se você precisar fazer uma alteração problemática, use o versionamento para isso. 

Primeiramente, vamos discutir brevemente como evitar mudanças problemáticas. Poderíamos chamar isso de gerenciamento de alterações da API. O gerenciamento eficaz de alterações no contexto de uma API é resumido pelos seguintes princípios:

- Manter o suporte a propriedades/_endpoints_ existentes
- Adicionar novas propriedades/_endpoints_ em vez de alterar os existentes
- Tornar obsoletos propriedades/_endpoints_ com muito cuidado

Esses princípios farão uma grande diferença na navegação pelas alterações em sua API sem a necessidade de lançar uma nova versão. No entanto, se você precisar de um novo contrato de dados, precisará de uma nova versão do seu _endpoint_. Então, você precisará comunicar isso ao público de alguma maneira.

---
#### **A. Versionamento por URL**

Ex: `http://api.exemplo.com/v1/produtos`

- **Vantagens:**
    - Explícito e Visível
    - Você pode copiar e colar o link no navegador e ele funciona. Ótima testabilidade. 
    
- **Desvantagens:**
    - **Poluição de Rotas:** Você acaba tendo que duplicar muitos códigos ou rotas no servidor para manter a `/v1` e a `/v2` rodando ao mesmo tempo.
    - **Violação Semântica:** Teoricamente, a URL deveria representar o recurso. Ao mudar a URL, parece que é um produto diferente, quando na verdade é o mesmo.
        

---
#### **B. Versionamento por Parâmetros de Consulta**

Ex: `http://api.exemplo.com/produtos?versao=1`

- **Vantagens:**
    - URL Base Preservada
    - É muito fácil configurar o sistema para assumir a versão mais recente se o usuário esquecer de enviar o parâmetro `?versao=`.
        
- **Desvantagens:**
    - **Problemas de Cache:** Alguns sistemas de cache ignoram tudo que vem depois do `?`, podendo entregar a versão errada para o usuário.
    - **Poluição Visual:** Se sua API tiver muitos filtros, a URL fica gigante e confusa.

---
#### **C. Versionamento por Cabeçalho**

Ex: `Accept: version=1.0` (Isso vai "escondido" nos metadados da requisição)

- **Vantagens:**    
    - URLs Limpas
    - A URL diz onde está o dado, o cabeçalho diz como você quer o dado. É considerado o jeito mais "elegante" arquiteturalmente.
        
- **Desvantagens:**
    - **Difícil de Compartilhar:** Você não pode mandar o link para um amigo abrir no navegador, pois ele não conseguirá configurar o cabeçalho facilmente.
    - **Complexidade:** Exige mais conhecimento técnico tanto de quem cria quanto de quem consome a API.
        

---
#### **D. Integração de Tipos**

A Integração propõe usar o versionamento de URL para o mudanças grandes e outro método (Query ou Header) para mudanças pequenas.

`http://api.exemplo.com/v1/produtos?versao=2`

- **Na URL:** Refere-se à versão da plataforma.

- **No Parâmetro:** Refere-se à versão do recurs.

