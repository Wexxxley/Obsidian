

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