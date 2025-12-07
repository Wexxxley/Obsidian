
#Concluded 

---
O Docker é uma plataforma para executar aplicações em unidades leves chamadas **containers**. Você junta a aplicação com todas as suas dependências, permitindo que ela rode da mesma maneira em qualquer lugar, no seu pc, no data center ou cloud.

1. **Contêineres são leves e descartáveis:** Você pode rodar dezenas no seu laptop e centenas em um servidor. Eles não exigem muita memória e não deixam rastros quando removidos.
    
2. **Plataforma Específica:** Um contêiner construído para uma plataforma não rodará em outra nativamente. Em produção, você precisa de servidores correspondentes.
    
3. **Docker Desktop:** O Docker Desktop suporta múltiplas plataformas. Ele tem emulação embutida, então num Mac você pode rodar contêineres Intel e Arm juntos. No Windows, ele usa o WSL para rodar contêineres Linux e Windows juntos.
    
4. **Rede Virtual:** O Docker pode rodar múltiplos contêineres e juntá-los numa rede virtual, permitindo rodar aplicações distribuídas complexas no seu laptop. Porém, o Docker sozinho não conecta múltiplas máquinas físicas (para isso, você precisa de Kubernetes ou serviços de nuvem).    

**Código-fonte do livro** 
```bash
git clone https://github.com/sixeyed/diamol.git
cd diamol
git checkout 2e
```

---
### **1. Apagando containers**

- `docker container ls`: Por padrão, este comando lista apenas os contêineres que estão rodando no momento. 
	- `-a` (all): O Docker passa a listar os que estão parados.
	- `-q` (quiet): Retorna apenas o ID do contêiner.

- `docker container rm ID`: Apaga um contêiner. 
	- `-f` (force): O Docker proíbe você de apagar um contêiner que está rodando.        

- `$()`: Comando do bash. Chamado de **substituição de comando**

- `docker container rm -f $(docker container ls -aq)`: procura todos os contêineres, pega só os IDs e os entrega para o comando de remover.
	- Ele apaga absolutamente todos os contêineres da sua máquina. Se você quiser apagar apenas os contêineres da aula, precisaria usar um **filtro**.
	- `docker container rm -f $(docker container ls -aq -f ancestor=diamol/*)`: apague apenas os contêineres que nasceram de imagens que começam com diamol.

---
### **2. Apagando imagens**

- `docker image ls`: Lista todas as imagens que foram baixadas ou criadas no seu computador.
    - `-f` (filter):  Argumento `reference='diamol/*'` diz ao Docker: Pegue apenas as imagens cujo nome começa com `diamol/`.
    
- `docker image rm`: É o comando para apagar uma imagem do disco.
    - `-f` (force): Docker não deixa apagar uma imagem se existir algum contêiner usando ela. 
    
- `docker image rm -f $(docker image ls -f reference='diamol/*'-q)`: O comando interno lista os IDs das imagens que começam com "diamol". O comando externo recebe essa lista e força a remoção delas, preservando suas outras imagens.

---
### **3. Mas o que é um contêiner?**

Um contêiner Docker é como uma caixa física: você coloca sua aplicação dentro dele. Dentro dessa caixa, a aplicação "pensa" que tem um computador inteiro só para ela, com seu próprio hostname, endereço IP e disco. Esses recursos são **virtuais**, criados e gerenciados pelo Docker.

Como o Docker equilibra dois problemas conflitantes da computação:

1. **Isolamento:** Aplicações precisam ser separadas. Se uma travar ou consumir muita CPU, não deve afetar as outras.
2. **Densidade:** Você quer rodar o máximo possível de aplicações em um único computador para economizar dinheiro e recursos.

#### **3.1 A Solução Antiga (Máquinas Virtuais):**

As VMs resolvem o isolamento, mas são pesadas. Cada VM precisa de seu próprio Sistema Operacional completo. Se você tem 3 apps em 3 VMs, você tem 3 sistemas operacionais consumindo memória e CPU só para manter a VM ligada.
#### **3.2 A Solução Docker (Contêineres):**

Cada contêiner tem seu ambiente virtual isolado. Mas todos compartilham o mesmo Sistema Operacional do computador. Isso os torna extremamente leves. Você pode rodar de 5 a 10 vezes mais contêineres do que VMs no mesmo hardware.

![](../../../attachments/Pasted%20image%2020251207141954.png)