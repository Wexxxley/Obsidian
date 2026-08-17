
#Concluded 

---
### **1. Introdução às CSS**

CSS significa **Folhas de Estilo em Cascata**. Existem 3 formas de aplicar estilos:
1. **Inline**: O estilo é mudado na mesma linha do html.
2. **Internal**: O estilo é alterado na  head com a tag style.
3. **External**(recomendado: Um novo arquivo é criado.
	![](../../../attachments/Pasted%20image%2020260503120005.png)
**Atributos HTML**:  São as especificações e configurações inseridas exclusivamente dentro da tag de abertura de um elemento HTML. 
- Na tag `<img src="imagem.jpg" alt="Descrição">`, tanto src quanto alt são os atributos. 

**Declaração CSS:** São as instruções do tipo `color: x;` 
  - **Propriedade**: Refere-se à característica, como color.
- **Valor**: Estado a ser aplicado.

---
### **2. Seletores**

Os seletores são usados para selecionar os elementos html que você deseja estilizar. Podemos dividir os seletores em 4 categorias:  
1. **Seletores simples**: selecionam elementos com base no nome, id ou classe
2. **Seletores combinadores**: selecionam elementos com base em uma relação entre eles.
3. **Pseudo-classes**: selecionam elementos com base em um determinado estado  
4. **Pseudo-elementos**: selecionam e estilizam uma parte de um elemento

#### **2.1 Seletores simples**
![300](../../../attachments/Pasted%20image%2020260503120426.png)
**ID e CLASS**
- O atributo **class** é empregado para definir um conjunto de regras de estilo que pode ser compartilhado por múltiplos elementos.
- O atributoid é  utilizado para identificar de forma exclusiva um único elemento na página.
![](../../../attachments/Pasted%20image%2020260817102928.png)![](../../../attachments/Pasted%20image%2020260817102944.png)
![](../../../attachments/Pasted%20image%2020260817102259.png)


---
#### **2.2 Seletores combinadores**
![200](../../../attachments/Pasted%20image%2020250512153555.png)Todos os p dentro de uma div.
![200](../../../attachments/Pasted%20image%2020250512153702.png)Todos os p filhos diretos de uma div.
![200](../../../attachments/Pasted%20image%2020250512153719.png)Seleciona o p que vem imediatamente depois de um h1
![500](../../../attachments/Pasted%20image%2020260817103924.png)
![200](../../../attachments/Pasted%20image%2020250512153729.png)Seleciona todos os p que vem depois de um h1.

**Mais exemplos** 
![200](../../../attachments/Pasted%20image%2020250512152603.png)Aplica o estilo nos paragrafos com a classe center
![200](../../../attachments/Pasted%20image%2020250512153107.png)Aplica o estilo nos paragrafos com o id center
![200](../../../attachments/Pasted%20image%2020250512152706.png)Seletor universal
![200](../../../attachments/Pasted%20image%2020250512152754.png)Seletores agrupados

**Seletores de atributo**![300](../../../attachments/Pasted%20image%2020250512154609.png)Seleciona a que tenha o atributo target
![300](../../../attachments/Pasted%20image%2020250512154753.png)Seleciona a com o valor blank no target

---
#### **2.3 Pseudo-classes**
Uma pseudo-classe especifica algum estado especial de um elemento.
- :**hover**: faz com que quando o mouse é passado por cima novos elementos surjam.
- :**visited**: se o link já foi visitado um novo estilo pode ser adicionado.
- :**active**: se algo for ativado (link, botão) um novo estilo é adicionado.
- :**focus** é usado para estilizar um elemento quando está selecionado ou ativo para interação.
- obs: **“transition duration: 1s;”** define o tempo para fazer a alteração.  
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6G4y0VSZUSbxDEjMJP_CqYJJwX5l9V-FqG-GsO9eozMfxmj5avcblJ0e-y3aO0xMj_gsQbrJLEaB7ZawwEIpTuj5OCuUFjTRby1k2G1wIDL8bEYid5jN6NiRS4b-RAfg8uqIehw?key=VYJVAqKhTdZyHt8enJbiwA)
**NTH-CHILD**
![500](../../../attachments/Pasted%20image%2020260817110008.png)![500](../../../attachments/Pasted%20image%2020260817110026.png)![300](../../../attachments/Pasted%20image%2020260817110046.png)

---

#### **2.4 Pseudo elemento**
Os pseudo-elementos permitem estilizar pedaços específico de um elemento.

**First-letter** modifica a primeira letra.
![300](../../../attachments/Pasted%20image%2020250512160202.png)![Pasted image 20250512160218](../../../attachments/Pasted%20image%2020250512160218.png)
**marker** modifica o marcador de listas.
![300](../../../attachments/Pasted%20image%2020250512160457.png)
![100](../../../attachments/Pasted%20image%2020250512160509.png)
**selection** modifica quando você seleciona o conteúdo com o mouse
![200](../../../attachments/Pasted%20image%2020250512160626.png)
Existem tambem: o before, after, first-line


---

![](../../../attachments/Pasted%20image%2020260817103648.png)
A) HTML
B) CSS