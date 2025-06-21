

---

![[Pasted image 20250621150057.png]]
- Diz ao FastAPI para expor uma rota especial para arquivos estáticos.
- Quando alguém acessa uma URL começando por `/static/img`, o FastAPI procura o arquivo correspondente dentro da pasta.
- Assim, o frontend pode acessar imagens e outros arquivos diretamente pela URL, sem precisar de um endpoint Python para cada arquivo.

**Um método coletando um imagem e armazendo no server.**
![[Pasted image 20250621150521.png]]
1. **`data: ProfFormData = Depends()`**:
    - **`data`**: Este parâmetro vai capturar os dados do formulário.
2. **`foto: UploadFile = File(...)`**:
    - **`foto`**: Este parâmetro é específico para lidar com o upload de arquivos.
    - **`UploadFile`**: É um tipo especial do FastAPI que representa o arquivo enviado. Ele permite acessar o conteúdo do arquivo, o nome, o tipo de conteúdo, etc.
    - **`File(...)`**: Indica que este parâmetro deve vir como um arquivo 

![[Pasted image 20250621150705.png]]
- **Propósito:** Prevenir colisões de nomes de arquivos e organizar o armazenamento.
- **`uuid4()`**: Gera um UUID (Universally Unique Identifier)
- **`f"{uuid4()}{file_extension}"`**: Concatena o UUID com a extensão original. Isso garante que o nome do arquivo no servidor seja praticamente único,.
- **`upload_dir`**: Constrói o caminho completo do diretório onde a imagem será salva.
- **`file_path_on_server`**: Combina o diretório de upload com o nome de arquivo único para criar o caminho completo onde o arquivo será salvo no servidor.