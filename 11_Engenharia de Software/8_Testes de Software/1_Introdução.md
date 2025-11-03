
#Concluded 

---
### **1. Evolução das Práticas de Teste**

- **Modelo Waterfall (Tradicional):**
    - Testes ocorriam em uma fase separada, _após_ a codificação.
    - Frequentemente realizados por uma equipe de testes separada.
    - Muitas vezes manuais (alguém usava o sistema e verificava as saídas).
        
- **Métodos Ágeis (Moderno):**
    - Grande parte dos testes passou a ser **automatizada**.
    - Testes são escritos **durante** o desenvolvimento, às vezes até _antes_ do código.
    - O **próprio desenvolvedor** que implementa a classe também implementa seus testes.
    - Testes ganharam **novas funções**: além de detectar bugs, servem como **rede de proteção contra regressões** (garantir que mudanças não quebrem o que funcionava) e como **documentação** do código .

---
### **2. A Pirâmide de Testes (Mike Cohn):**

1. **Testes de Unidade:**
	- Verificam pequenas partes isoladas do código (geralmente uma classe) .
	- São os mais numerosos, simples, fáceis de implementar e rápidos de executar.
		
2. **Testes de Integração ou de serviços:**
	- Verificam uma funcionalidade ou transação completa, envolvendo diversas classes e, possivelmente, componentes externos (banco de dados, outros serviços).
		
3. **Testes de Sistema:**
	- Simulam a interação de um usuário real com o sistema através de sua interface .
	- São os mais caros, mais lentos e menos numerosos .
            
![](attachments/Pasted%20image%2020251027133352.png)


