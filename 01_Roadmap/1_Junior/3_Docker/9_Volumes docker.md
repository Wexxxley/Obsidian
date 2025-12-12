


---
### **1. O que é um volume** 

Todo contêiner tem seu próprio sistema de arquivos, um disco virtual. Esse disco é montado pelo Docker juntando as camadas da imagem (que são fixas). Mas quando um container é apagado, esses dados são perdidos. Você nunca deve confiar na camada de escrita do contêiner para dados importantes. Para isso, precisamos de Volumes.

Um volume Docker é uma unidade de armazenamento, você pode pensar nele como um pen drive USB para contêineres. Os volumes existem independentemente dos contêineres e têm seus próprios ciclos de vida, mas podem ser anexados aos contêineres. Você cria um volume e o anexa ao contêiner da sua aplicação; ele aparece como um diretório no sistema de arquivos do contêiner. O contêiner grava dados no diretório, que são, na verdade, armazenados no volume. Quando você atualiza seu aplicativo com uma nova versão, você anexa o mesmo volume ao novo contêiner, e todos os dados originais ficam disponíveis.

Existem duas maneiras de usar volumes com contêineres: você pode criar volumes manualmente e anexá-los a um contêiner, ou pode usar uma instrução `VOLUME` no Dockerfile, que constrói uma imagem que criará um volume quando você iniciar um contêiner. 

---
### **2. Criando volume via Dockerfile**

A sintaxe é simplesmente `VOLUME <diretório-alvo>`. 
![](../../../attachments/Pasted%20image%2020251212164045.png)

Quando você executa um contêiner a partir desta imagem, o Docker cria automaticamente um volume e o anexa ao contêiner. O contêiner terá um diretório em `/data` no qual ele pode ler e escrever normalmente. Mas os dados estão, na verdade, sendo armazenados em um volume, que continuará existindo após o contêiner ser removido. 

---
### 3. Criando volume manualmente

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