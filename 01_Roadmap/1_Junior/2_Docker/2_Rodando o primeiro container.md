


---

Digite o seguinte comando para rodar o contêiner Hello World:
```bash
docker run hello-world
```

O objetivo desse contêiner é ser o mais leve possível e confirmar que o docker está funcionando na sua máquina.

1. O Docker checa se você já tem a imagem `hello-world` salva localmente.
2. Se não tiver, ele busca e baixa a imagem (faz o pull) do repositório Docker Hub.
3. O Docker cria e inicia um novo contêiner a partir dessa imagem.
4. O código dentro do contêiner é executado. Esse código simplesmente imprime uma mensagem no seu terminal, e então o contêiner encerra a execução.

![](../../../attachments/Pasted%20image%2020251207140344.png)

---

### Análise do Resultado (O que aconteceu?)

Quando você roda esse comando, verá uma saída similar à da **Figura 2.1** do livro. Vamos dissecar o que aconteceu linha por linha5555:

1. **O comando:** `docker run ...` diz ao Docker para rodar uma aplicação dentro de um contêiner.
    
2. **A Imagem:** A aplicação já foi empacotada e publicada com o nome `diamol/ch02-hello-diamol:2e`. No Docker, esse pacote de aplicação é chamado de **Imagem**6.
    
3. **O Download (Pull):**
    
    - O Docker precisa ter uma cópia da imagem localmente antes de rodar o contêiner.
        
    - Como é a primeira vez que você roda, você não tem a imagem.
        
    - O Docker avisa: `Unable to find image '...' locally` (Incapaz de encontrar a imagem localmente)7.
        
    - Então, ele baixa a imagem (o termo técnico é **pulling**). Você verá linhas com códigos (ex: `690e87... Pull complete`). Esses são os **layers** (camadas) da imagem sendo baixados 8.
        
4. **A Execução:**
    
    - Agora o Docker inicia um contêiner usando essa imagem.
        
    - A imagem contém todo o conteúdo da aplicação e instruções de como iniciá-la.
        
    - A aplicação neste exemplo é um script simples que escreve na tela9.
        

A Saída da Aplicação:

O script imprime informações sobre o ambiente onde está rodando 10:

- `Hello from Chapter 2!`
    
- `My name is: 2f97e02a5924` (Este é o **Hostname** ou nome da máquina virtual do contêiner).
    
- `I'm running on: Linux...` (O Sistema Operacional).
    
- `My address is: 172.17.0.2...` (O endereço IP do contêiner na rede virtual do Docker).
    

_Observação:_ Os detalhes exatos (como o ID `2f97...` e o IP) serão diferentes na sua máquina, pois o Docker gera isso dinamicamente11. Se você estiver no Windows, verá que o sistema operacional listado pode ser Windows, e se estiver num Raspberry Pi, verá que o processador é ARM 12.

---

### O Fluxo "Build, Share, Run"

Este exemplo simples demonstra o fluxo principal do Docker13:

1. **Build (Construir):** Alguém empacotou a aplicação (o autor fez isso).
    
2. **Share (Compartilhar):** Alguém publicou a imagem em um site público (Docker Hub) para que outros pudessem acessar.
    
3. **Run (Rodar):** Você, com acesso, rodou a aplicação.
    

A grande vantagem é que esse fluxo é o mesmo se a aplicação for um script simples ou um sistema bancário complexo em Java. A aplicação é **portátil**: roda em qualquer computador que tenha Docker14.

---

### Rodando pela segunda vez

O que acontece se você rodar o mesmo comando novamente?

#### Tente agora

Repita o comando exato:

`docker run diamol/ch02-hello-diamol:2e`

**O que mudou?**

1. O Docker **não** baixou a imagem novamente. Ele viu que já tinha uma cópia local (`Unable to find image...` não aparece) e foi direto para a execução15.
    
2. O resultado na tela é quase o mesmo, mas:
    
    - O **Nome (Hostname)** mudou (ex: de `2f97...` para `d147...`).
        
    - O **IP** pode ter mudado.
        

Isso acontece porque cada vez que você roda `docker run`, o Docker cria um **novo contêiner** fresco. É uma nova "caixa" com seu próprio nome e identificação, mesmo que esteja rodando a mesma aplicação 16.

---

Podemos avançar para a seção **2.2: Então, o que é um contêiner?**