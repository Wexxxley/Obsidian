


---
# Usando volumes Docker para armazenamento persistente

Contêineres são perfeitos para aplicações "stateless" (sem estado), onde você pode subir e descer instâncias sem perder nada importante. Mas a maioria dos sistemas precisa salvar dados em algum lugar (bancos de dados, arquivos).

Neste capítulo, você aprenderá como dockerizar aplicações **stateful** (com estado) usando **Volumes** e **Mounts** (montagens) para garantir que seus dados sobrevivam mesmo se o contêiner for destruído.

### 6.1 Por que os dados em contêineres não são permanentes

Todo contêiner tem seu próprio sistema de arquivos (um disco virtual). Esse disco é montado pelo Docker juntando as **camadas da imagem** (que são fixas/somente leitura) com uma **camada de escrita** (writable layer) que é exclusiva daquele contêiner.

#### O Isolamento do Sistema de Arquivos

Cada contêiner tem seu próprio disco isolado. Mesmo que você rode 10 contêineres da mesma imagem, se você alterar um arquivo no "Contêiner A", o "Contêiner B" não saberá disso.

**Tente agora:** Vamos provar isso rodando dois contêineres que geram números aleatórios e salvam em um arquivo.

1. Rode dois contêineres (`rn1` e `rn2`) a partir da mesma imagem:
    
    Bash
    
    ```
    docker container run --name rn1 diamol/ch06-random-number:2e
    docker container run --name rn2 diamol/ch06-random-number:2e
    ```
    
    _(Nota: Esses contêineres rodam um script que escreve um número num arquivo e depois param)._
    
2. Copie o arquivo gerado de dentro de cada contêiner para o seu computador:
    
    Bash
    
    ```
    docker container cp rn1:/random/number.txt number1.txt
    docker container cp rn2:/random/number.txt number2.txt
    ```
    
3. Verifique o conteúdo dos arquivos (no Linux/Mac use `cat`, no Windows `type`):
    
    Bash
    
    ```
    cat number1.txt
    cat number2.txt
    ```
    

**Resultado:** Você verá números diferentes.

Isso prova que cada contêiner tem sua própria camada de escrita. A imagem base é a mesma (somente leitura), mas o arquivo `number.txt` foi criado na camada de escrita exclusiva de cada contêiner.

#### O Problema da Persistência (Ciclo de Vida)

A camada de escrita (onde ficam seus dados novos) tem o mesmo ciclo de vida do contêiner.

- Se você **parar** (`stop`) o contêiner, os dados permanecem lá.
    
- Se você **remover** (`rm`) o contêiner, **a camada de escrita é destruída e os dados são perdidos para sempre**.
    

Vamos ver isso na prática com um contêiner que permite editar arquivos.

**Tente agora:**

1. Rode um contêiner chamado `f1`: `docker container run --name f1 diamol/ch06-file-display:2e` _(Ele vai mostrar o conteúdo de um arquivo texto padrão)._
    
2. Modifique esse arquivo dentro do contêiner (vamos sobrescrever o texto): `echo "https://blog.sixeyed.com" > url.txt` `docker container cp url.txt f1:/input.txt`
    
3. Inicie o contêiner novamente (ele vai ler o arquivo modificado): `docker container start --attach f1` _(Agora ele mostra o novo texto, provando que a alteração persistiu enquanto o contêiner existia)._
    
4. **Agora o teste destrutivo:** Remova o contêiner e crie um novo com o mesmo nome:
    
    Bash
    
    ```
    docker container rm -f f1
    docker container run --name f1 diamol/ch06-file-display:2e
    ```
    

**O que aconteceu?** O novo contêiner `f1` mostrou o texto original da imagem. A sua alteração foi perdida quando você rodou o comando `rm`.

**Conclusão:** Você nunca deve confiar na camada de escrita do contêiner para dados importantes (banco de dados, uploads). Para isso, precisamos de **Volumes**.

---

### 6.2 Executando contêineres com Volumes Docker

Um **Volume Docker** é como um pen drive USB virtual.

- Ele existe independentemente do contêiner.
    
- Ele tem seu próprio ciclo de vida (você pode apagar o contêiner e o volume fica lá).
    
- Você pode "plugar" (anexar) esse volume em qualquer contêiner.
    

Você pode criar volumes manualmente ou instruir o Docker a criá-los automaticamente através do comando `VOLUME` dentro de um Dockerfile.

#### Volumes definidos no Dockerfile

A imagem do próximo exercício (`diamol/ch06-todo-list:2e`) foi construída com a instrução `VOLUME /data`. Isso diz ao Docker: _"Sempre que alguém rodar este contêiner, crie um volume automaticamente e conecte-o na pasta `/data`"_.

**Tente agora:** Rode o aplicativo de lista de tarefas (To-Do List):

1. Rode o contêiner em background: `docker container run --name todo1 -d -p 8010:8080 diamol/ch06-todo-list:2e`
    
2. Verifique se o Docker realmente criou um volume para ele: `docker container inspect --format '{{json .Mounts}}' todo1`
    

Você verá na saída que o `Type` é `volume` e que existe um `Name` (um ID longo aleatório) para esse volume.

3. Acesse `http://localhost:8010` e adicione algumas tarefas na lista.
    
    - Esses dados estão sendo salvos num arquivo dentro da pasta `/data`, que agora vive em um **Volume**, não na camada de escrita descartável.
        

#### Compartilhando Volumes (O jeito rápido)

Se você iniciar um segundo contêiner, ele terá o próprio volume vazio. Mas e se você quiser que o segundo contêiner veja os dados do primeiro?

Você pode usar a flag `--volumes-from`.

**Tente agora:**

1. Rode um novo contêiner (`t3`) e diga para ele usar os volumes do `todo1`: `docker container run -d --name t3 --volumes-from todo1 diamol/ch06-todo-list:2e`
    
2. Verifique se o `t3` consegue ver os arquivos criados pelo `todo1`:
    
    - No Linux/Mac: `docker container exec t3 ls /data`
        
    - No Windows: `docker container exec t3 cmd /C "dir C:\data"`
        

Você verá os arquivos de banco de dados (`todo-list.db`) lá dentro. O contêiner `t3` está lendo o mesmo "pen drive" que o `todo1` .

---

**Fim da primeira parte do Capítulo 6.**

Até aqui vimos que contêineres perdem dados ao serem apagados e que volumes anônimos (com IDs aleatórios) resolvem a persistência.

Na próxima parte, vamos ver como usar **Volumes Nomeados** (Named Volumes) para fazer a atualização de uma aplicação sem perder os dados do usuário.

Podemos continuar para a **Seção 6.2 (Continuação - Volumes Nomeados)**?