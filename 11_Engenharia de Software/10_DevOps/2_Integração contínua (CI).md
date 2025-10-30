
#Concluded 

---

Era comum usar **branches de longa duração**. 
1. Um desenvolvedor (ex: Alice) criava um branch separado, trabalhava nele isoladamente por semanas ou meses e, só ao final, tentava integrar (fazer _merge_) seu código de volta ao branch principal (master/trunk).
2. **Integration Hell:** Durante esse tempo, o branch principal continuava evoluindo (outros desenvolvedores integravam seus códigos). Quando Alice finalmente tentava fazer o _merge_, surgiam inúmeros **conflitos de integração**.
    
**Definição:** CI é uma prática de desenvolvimento (originalmente do XP). A ideia é simples: em vez de integrar raramente,  os desenvolvedores devem integrar seu código no branch principal de forma frequente e contínua. Pelo menos uma vez pode dia

---
### **Boas Práticas para Uso de CI**

1. **Build Automatizado:** O processo de compilar todo o sistema e gerar uma versão executável deve ser totalmente automatizado.
    
2. **Testes Automatizados:** O build automatizado deve **rodar a suíte de testes** automaticamente. Isso garante que o novo código não apenas compila, mas também não introduziu regressões.
    
3. **Servidores de Integração Contínua (Servidor de CI):**
    - São ferramentas (como Jenkins, TravisCI, GitLab CI) que automatizam esse fluxo.
	
	1. O desenvolvedor faz um _commit_ (e _push_) no repositório.
	2. O VCS avisa o Servidor de CI.
	3. O Servidor de CI clona o código, executa o **build automatizado** e roda os **testes automatizados**.
	4. O servidor notifica o time/desenvolvedor se o build passou ou quebrou.
        
4. **Desenvolvimento Baseado no Trunk (Trunk Based Development - TBD):**
    - TBD significa que todos os desenvolvedores trabalham diretamente no branch principal, evitando _merges_ complexos. É a prática usada por Google e Facebook.
        