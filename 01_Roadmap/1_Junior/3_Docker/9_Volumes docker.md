


---
Todo contêiner tem seu próprio sistema de arquivos, um disco virtual. Esse disco é montado pelo Docker juntando as camadas da imagem (que são fixas). Mas quando um container é apagado, esses dados são perdidos. Você nunca deve confiar na camada de escrita do contêiner para dados importantes. Para isso, precisamos de Volumes.

Um Volume Docker é como um pen drive USB virtual.
- Ele existe independentemente do contêiner.
- Ele tem seu próprio ciclo de vida (você pode apagar o contêiner e o volume fica lá).
- Você pode "plugar" (anexar) esse volume em qualquer contêiner.

Você pode criar volumes manualmente ou instruir o Docker a criá-los automaticamente através do comando `VOLUME` dentro de um Dockerfile.
Vou explicar de forma direta, usando uma analogia que todo estudante de computação entende.

No Linux, o Docker guarda esses Volumes numa pasta segura (`/var/lib/docker/volumes/`), longe da bagunça dos seus arquivos pessoais.

#### 1. Criar um Volume (Comprar o HD Externo)

Você dá um nome para ele, para poder achá-lo depois.

Bash

```
docker volume create dados-do-banco
```

#### 2. Usar o Volume (Plugar o HD no Contêiner)

Essa é a parte mais importante. Usamos a flag -v (ou --mount).

A sintaxe é: -v nome-do-volume:/onde/ele/vai/aparecer/no/container

Bash

```
# Exemplo genérico
docker run -d -v dados-do-banco:/data minha-imagem
```

_Isso diz: "Pegue o volume `dados-do-banco` e faça ele aparecer como a pasta `/data` dentro desse contêiner"._

#### 3. Listar e Inspecionar (Ver o que você tem)

Bash

```
# Lista todos os volumes criados
docker volume ls

# Mostra detalhes (onde ele está fisicamente no seu Linux)
docker volume inspect dados-do-banco
```

#### 4. Apagar o Volume (Jogar o HD fora)

Cuidado: isso apaga os dados permanentemente. O Docker não deixa você apagar um volume que está sendo usado por um contêiner (mesmo parado).

Bash

```
docker volume rm dados-do-banco
```

---

### Resumo da Prática que acabamos de fazer

Aplicando isso ao exercício do livro que você acabou de rodar:

1. **O Problema:** O app To-Do salva as tarefas num arquivo dentro da pasta `/data` do contêiner. Se o contêiner morre, a pasta `/data` morre junto.
    
2. **A Solução:**
    
    - Criamos o "HD Externo": `docker volume create todo-list`.
        
    - Rodamos o container V1 plugando o HD na pasta do app: `-v todo-list:/data`.
        
    - O app gravou as tarefas no "HD Externo".
        
    - Destruímos o container V1 (o notebook queimou).
        
    - Rodamos o container V2 plugando o **mesmo** HD na mesma pasta: `-v todo-list:/data`.
        
    - **Mágica:** A versão 2 leu o "HD Externo" e achou as tarefas da versão 1.
        

Ficou mais claro e direto dessa forma?