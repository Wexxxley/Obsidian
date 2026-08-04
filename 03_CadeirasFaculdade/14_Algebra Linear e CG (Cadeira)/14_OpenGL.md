

---

O desenho de qualquer forma geométrica ocorre dentro de um bloco delimitador.

- **glBegin(...)**: Notifica a GPU que os vértices enviados a seguir devem ser interpretados como uma forma específica.
    - GL_POINTS.
    - GL_TRIANGLES.
    - GL_QUADS.
- **glEnd()**: Finaliza a transferência de dados e processa o desenho.

---
Dentro do bloco de renderização, a ordem dos comandos é fundamental para que os atributos sejam associados corretamente.
- **glNormal3f(nx, ny, nz)**: Define o vetor normal. O OpenGL associa a última normal definida a todos os vértices que vierem depois dela. Por isso, a normal deve ser declarada antes dos vértices da face.
- **glVertex3f(x, y, z)**: Define a posição espacial de um ponto. 

---
O OpenGL utiliza a ordem de definição dos vértices para distinguir a face frontal da traseira.
- **Sentido Anti-Horário**: Padrão para faces frontais. Ao olhar para a face, os vértices devem girar no sentido contrário ao relógio.

---
glTranslatef(3.0f, 2.0f, 0.0f);
glRotatef(-45.0f, 0.0f, 0.0f, 1.0f);
glScalef(-1.0f, 1.0f, 1.0f);

---

A função `gluLookAt` é uma das mais importantes. Ela recebe 9 parâmetros, divididos em três blocos de vetores $(x, y, z)$:

1. **Eye:** Onde a câmera está fisicamente.
2. **Alvo:** Para onde a lente está apontando.
3. **Vetor para Cima:** Indica qual direção é "para cima" no mundo,

```
gluLookAt(
    0.0, 0.0, 5.0,  // Posição da Câmera (Eye)
    0.0, 0.0, 0.0,  // Ponto para onde olha
    0.0, 1.0, 0.0   // Vetor Up apontando para o Y positivo
);
```