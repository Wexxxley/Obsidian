
---
### **1. Definindo variáveis de cor**
![[Pasted image 20250527095845.png]]
- `:root { ... }` define **variáveis CSS** que podem ser usadas em todo o seu arquivo CSS.Dentro dele, você declara variáveis com dois hífens no início, por exemplo: `--cor-mais_escura`.
- Essas variáveis facilitam a manutenção e a reutilização de cores e valores no CSS.  
- Para usar uma variável, utilize a função `var()`. 

**Vantagens:**
- Se quiser mudar uma cor em todo o site, basta alterar o valor na variável.
- Deixa o código mais organizado e fácil de entender.

---
### **2. Limpando a base do css**
![[Pasted image 20250527095931.png]]
- **Remove espaçamentos padrão:** Elimina as margens e paddings padrões dos navegadores, deixando o layout mais previsível e consistente.
- **Facilita o controle do layout:** Com `box-sizing: border-box`, a largura e altura dos elementos incluem bordas e paddings, facilitando o cálculo de tamanhos.