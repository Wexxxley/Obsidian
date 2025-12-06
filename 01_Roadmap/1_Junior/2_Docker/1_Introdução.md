


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
	- **`-q` (quiet)**: Retorna apenas o ID do contêiner.
	-  `docker container ls -aq`: O terminal gera uma lista simples de IDs, um por linha.

- **docker container rm**: É o comando para apagar um contêiner. Normalmente, você digitaria `docker container rm ID`.
	- **`-f` (force)**: O Docker tem uma trava de segurança: ele proíbe você de apagar um contêiner que ainda está rodando.        

- O símbolo `$()` não é do Docker, mas sim do bash, é chamado de substituição de comando

- **docker container rm -f $(docker container ls -aq)**: procura todos os contêineres (ativos e parados) e pega só os IDs e os entrega para o comando de remover e apaga todos eles de uma vez, sem pedir confirmação. 
	- Ele apaga absolutamente todos os contêineres da sua máquina. Se você quiser apagar apenas os contêineres da aula, precisaria usar um **filtro** (igual ao comando de imagens que vou explicar abaixo).

Aqui está a explicação do comando de imagens seguindo exatamente o seu padrão. Note que ele é **mais seguro** justamente por ter o filtro:
    

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