
#Concluded 

---
Uma regra fundamental do JSX é que um componente deve retornar um único elemento. 

**Problema:** Até agora, temos envolvido os elementos `label` e `input` do componente `Search` dentro de uma `div`. Essa `div` extra é renderizada no DOM final. Em muitos casos, isso é inofensivo, mas pode quebrar layouts CSS  ou prejudicar a semântica HTML.
![](../../../../attachments/Pasted%20image%2020251124151047.png)

O **React Fragment** permite agrupar uma lista de filhos sem adicionar nós extras ao DOM. A forma mais comum de utilizar fragmentos é através da sintaxe vazia `<> ... </>`.
![](../../../../attachments/Pasted%20image%2020251124151206.png)
Ao inspecionar o elemento no navegador após essa mudança, você verá que a `div` container desapareceu.

Existe também a sintaxe explícita `<React.Fragment>`.
![](../../../../attachments/Pasted%20image%2020251124151416.png)
A sintaxe curta `<>` não suporta atributos. A única razão para usar a sintaxe completa `<React.Fragment>` é se você precisar passar um atributo **`key`** para o fragmento (comum ao mapear uma lista onde cada item retorna múltiplos elementos irmãos).