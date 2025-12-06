


---

O Docker é uma plataforma para executar aplicações em unidades leves chamadas **containers**. Você junta a aplicação com todas as suas dependências, permitindo que ela rode da mesma maneira em qualquer lugar, no seu pc, no data center ou cloud.

Alguns pontos para te situar antes de começar:

1. **Contêineres são leves e descartáveis:** Você pode rodar dezenas no seu laptop e centenas em um servidor. Eles não exigem muita memória ou processador, e não deixam rastros quando removidos.
    
2. **Plataforma Específica:** Um contêiner construído para uma plataforma (ex: Linux em Arm) não rodará em outra (ex: Windows em Intel) nativamente. Em produção, você precisa de servidores correspondentes.
    
3. **Docker Desktop e Emulação:** O Docker Desktop suporta múltiplas plataformas. Ele tem emulação embutida, então num Mac você pode rodar contêineres Intel e Arm juntos. No Windows, ele usa o WSL (Windows Subsystem for Linux) para rodar contêineres Linux e Windows juntos.
    
4. **Rede Virtual:** O Docker pode rodar múltiplos contêineres e juntá-los numa rede virtual, permitindo rodar aplicações distribuídas complexas no seu laptop. Porém, o Docker sozinho não conecta múltiplas máquinas físicas (para isso, você precisa de Kubernetes ou serviços de nuvem).    

**Código-fonte do livro** 
```bash
git clone https://github.com/sixeyed/diamol.git
cd diamol
git checkout 2e
```


### 1. Alguns comandos

- **docker container ls**: Por padrão, este comando lista apenas os contêineres que estão **rodando** no momento. 
	- **`-a` (all)**: O Docker passa a listar não só os que estão rodando, mas também os que estão com status parados.
	- **`-q` (quiet)**: Em vez de mostrar a tabela enorme com nomes e datas, ele retorna **apenas o ID numérico** do contêiner.
        
    - _Por que usar aqui?_ Porque o comando de deletar (que veremos a seguir) precisa receber apenas os números de identificação, não uma tabela de texto.
        

Resultado da Parte 1 + Parte 2 (docker container ls -aq):

O terminal gera uma lista simples de IDs, um por linha, de todos os contêineres da sua máquina.

---

### Parte 3: A "Mágica" do Shell `$(...)`

O símbolo `$()` não é um comando do Docker, mas sim do seu terminal (Shell/PowerShell).

- Ele diz ao computador: _"Execute o comando que está aqui dentro primeiro, pegue o resultado (a lista de IDs que vimos acima) e coloque-o aqui como se eu tivesse digitado manualmente"_. 4
    

---

### Parte 4: Removendo (`docker container rm -f`)

Agora a parte externa do comando, que recebe a lista de IDs:

- **`docker container rm`**: É o comando para remover (apagar) um contêiner. Normalmente, você digitaria `docker container rm <ID_DO_CONTAINER>`.
    
- **`-f` (force)**: Significa "forçar".
    
    - O Docker tem uma trava de segurança: ele proíbe você de apagar um contêiner que ainda está rodando5.
        
    - O `-f` ignora essa trava. Ele força a parada imediata do contêiner e o remove logo em seguida.
        

---

### Juntando tudo (O Resumo)

Quando você roda:

docker container rm -f $(docker container ls -aq)

O que acontece passo a passo é:

1. O **`ls -aq`** procura todos os contêineres (ativos e parados) e pega só os números de ID.
    
2. O **`$()`** pega esses números e os entrega para o comando de remover.
    
3. O **`rm -f`** pega essa lista e apaga todos eles de uma vez, sem pedir confirmação.
    

Ficou mais claro agora como as partes se conectam? Posso prosseguir para o **Capítulo 2**?


- Para recuperar espaço em disco (remove imagens do livro):
    
    `docker image rm -f $(docker image ls -f reference='diamol/*' -q)`
    
- O Docker é inteligente: se você rodar um comando no futuro e a imagem não estiver lá, ele fará o download novamente.
    

---

### Sobre o Docker ser "inteligente"

A frase _"se você rodar um comando no futuro e a imagem não estiver lá, ele fará o download novamente"_ significa o seguinte:

Quando você apaga uma imagem do seu computador (usando o comando acima), você não a perdeu para sempre. Essas imagens ficam hospedadas na nuvem (no **Docker Hub**).

Se amanhã você decidir refazer um exercício e rodar `docker run diamol/hello-world`:

1. O Docker vai procurar a imagem no seu PC.
    
2. Ele vai ver que você apagou.
    
3. Automaticamente, ele vai se conectar à internet, baixar a imagem de novo e rodar.
    

Isso permite que você limpe seu disco sem medo de "quebrar" os exercícios futuros.

Ficou mais claro o funcionamento técnico dos comandos? Podemos ir para o Capítulo 2? 1
---

### 1.5 Sendo imediatamente eficaz (Página 14)

"Imediatamente eficaz" é um princípio da série _Month of Lunches_.

- Cada capítulo começa com uma introdução, seguida de exercícios "Try it now" (Tente agora) onde você pratica.
    
- Depois há uma recapitulação com mais detalhes teóricos para preencher as lacunas.
    
- Por fim, um laboratório "Hands-on" para você ir para o próximo estágio.
    
- Todos os tópicos focam em tarefas genuinamente úteis no mundo real.