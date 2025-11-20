

---
## Requisitos de Projeto: Amethyst

O sistema **Amethyst** é uma aplicação web destinada a otimizar o estudo de idiomas a partir de vídeos do YouTube. Seu objetivo principal é sincronizar a reprodução de vídeo com legendas bilíngues e fornecer ferramentas de análise de vocabulário e contexto assistidas por Inteligência Artificial (LLM).

### 1. Requisitos Funcionais (RF)

#### Módulo 1: Gerenciamento e Visualização de Mídia

- **RF 1.1 - Entrada de URL:** O sistema **deve** apresentar uma interface de entrada para que o usuário insira a URL de um vídeo do YouTube.
    
- **RF 1.2 - Processamento e Transição:** Após a submissão da URL, o sistema **deve** processar o vídeo e transicionar para a interface de estudo, exibindo o vídeo incorporado (RF 1.3) e as legendas (RF 1.4).
    
- **RF 1.3 - Visualização de Vídeo:** O sistema **deve** incorporar e controlar a reprodução do vídeo através da **YouTube Iframe Player API**.
    
- **RF 1.4 - Geração de Legendas Bilíngues:** O sistema **deve**, para um vídeo em idioma estrangeiro, exibir a **legenda na língua original** e a **tradução automática em Português (PT-BR)**, sincronizadas com o tempo de reprodução do vídeo.
    
- **RF 1.5 - Sincronização e Destaque:** O sistema **deve** monitorar a reprodução e **destacar visualmente** a linha de legenda correspondente ao trecho sendo falado no momento.
    
#### Módulo 2: Interatividade e Exportação de Conteúdo

- **RF 2.1 - Cópia Rápida de Legenda:** O sistema **deve** permitir que o usuário copie a legenda atualmente destacada (tanto a versão original quanto a PT-BR) para a área de transferência do sistema com uma ação mínima (ex: clique em um ícone).
    
- **RF 2.2 - Exportação de Transcrição:** O sistema **deve** permitir ao usuário exportar toda a transcrição em formato **Markdown**, incluindo a opção de exportar apenas o idioma original, apenas a tradução (PT-BR), ou ambas as versões (bilíngue).
    

#### Módulo 3: Análise Assistida por IA

- **RF 3.1 - Ativação do Modo de Estudo:** O sistema **deve** permitir que o usuário ative o "Modo de Estudo" ao selecionar (clicar em) uma **palavra** ou uma **frase completa** na área de legendas.
    
- **RF 3.2 - Ajuste de Layout (Modo de Estudo):** Ao ativar o Modo de Estudo, o sistema **deve** reduzir a área de visualização do vídeo e abrir um **painel lateral de análise da LLM**.
    
- **RF 3.3 - Análise de Palavra:** Se uma palavra for selecionada, o sistema **deve** enviar a palavra e o contexto da frase completa para a LLM, solicitando uma **explicação do significado e múltiplos exemplos de uso em frases**.
    
- **RF 3.4 - Análise de Frase:** Se uma frase for selecionada, o sistema **deve** enviar a frase completa para a LLM, solicitando uma **explicação gramatical e/ou contextual/cultural**.
    
- **RF 3.5 - Escolha do Idioma de Explicação:** O sistema **deve** permitir que o usuário defina o idioma da resposta da LLM (Inglês ou PT-BR). As frases de exemplo/comparação **devem** ser fornecidas tanto no idioma original quanto em PT-BR.
    
- **RF 3.6 - Cópia de Resposta da LLM:** O sistema **deve** permitir que o usuário copie blocos de texto específicos da resposta gerada pela LLM.
    

#### Módulo 4: Autenticação e Segurança (Requisito de Alto Nível)

- **RF 4.1 - Autenticação de Chave de API:** O sistema **deve** implementar um sistema de login/registro. do google. Após o login, o usuário **deve** ser solicitado a fornecer a sua própria chave de API da LLM (ex: Gemini/Google Translate).
    
- **RF 4.2 - Armazenamento Seguro:** O sistema **deve** armazenar a chave de API fornecida pelo usuário em um banco de dados de forma **criptografada e associada ao seu perfil**.
    
- **RF 4.3 - Uso de Chave Dinâmica:** Todas as chamadas para a LLM **devem** ser feitas pelo _back-end_ (agindo como _proxy_), utilizando a chave de API recuperada do perfil do usuário autenticado.


---
### 2. Requisitos Não Funcionais (RNF)

Estes requisitos definem critérios de qualidade, desempenho e restrições técnicas.

- **RNF 3.1 - Desempenho (Sincronização):** A sincronização entre a fala do vídeo e o destaque da legenda **não deve** ter atraso perceptível (> 500ms).
    
- **RNF 3.2 - Segurança (API Key):** A chave de API do usuário **não deve** ser exposta em nenhum ponto do _front-end_ e **deve** ser armazenada de forma segura no _back-end_ com uso de criptografia robusta.
    
- **RNF 3.3 - Usabilidade (UX):** A transição do layout para o Modo de Estudo (RF 3.2) **deve** ser suave e intuitiva.
    
- **RNF 3.4 - Confiabilidade:** O sistema **deve** tratar falhas na obtenção da transcrição ou erros de chamadas à LLM, exibindo mensagens de erro claras ao usuário.
    
- **RNF 3.5 - Tecnologia:** O sistema **deve** ser construído utilizando um _framework_ de desenvolvimento web moderno (ex: React, Node.js) para garantir a modularidade e o apelo no mercado de trabalho.
    
---

## Prompt prototipo

## 🎨 Paleta de Cores do Projeto Amethyst

Com base na imagem do cristal roxo em um fundo escuro, a paleta será focada em um esquema "Dark Mode" de alta contraste e sofisticação.

|**Nome da Cor**|**Código HEX Sugerido**|**Uso Principal**|
|---|---|---|
|**Fundo Principal (Primary Background)**|`#0D0616` (Roxo Quase Preto)|Fundo da tela inteira, painéis laterais.|
|**Destaque (Amethyst Accent)**|`#9933FF` (Roxo Magenta Brilhante)|Cor primária para botões, ícones ativos, _highlights_ de texto (RF 1.5), foco.|
|**Amethyst Escuro (Dark Amethyst)**|`#4C007F`|Borda de botões inativos, divisores, cards não selecionados.|
|**Texto Principal (Primary Text)**|`#F0F0F0` (Branco Suave)|Textos longos, títulos.|
|**Texto Secundário (Secondary Text)**|`#AAAAAA`|Legendas bilíngues não ativas, descrições secundárias.|
|**Interativo (Call to Action/Botões)**|`#3366FF` (Azul Elétrico - Alternativo)|Usado para o botão "Processar URL" e links essenciais, para garantir alto contraste com o roxo.|

---

## ✏️ Prompt para Criação de Protótipo no Figma

Este _prompt_ detalha as três telas principais (Login/Home, Estudo e Modo de Estudo) e instrui o designer a usar a paleta e os requisitos formais (RFs).

**Instruções de Criação:**

> Crie um protótipo de alta fidelidade para a aplicação web "Amethyst", uma ferramenta de estudo de idiomas via YouTube, focando em um design _Dark Mode_ sofisticado e minimalista, utilizando a paleta de cores fornecida (Fundo: `#0D0616`, Destaque Principal: `#9933FF`, Texto: `#F0F0F0`). O protótipo deve ter um visual de "aplicação desktop/web profissional" (não mobile).

### 1. Tela Inicial e Autenticação (RF 1.1, RF 4.1)

- **Objetivo:** Capturar a URL e o login do usuário.
    
- **Elementos:**
    
    - **Área Central:** Campo de Input grande e centralizado para a **URL do YouTube** (RF 1.1).
        
    - **Botão Principal:** Botão `PROCESSAR VÍDEO` em cor de Destaque (`#9933FF`).
        
    - **Header:** Espaço para o logo **Amethyst** e, no canto superior direito, um botão `ENTRAR`.
        
    - **Modal de Login:** Ao clicar em `ENTRAR`, um modal simples aparece com a única opção: **"Continuar com Google"** (RF 4.1).
        
    - **Modal de Chave de API:** Após o login bem-sucedido, um modal de _onboarding_ pede a chave da LLM do usuário: **"Configure sua Chave Gemini/Google API"** (RF 4.1), com um campo de input e um botão de salvamento.
        

### 2. Tela de Estudo Principal (RF 1.3, RF 1.4, RF 1.5, RF 2.1)

- **Objetivo:** Exibir o vídeo e as legendas sincronizadas.
    
- **Layout (Duas Colunas):**
    
    - **Coluna Esquerda (Vídeo):** Container do vídeo do YouTube (RF 1.3). Deve ser dominante na tela (aprox. 60-70% da largura). Incluir controles de reprodução customizados ou simular os nativos.
        
    - **Coluna Direita (Legendas):** Uma área de texto rolável com todas as transcrições do vídeo.
        
- **Design das Legendas (RF 1.4, RF 1.5):**
    
    - Cada legenda deve aparecer em **blocos separados** com _timestamp_.
        
    - Dentro de cada bloco, deve haver duas linhas de texto: **Original (Texto Principal)** e **PT-BR (Texto Secundário/menor)**.
        
    - A legenda ativa no momento **deve ser destacada** (fundo sutil ou borda com a cor Destaque: `#9933FF`).
        
    - **Iconografia:** Ao lado de cada bloco de legenda, adicione um ícone de "Cópia" (RF 2.1) em cor secundária.
        
    - **Funcionalidade de Seleção:** Simular o clique em uma palavra e em uma frase inteira.
        

### 3. Tela Modo de Estudo Ativado (RF 3.2, RF 3.5, RF 3.6)

- **Objetivo:** Demonstrar a transição de layout e a análise da LLM.
    
- **Layout (Transição):** Mostrar a tela após a ativação do "Modo de Estudo" (RF 3.1).
    
    - **Coluna Esquerda (Vídeo Reduzido):** O container do vídeo deve ter seu tamanho **reduzido** (aprox. 30-40% da largura).
        
    - **Coluna Direita (Painel de Análise):** O painel lateral (agora principal) deve ser aberto.
        
- **Painel de Análise da LLM:**
    
    - **Controle de Idioma (RF 3.5):** No topo do painel, um _dropdown_ para o usuário escolher o idioma da explicação (`Explicação em: Inglês | Português`).
        
    - **Área de Resposta:** Exibir um **exemplo de resposta** de análise de uma palavra (RF 3.3). A resposta deve estar bem formatada, com a explicação em destaque e os exemplos de frases em listas separadas (Original e PT-BR).
        
    - **Ferramenta de Cópia (RF 3.6):** Adicionar um ícone de cópia ao lado de cada bloco de exemplo gerado pela LLM.
        
- **Header:** Adicionar um botão `EXPORTAR` no header para demonstrar o RF 2.2.