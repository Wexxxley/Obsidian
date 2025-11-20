

---

A tela inical deve ter o logo e um campo para inserir a url do video. apos prosessamento parece a outra tela com o video e trduçoes.

eu como usuario quero assistir o video do youtube e, ao mesmo tempo quero que tenha as legendas bilingues a baixo. Se o video for em ingles, vai ter a legenda em ingles e em ptbr.

eu como usuario quero conseguir copiar qualquer uma das legendas que estiver passando naquele momento para inserir em anotaçoes para estudo.

eu como user quero exposrtar uma das legendas ou as duas para markdown para estudo.

Se eu clico em uma palavra e dps clico em Study, o video reduz e abre ao lado uma tela de uma llm como gemini com a explicação da palavra e varios exemplos de frases com o uso da palavra.

Se eu clico em uma frase e dps clico em Study, o video reduz e abre ao lado uma tela de uma llm como gemini com a explicação da frase.

Nessas explicaçoes eu quero ter a possibilidade escolher em qual lingua vai ser a explicação, se sou avançado quero tudo em ingles, e as frases vem em ingles e em ptbr para comparar. se sou novato quero que a explicação venha em ptbr e as frases em ingles + ptbr. 

Dessas explicações quero copiar partes especificas.

o user precisa fornecer a chave da api llm.

vamos começar com o basico, entao só a legenda na lingua original do video e em ptbr.

---
## Requisitos de Projeto: Language Study Tool (Amethyst)

O objetivo principal é criar um ambiente de estudo imersivo, sincronizado e assistido por IA para vídeos do YouTube.

### Módulo Básico (MVP - Foco no Front-End e Transcrição)

Esta fase inicial garante a fundação visual e a utilidade central do projeto.

|**ID**|**Requisito (O que o Usuário Quer)**|**Funcionalidade Técnica**|**Destaque no Currículo**|
|---|---|---|---|
|**B.1**|**Página Inicial:** Inserir a URL do vídeo para processamento.|**Front-end:** Layout simples com input de URL e botão de submissão.|UX simples e claro.|
|**B.2**|**Visualização de Estudo:** Assistir ao vídeo com legendas.|**Front-end:** Layout de duas colunas (Vídeo + Área de Legendas). **YouTube Iframe API** para _embed_ do vídeo.|Integração de mídia.|
|**B.3**|**Legendas Bilíngues:** Exibir a legenda no idioma original do vídeo e a tradução (PT-BR).|**Back-end:** Serviço para buscar a transcrição do vídeo (com _timestamps_). **Back-end/API de Tradução** para gerar a versão PT-BR.|Uso de API de terceiros.|
|**B.4**|**Sincronização:** As legendas devem ser destacadas e mudar automaticamente conforme o vídeo avança.|**Front-end:** Lógica para monitorar o `currentTime` do vídeo e aplicar **CSS _highlight_** na frase correspondente.|Sincronização de Interface.|
|**B.5**|**Cópia Rápida:** Copiar a legenda que está sendo exibida para anotações.|**Front-end:** Botão/ícone de "copiar" que usa o `navigator.clipboard.writeText` para copiar a frase inteira (Original ou PT-BR).|Interatividade e UX.|
|**B.6**|**Exportação Markdown:** Exportar a transcrição completa (Original, PT-BR, ou Bilíngue) para estudo.|**Front-end & Back-end:** Gerar uma estrutura de dados com todas as frases/traduções e formatá-la em um arquivo `.md` para download/cópia.|Geração de arquivos.|

### Módulo Intermediário (Autenticação e LLM Setup)

Esta fase adiciona a segurança e prepara o _engine_ de IA.

|**ID**|**Requisito (O que o Usuário Quer)**|**Funcionalidade Técnica**|**Destaque no Currículo**|
|---|---|---|---|
|**I.1**|**Autenticação de Chave:** O usuário deve fornecer sua própria chave da API da LLM (ex: Gemini/Google Translate).|**Back-end & DB:** Formulário de configuração de chave. Armazenamento da chave em um **banco de dados seguro** (criptografado) associado ao perfil do usuário.|Segurança e Gerenciamento de Dados.|
|**I.2**|**Modo de Estudo (Study Mode) - Trigger:** Selecionar uma palavra ou frase para análise.|**Front-end:** Lógica de manipulação de texto para detectar o clique ou seleção do mouse em palavras/frases na área de legenda.|Manipulação avançada do DOM.|
|**I.3**|**Layout Adaptativo:** Ao iniciar o modo Study, o vídeo deve reduzir e um painel de explicação deve abrir ao lado.|**Front-end:** CSS/State management para transição do layout (ex: 70/30 para 30/70).|Design Responsivo e Dinâmico.|

### Módulo Avançado (Integração e Flexibilidade da LLM)

Esta fase implementa o poder da IA e a customização avançada.

|**ID**|**Requisito (O que o Usuário Quer)**|**Funcionalidade Técnica**|**Destaque no Currículo**|
|---|---|---|---|
|**A.1**|**Explicação de PALAVRA:** Obter significado e exemplos de uso.|**Back-end & LLM:** Enviar a palavra + frase de contexto para a LLM, usando a chave do usuário (I.1). Pede à LLM que gere a explicação.|Integração de IA/LLM.|
|**A.2**|**Explicação de FRASE:** Obter explicação gramatical/cultural da frase.|**Back-end & LLM:** Enviar a frase completa para a LLM com um _prompt_ específico para análise de contexto.|Engenharia de _Prompt_ (Prompt Engineering).|
|**A.3**|**Flexibilidade de Idioma:** Escolher se a explicação da LLM será em Inglês (avançado) ou PT-BR (novato).|**Front-end:** Dropdown de preferência de idioma na tela de estudo. **Back-end & LLM:** Adicionar o idioma de saída desejado como um parâmetro no _prompt_ da LLM.|Lógica de Personalização.|
|**A.4**|**Cópia de Explicações:** Copiar partes da resposta da LLM.|**Front-end:** Tornar o painel de resposta da LLM copiável e talvez usar um ícone de cópia para blocos de texto gerados.|UX finalizada.|

---

Com este roteiro, você pode focar no Módulo Básico para ter um MVP funcional e visualmente atraente rapidamente, e depois iterar sobre as funcionalidades de IA.

**Próximo Passo:** Vamos focar no Módulo Básico. Você precisa de ajuda para escolher o **Stack Tecnológico** final (React, Node.js, etc.) para começarmos o plano de desenvolvimento?