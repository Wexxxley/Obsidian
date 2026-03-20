

---

O componente permite que o usuário selecione um item de uma lista suspensa para realizar ações ou preencher campos. O menu não é um componente único, mas uma combinação de elementos que trabalham juntos:

- **Box:** Utilizado como contêiner principal.
- **Row/Text/Image:** Servem como o "gatilho" visual que o usuário clica para abrir a lista.
- **DropDownMenu:** O componente que contém a lista suspensa.
- **DropdownMenuItem:** Cada opção individual dentro do menu.

O componente depende de dois estados principais para funcionar:
- **expanded (Boolean):** Controla a visibilidade do menu.
- **onDismissRequest:** Um _callback_ acionado quando o usuário clica fora do menu ou pressiona o botão voltar. 

## 3. Gerenciamento de Estado e Dinamismo

Para evitar código repetitivo e complexo, o instrutor utiliza uma abordagem baseada em listas e índices:

- **Lista de Itens:** Uma `listOf` contendo as strings (ex: nomes de países).
    
- **Estado da Posição:** Uma variável `itemPosition` (Int) criada com `remember { mutableStateOf(0) }` para armazenar o índice do item selecionado.
    
- **Loop forEach:** O menu percorre a lista de países e cria um `DropdownMenuItem` para cada um automaticamente.
    

## 4. Integração com o arquivo `strings.xml`

Uma prática de organização recomendada na aula é mover a lista de dados para os recursos do Android:

- **string-array:** Criado no arquivo `res/values/strings.xml`. Isso separa os dados da lógica do código.
    
- **stringArrayResource:** Função utilizada no Kotlin para recuperar essa lista: `stringArrayResource(R.array.country_list)`.
    

![580](../../attachments/Pasted%20image%2020260320083512.png)
![300](../../attachments/dropdown.gif)


- **Rolagem Automática:** Se a lista for muito longa, o DropdownMenu cria automaticamente uma barra de rolagem interna.
