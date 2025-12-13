'''''
{
  "roadmapTitle": "DevOps Basic",
  "version": "1.0",
  "theme": "dark",
  // CAMADA 1: O VISUAL (O que aparece na Imagem 1)
  "canvas": {
    "nodes": [
      {
        "id": "node-1",
        "type": "start", // O ícone de largada
        "position": { "x": 0, "y": 0 },
        "data": { "label": "Start" }
      },
      {
        "id": "node-2",
        "type": "topic", // Um tópico clicável
        "position": { "x": 0, "y": 200 },
        "data": { 
          "label": "Fundamentos",
          "color": "#E1BEE7", // A cor roxa da imagem
          "sectionId": "section-abc" // <--- O ELO DE LIGAÇÃO
        }
      },
      {
        "id": "node-3",
        "type": "subtopic",
        "position": { "x": -200, "y": 200 },
        "data": { "label": "Sistemas Operacionais" }
      }
    ],
    "edges": [
      {
        "id": "edge-1",
        "source": "node-1",
        "target": "node-2",
        "style": "solid" // Linha sólida
      },
      {
        "id": "edge-2",
        "source": "node-3",
        "target": "node-2",
        "style": "dashed" // Linha tracejada da imagem
      }
    ]
  },

  // CAMADA 2: OS DETALHES (O que aparece na Imagem 2 quando clica)
  "sections": {
    "section-abc": { // Conteúdo do nó "Fundamentos"
      "title": "Fundamentos da Computação",
      "description": "Base teórica necessária antes de codar.",
      "groups": [
        {
          "type": "book-shelf", // O grupo pontilhado da imagem 2
          "title": "Livros que eu indico",
          "items": [
            {
              "type": "book",
              "title": "Arquitetura Limpa",
              "coverUrl": "url-da-imagem.jpg",
              "link": "amazon.com/..."
            },
            {
              "type": "book",
              "title": "Domain-Driven Design",
              "coverUrl": "url-da-imagem-2.jpg",
              "link": "amazon.com/..."
            }
          ]
        },
        {
          "type": "video-playlist",
          "title": "Cursos recomendados",
          "items": [...]
        }
      ]
    }
  }
}