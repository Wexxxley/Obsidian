
#Concluded 

---
### **1. O que é um volume** 

Todo contêiner tem seu próprio sistema de arquivos, um disco virtual. Esse disco é montado pelo Docker juntando as camadas da imagem (que são fixas). Mas quando um container é apagado, esses dados são perdidos. Você nunca deve confiar na camada de escrita do contêiner para dados importantes. Para isso, precisamos de Volumes.

![600](../../../attachments/Pasted%20image%2020251212190355.png)

Um volume Docker é uma unidade de armazenamento, você pode pensar nele como um pen drive USB para contêineres. Os volumes existem independentemente dos contêineres e têm seus próprios ciclos de vida, mas podem ser anexados aos contêineres. 

Você cria um volume e o anexa ao contêiner da sua aplicação; ele aparece como um diretório no sistema de arquivos do contêiner. O contêiner grava dados no diretório, que são, na verdade, armazenados no volume. Quando você atualiza seu aplicativo com uma nova versão, você anexa o mesmo volume ao novo contêiner.

>[!info]
>
Essa arquitetura de muitos containers usarem um mesmo volume é muito usada para **Escalabilidade Horizontal**. Exemplo: Você tem um site muito acessado e sobe 5 contêineres do mesmo site. Todos eles precisam ler as mesmas fotos de perfil dos usuários. Você conecta os 5 no mesmo volume..

Existem duas maneiras de usar volumes com contêineres: você pode criar volumes manualmente e anexá-los a um contêiner, ou pode usar uma instrução `VOLUME` no Dockerfile, que constrói uma imagem que criará um volume quando você iniciar um contêiner. 

---
### **2. Criando volume via Dockerfile**

A sintaxe é simplesmente `VOLUME <diretório-alvo>`. 
![](../../../attachments/Pasted%20image%2020251212164045.png)

Quando você executa um contêiner a partir desta imagem, o Docker cria automaticamente um volume e o anexa ao contêiner. O contêiner terá um diretório em `/data` no qual ele pode ler e escrever normalmente. Mas os dados estão, na verdade, sendo armazenados em um volume.

---
### **3. Criando volume manualmente**

**Criar um volume**
```bash
docker volume create nome-volume
```

**Plugando o volume no container**
Usamos a flag -v (ou --mount)
```
docker run -d -v nome-volume:/data nome-container
```

**Visualizando volumes**
- Lista todos os volumes criados: docker volume ls
- Mostra detalhes docker volume inspect nome-volume

![](../../../attachments/Pasted%20image%2020251212164551.png)
![](../../../attachments/Pasted%20image%2020251212164603.png)

**Apagar volume**
Isso apaga os dados permanentemente. O Docker não deixa você apagar um volume que está sendo usado por um contêiner (mesmo parado).
```
docker volume rm nome-volume
```
