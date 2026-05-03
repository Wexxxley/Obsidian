
#Concluded 

___

O HTML é uma linguagem semântica, ou seja, ela não se preocupa com as formas, mas com o sentido, com o conteúdo. E qualquer tag que seja usado exclusivamente pela forma está desatualizada e entrando em desuso.

Antes existiam somente duas tags de agrupamento, a **div** e a **span**. Com o html5 surgiram as tags semânticas que estão sendo utilizadas para dividir as partes do documento html e ajudar os mecanismos de busca.

- **header**: É o cabeçalho, pode ser o cabeçalho principal do site ou de uma seção. Geralmente, o cabeçalho contém logotipos, títulos, menus de navegação.

- **nav**: Utilizada para criar um bloco de navegação, geralmente contendo links para diferentes páginas ou seções do site.

- **main**: Usada para representar o conteúdo principal. Deve ser usada uma única vez em um doc HTML e engloba o conteúdo central, excluindo cabeçalhos, rodapés, barras laterais e outros elementos secundários.

- **section**: É usada para separar e organizar o conteúdo em diferentes seções, tornando-o mais claro e significativo para os leitores e mecanismos de busca.

- **article**: É usado para representar um conteúdo independente e autossuficiente, como uma postagem de blog, uma notícia, um artigo ou qualquer outro conteúdo que possa ser distribuído separadamente do restante da página ou do site.

- **figure**: É usada para representar conteúdo multimídia, como imagens, ilustrações, gráficos e vídeos.

- **aside**: É usado para representar um conteúdo tangencial ao conteúdo principal. Frequentemente utilizado para incluir barras laterais, widgets, anúncios, links.

- **footer**: É usada para representar o rodapé de uma página da web ou de uma seção específica do documento. O rodapé normalmente contém informações de contato, links úteis, direitos autorais, créditos, etc.

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exemplo de HTML Semântico</title>
</head>
<body>

    <header>
        <h1>Portal de Tecnologia</h1>
        <nav>
            <ul>
                <li><a href="#home">Início</a></li>
                <li><a href="#noticias">Notícias</a></li>
                <li><a href="#contato">Contato</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section id="noticias">
            <h2>Destaques do Dia</h2>
            
            <article>
                <h3>O Avanço da Inteligência Artificial</h3>
                <p>A inteligência artificial tem transformado diversos setores da indústria global.</p>
                
                <figure>
                    <img src="https://via.placeholder.com/300" alt="Representação de circuitos integrados">
                    <figcaption>Figura 1: Ilustração de processamento de dados.</figcaption>
                </figure>
            </article>

            <article>
                <h3>Novas Energias Renováveis</h3>
                <p>Pesquisadores descobrem métodos mais eficientes para a captação de energia solar.</p>
            </article>
        </section>

        <aside>
            <h4>Conteúdo Relacionado</h4>
            <p>Confira também nossa newsletter semanal sobre inovações tecnológicas.</p>
            <ul>
                <li><a href="#">Link externo 1</a></li>
                <li><a href="#">Link externo 2</a></li>
            </ul>
        </aside>
    </main>

    <footer>
        <p>&copy; 2026 Portal de Tecnologia. Todos os direitos reservados.</p>
        <p>Contato: info@tecnologiaexemplo.com</p>
    </footer>

</body>
</html>
```

