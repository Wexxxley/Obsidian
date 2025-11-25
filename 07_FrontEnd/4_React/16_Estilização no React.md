
#Concluded 

---
No React, a estilização funciona de forma muito similar ao HTML padrão, mas com duas diferenças  que você precisa memorizar:

1. **clas vira className**
2. **Estilos Inline são Objetos:** Ao usar o atributo `style`, você não passa uma string (`"color: red"`), mas sim um objeto JavaScript (`{{ color: 'red' }}`).

### **1. A Orquestração dos Arquivos**

**main.jsx e index.css**: main.jsx é o ponto de entrada da aplicação React. 
- Ele importa o componente raiz (App). 
- Ele importa o estilo global (index.css).
- Ele injeta toda a aplicação na div com id root do seu HTML.
- **index.css** Contém estilos globais que o Vite injeta na página inteira. As regras aqui afetam todos os elementos da aplicação, a menos que sejam sobrescritas por estilos mais específicos.

**App.jsx App.css**: App.jsx é onde toda a sua lógica React reside, ele importa o App.css
- **App.css:** Contém estilos específicos para os componentes definidos em App.jsx. 

Para que a estilização funcione corretamente é preciso:

1. **Conectar o CSS ao Componente**
	No arquivo App.jsx, adicione a importação do CSS logo abaixo da importação do React.
	![](../../attachments/Pasted%20image%2020251125185751.png)

2. **Adicionar as Classes className no JSX**
	O CSS define classes (ex: `.container`, `.button`), mas o seu JSX atual não está usando essas classes. Você precisa adicionar o atributo `className` aos elementos correspondentes.
	![](../../attachments/Pasted%20image%2020251125190128.png)
	
3. **Limpar Conflitos do index.css**
	O arquivo `index.css` que veio com o Vite tem estilos padrão  que podem brigar com o estilo de app. Para garantir que o estilo do livro prevaleça você pode apagar tudo em index ou comentar as linhas conflitantes.