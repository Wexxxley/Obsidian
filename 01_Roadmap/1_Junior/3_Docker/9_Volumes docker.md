


---
Neste capítulo, você aprenderá como dockerizar aplicações **stateful** (com estado) usando **Volumes** e **Mounts** (montagens) para garantir que seus dados sobrevivam mesmo se o contêiner for destruído.

Todo contêiner tem seu próprio sistema de arquivos (um disco virtual). Esse disco é montado pelo Docker juntando as **camadas da imagem** (que são fixas) com uma **camada de escrita** que é exclusiva daquele contêiner.

###  Executando contêineres com Volumes Docker

Um **Volume Docker** é como um pen drive virtual.
- Ele existe independentemente do contêiner.
- Ele tem seu próprio ciclo de vida (você pode apagar o contêiner e o volume fica lá).
- Você pode anexar esse volume em qualquer contêiner.

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