


---
Todo contêiner tem seu próprio sistema de arquivos, um disco virtual. Esse disco é montado pelo Docker juntando as camadas da imagem (que são fixas). Mas quando um container é apagado, esses dados são perdidos. Você nunca deve confiar na camada de escrita do contêiner para dados importantes. Para isso, precisamos de Volumes.

Um Volume Docker é como um pen drive USB virtual.
- Ele existe independentemente do contêiner.
- Ele tem seu próprio ciclo de vida (você pode apagar o contêiner e o volume fica lá).
- Você pode "plugar" (anexar) esse volume em qualquer contêiner.

Você pode criar volumes manualmente ou instruir o Docker a criá-los automaticamente através do comando `VOLUME` dentro de um Dockerfile.
Vou explicar de forma direta, usando uma analogia que todo estudante de computação entende.

No Linux, o Docker guarda esses Volumes numa pasta segura (`/var/lib/docker/volumes/`), longe da bagunça dos seus arquivos pessoais.

**Criar um volume**
```bash
docker volume create nome-volume
```

**Plugando o volume no container**
Usamos a flag -v (ou --mount)
```
docker run -d -v nome-volume:/data nome-container
```
- "Pegue o volume `nome-volume` e faça ele aparecer como a pasta `/data` dentro desse contêiner".

```
# Lista todos os volumes criados
docker volume ls

# Mostra detalhes (onde ele está fisicamente no seu Linux)
docker volume inspect nome-volume
```

**Apagar volume**
Isso apaga os dados permanentemente. O Docker não deixa você apagar um volume que está sendo usado por um contêiner (mesmo parado).
```
docker volume rm nome-volume
```