
#Concluded 

---
Casos de uso são documentos textuais usados para especificar requisitos, sendo geralmente mais detalhados que as Histórias de Usuário. Escritos pelos desenvolvedores após consultarem os usuários, os casos de uso **devem ser claros o suficiente para serem lidos, entendidos e validados pelos próprios usuários antes do início do design e da implementação.**

Um caso de uso descreve, da perspectiva de um **ator**, os passos necessários para atingir um objetivo específico no sistema. Ele é estruturado em duas listas de passos:

1. **Fluxo Normal**: Descreve o "cenário feliz", onde tudo ocorre como esperado.
2. **Extensões**: Descrevem fluxos alternativos, tratando situações de erro, exceções ou variações do fluxo normal. 

### **Exemplo: Transferir Valores entre Contas**

• **Ator**: Cliente do Banco

• **Fluxo normal**:
1. Autenticar Cliente (_inclusão de outro caso de uso_)
2. Cliente informa agência e conta de destino da transferência.
3. Cliente informa valor que deseja transferir.
4. Cliente informa a data em que pretende realizar a operação.
5. Sistema efetua transferência.
6. Sistema pergunta se o cliente deseja realizar uma nova transferência.

• **Extensões**:
1. 2a - Se conta e agência incorretas, solicitar nova conta e agência.
2. 3a - Se valor acima do saldo atual, solicitar novo valor.
3. 4a - Data informada deve ser a data atual ou no máximo um ano à frente.
4. 5a - Se data informada é a data atual, transferir imediatamente.
5. 5b - Se data informada é uma data futura, agendar transferência.

• **Foco no "o quê", não no "como"**: Evite detalhes de tecnologia, design ou interface. 
• **Evite casos de uso CRUD simples**: Não crie casos de uso separados para Cadastrar, Recuperar, Atualizar e Deletar. Agrupe-os em um único caso de uso, como "Gerenciar Professor".
