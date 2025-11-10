

---
### C# é uma linguagem:

1. Tipada: Os  valores manipulados em c# possuem tipos e uma vez declarados não podem ser mudados.

2. Compilada: O código fonte é traduzido em linguagem de máquina por um compilador antes de ser executado.

3. Gerenciada: A execução do código é gerenciada por um ambiente de execução, o Common Language Runtime (CLR), então não precisamos lidar com a liberação de memória. 

### Dotnet

 O .NET é uma plataforma de desenvolvimento de software desenvolvida pela Microsoft. Ela fornece um ambiente de execução para a criação e execução de aplicativos Windows, web, mobile, gaming, entre outros. A seguir, está listado características do .NET:

  

1. Multi linguagens : O .NET Framework suporta várias linguagens de programação, incluindo C#, Visual Basic, F#, J# e outras linguagens .NET.

  

2. CLR (Common Language Runtime): Máquina virtual responsável pela execução dos programas escritos para a plataforma. O CLR gerencia a execução do código, incluindo compilação, carregamento, execução e descarte de recursos.

  - JIT compilation: Ele traduz o código intermediário (CIL) em código de máquina nativo no momento em que o programa é executado. Isso ajuda a melhorar o desempenho, pois o código compilado é otimizado para a plataforma específica em que está sendo executado.

 - Coletor de Lixo (Garbage Collector): responsável por gerenciar a memória alocada para os objetos durante a execução do programa. O coletor de lixo monitora os objetos alocados na memória e periodicamente libera aqueles que não são mais utilizados, recuperando a memória para uso futuro.

  

3. Suporte Multiplataforma: Originalmente, o .NET Framework era exclusivo para plataformas Windows. No entanto, com o lançamento do .NET Core (e posteriormente, .NET 5), a Microsoft expandiu o suporte do .NET para outras plataformas, como macOS e Linux. 

  
  
  

Compilação arquivo.cs

  

1. Compilador C#: O compilador C#, chamado CSC (C# Compiler), é responsável por traduzir o código fonte C# em CIL (Common Intermediate Language), que é uma linguagem de baixo nível, independente de plataforma. 

  

2. CLR (Common Language Runtime): A CLR é a máquina virtual que executa o código gerado por um compilador de linguagem .NET. Ela fornece serviços essenciais para a execução de programas.

  

3. JIT Compilation: Quando o programa é executado, o código CIL é traduzido em código de máquina específico da plataforma. O código de máquina .exe gerado é então executado pelo SO.

  
  
  
  
  

Instalações necessárias

 É necessário instalar o .NET, a linguagem c#, o compilador (CSC) e uma IDE. Com o Visual Studio é possível instalar isso tudo de uma vez. O Visual Studio é mais robusto do que o visual studio code e abrange projetos .NET, Python, C ++, entre outros.

  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

___________________________________________________________________________

## <Estrutura projeto c#

1. csproj: Ele contém informações sobre o projeto, arquivos de código-fonte, configurações de compilação, debug, versão, entre outras. 

2. Program.cs: Este é o arquivo que contém o método Main, que é o ponto de entrada do programa. É aqui que a execução do programa começa.

3. sln: Contém informações sobre agrupamentos de projetos para uma solução.

 Mais comumente usado no Visual Studio, mas com a extensão “vscode-solution” é possível ter uma interface no vscode para criação de soluções.

  

Extensões VS Code

  

Organizando soluções

 É interessante organizar sua solução antes de iniciar a codar. 

 Dentro da solução “AmbienteTeste02” existe o projeto “AmbienteTeste02”, o projeto para biblioteca “AmbienteTeste02.Common” e o arquivo .sln que faz de fato o agrupamento de projetos.

 É necessário que “AmbienteTeste02” tenha noção da existência do “common”, por isso é preciso adicionar a referência.

___________________________________________________________________________

  
  
  
  

___________________________________________________________________________

## <Contato inicial com c#

 Só lembrando que c# é apenas uma linguagem de todo o ecossistema .NET.

Namespace: É uma área de escopo que contém um conjunto de classes relacionadas. É uma prática comum organizar o código em namespaces para evitar conflitos de nome e manter a estrutura do código bem organizada.

Classe Program: A classe principal de um aplicativo de console em C# é chamada de “Program”. Esta classe contém o método “Main”.

Método Main: É por onde a execução do programa começa. O parâmetro “args” do tipo “string[]” representa os argumentos da linha de comando passados para o programa quando ele é iniciado.

  

<Escrever na tela

  - WriteLine: Pula linha no final.

  - Write: Não pula linha

  

<Declarando variável e constante

  

<Eventos temporizados

 Existe a função ‘sleep’ em ‘System.Threading’ para temporizar (em milisegundos). 

___________________________________________________________________________

___________________________________________________________________________

## <Tipos

### Tipos Primitivos/Built-in types

1.Inteiros

2.Reais

Obs: para float e decimal é necessário usar sufixos.

3.Boolean

   - bool: representa valores booleanos.  

4.Caracter 

   - char: representa um único caractere.

   - string: representa uma sequência de caracteres.

### Nullable Types

 Os nullable types são tipos que podem armazenar valores do valor especial `null`.

Para criar um tipo nullable, você deve adicionar um (?) após o tipo.

  

### Alias

 Em C#, um alias é um nome alternativo para um tipo de dado existente. Isso é útil em situações em que você precisa usar tipos com nomes longos.

Ex: Int32 -> int

Ex: System.String ->string

  
  

___________________________________________________________________________

### Conversão de tipos

1. Conversão implícita: Ocorre quando não há perda de dados ao converter de um tipo para outro. O compilador é capaz de realizar essa conversão automaticamente.

 Por exemplo, converter um int em um float.

2. Conversão explícita (casting): ocorre quando há uma possível perda de dados ao converter de um tipo para outro. Para realizar, você precisa usar um operador de cast entre parênteses com o tipo desejado.

3. Conversão por métodos auxiliares: A classe estática “Convert” fornece uma série de métodos estáticos para converter valores entre diferentes tipos de dados. 

4. TryParse: TryParse é uma maneira segura de converter um string em número. Ele é especialmente útil quando você está lidando com entrada de usuário.

___________________________________________________________________________

### Extras

-var: é uma palavra-chave usada para que o compilador infira o tipo da variável com base no valor atribuído a ela.

___________________________________________________________________________

___________________________________________________________________________

## <Leitura de dados

1. Console.ReadLine(): Lê uma linha de entrada e a retorna como uma string.

2. Como ler valores numéricos: Usa-se o TryParse para converter o retorno.

3. Console.ReadKey(): lê o próximo caractere de entrada do console e o retorna como um objeto `ConsoleKeyInfo`.

___________________________________________________________________________

## <Array

 Estrutura de dados que armazena valores do mesmo tipo e com tamanho fixo.

1. Criando array

2. Aumentando tamanho

 Na verdade esse método cria um novo array de tamanho n e copia os dados.

3. Copiando array

  

___________________________________________________________________________

___________________________________________________________________________

## <Mathematic

### Math 

Biblioteca math.

### Classe Random

 Utilizada para gerar números aleatórios. É necessário criar um gerador do tipo Random e usar next(). Neste exemplo, será gerado um número inteiro entre 1 e 9.

 Para gerar números com ponto flutuante usa-se o NextDouble(). Gera entre 0 e 1.

### Moedas

 No geral, para trabalhar com moedas é interessante utilizar o tipo decimal, visto que possui uma maior precisão.

1. Formatações

__________________________________________________________________________

__________________________________________________________________________

## <Data e hora

 Existe a struct ‘DateTime’ dentro de ‘System.Data’

  

-Inicialização: DateTime date = new DateTime(2024, 1, 2, 11, 59, 59);

-Data e hora atual: DateTime date = DateTime.now;

-Atributos:date.year, date.month. date.day, date.hour, date.minute, date.second, …

  

1. Formatações

  

2. Adicionando valores a data

__________________________________________________________________________

__________________________________________________________________________

## <Informações regionais

1. Culture Info

 Presente em System.Globalization. Encapsula informações sobre uma cultura específica, como idioma, região, formato de data e hora, formato de moeda e outras configurações culturais.

  

-Setando CultureInfo do Sistema

  

-Setando CultureInfo para determinadas informações

  

-Coletando Cultura atual

  

2. TimeZoneInfo

 É importante tomar cuidado com a CultureInfo, uma vez que por mais que, por exemplo, o usuário esteja no brasil, as informações para ele podem aparecer em outro formato, visto que o servidor onde a aplicação está hospedada pode ser de outro país. E quando você usa o CurrentCulture é utilizado a cultura da máquina, ou seja, do servidor.

 Para quem trabalha com aplicações globalizadas é interessante utilizar o horário padrão mundial, que é obtido através de “DateTime.UtcNow”. Depois é só converter para o horário do usuário. Com o TimeZoneInfo.FindSystemTimeZoneById(“id”) e depois utilizando TimeZoneInfo.ConvertTimeFromUtc(date, TimeZone)

  

3. Listar ids TimeZone

  

4. Métodos e funções importantes

___________________________________________________________________________

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

## <Trabalhando com strings

1. Interpolação/concatenação

2.Formatação numéricas interpoladas

3. Comparações

string.Contains(“text”)      -> retorna boolean

string.equals(“text”)          -> retorna boolean

string.StartsWith(“text”)  -> retorna boolean

string.EndsWith(“text”)    -> retorna boolean

4. Índices

string.IndexOf(“txt”)         -> retorna o índice da primeira ocorrência (-1 se não tiver)

string.LastIndexOf(“txt”) -> retorna o índice da última ocorrência (-1 se não tiver)

5. Mais métodos

string.insert(i, “text”)                        -> insere ‘text ’no índice ‘i’

string.remove(startindex, count)  -> remove

string.ToLower()                                 -> deixa o texto minúsculo

string.ToUpper()                                 -> Deixa o texto maiúsculo

string.replace(“text”, “newtext”)  -> Substitui todas as ocorrências

string.Trim()                                         ->remove espaços do começo e do final

string.length()                                     -> tamanho da string

string.split(“ ”)                                     -> separa as palavras com base no arg passado

6. StringBuilder

 Está no namespace System.Text e é usado para manipular eficientemente strings mutáveis. A principal vantagem do StringBuilder em comparação com string é que o StringBuilder evita a criação desnecessária de objetos de string intermediários.

___________________________________________________________________________

___________________________________________________________________________

## <Enum

 Enum, abreviação de "enumeration" é um tipo de dados em C# que nos permite definir um conjunto de constantes nomeadas e numeradas. 

___________________________________________________________________________

## <Switch case

___________________________________________________________________________

  
  
  
  

___________________________________________________________________________

## <If ternário

 O operador ternário é uma forma compacta de expressar uma condição simples.

1. Sintaxe: var tipo = (condição)? “Caso V” : ”Caso F”;

2. If ternário aninhado

___________________________________________________________________________

## <Estruturas de repetição

<For

<Foreach

<While

___________________________________________________________________________

  

___________________________________________________________________________

## <Struct

___________________________________________________________________________

## <Tipos anônimos

 Tipos anônimos permitem a criação de objetos sem a necessidade de definir explicitamente uma classe. Eles são particularmente úteis para armazenar temporariamente um conjunto de valores relacionados de maneira simples.

___________________________________________________________________________

  
  
  
  
  
  

___________________________________________________________________________

## <Tupla

 É uma estrutura de dados que permite combinar múltiplos valores em um único objeto, sem a necessidade de criar uma classe.

  

1. Declarando

  

2. Acessando

  

3. Desconstruindo

___________________________________________________________________________

## <Guid

 Em C#, um Guid (Globally Unique Identifier) é uma estrutura de dados que representa um identificador exclusivo globalmente. Geralmente, é utilizado para identificar de forma única entidades ou informações em um sistema. Um Guid é uma sequência de 32 caracteres hexadecimais. O uso de Guid é comum em cenários onde a exclusividade é crucial, como em identificadores de banco de dados, chave primária de registros, etc.

  
**