


---
### **1. O que é Bind Mount**
Até agora, usamos volumes. O Docker gerenciava onde os dados ficavam (numa pasta escondida em `/var/lib/docker/...`).

Um **Bind Mount** é diferente: você diz explicitamente ao Docker para usar uma pasta do seu host e fazê-la aparecer dentro do contêiner.

- **Volume:** "Docker, guarde esses dados para mim num lugar seguro. Eu não quero saber onde é, só quero que persista." (Ideal para Banco de Dados).
    
- **Bind Mount:** "Docker, pegue a pasta `/home/wesley/projeto` do meu Linux e faça ela aparecer em `/app` dentro do contêiner." (Ideal para Desenvolvimento e Configuração).

Imagine que você quer mudar a configuração de um site.

- **Sem Bind Mount:** Você edita o arquivo no seu PC -> Reconstrói a imagem (`docker build`) -> Mata o contêiner antigo -> Roda o novo.
    
- **Com Bind Mount:** Você mapeia o arquivo de configuração do seu PC para dentro do contêiner. Você edita no seu PC, salva, e o contêiner lê a mudança na hora.

---
### **2. Exemplo de uso**

Imagine que dentro do contêiner existe um arquivo de configuração padrão na imagem. Você quer mudar uma configuração, mas não quer ter que reconstruir a imagem inteira só para mudar uma linha de texto.

O **Bind Mount** permite que você pegue um arquivo do seu computador e **"cole por cima"** do arquivo que está dentro do contêiner.

O comando mágico é sempre a flag `-v` (ou `--volume`):

```
docker run -v <CAMINHO_NO_SEU_PC>:<CAMINHO_NO_CONTAINER> ...
```

- **Lado Esquerdo**: É a pasta ou arquivo no seu pc. 
- **Lado Direito**: É onde esse arquivo vai aparecer dentro do contêiner.

O exemplo mais comum no mundo real é com servidores web, como o **Nginx**.

1. O Nginx padrão já vem com um arquivo de configuração dentro dele em `/etc/nginx/nginx.conf`.
2. Você cria um arquivo `meu-site.conf` no seu computador com as suas regras.
3. Você roda o contêiner dizendo: _"Docker, faça o meu arquivo `meu-site.conf` substituir o `/etc/nginx/nginx.conf` lá dentro"_.
 
```
docker run -d \
  -v /home/wesley/meu-site.conf:/etc/nginx/nginx.conf \
  nginx
```

---
### **3. Entendendo as limitações do sistema de arquivos**

Bind Mounts são poderosos, mas perigosos. Você está abrindo um buraco direto entre o contêiner e o seu sistema operacional. Se você mover a pasta `config` no seu computador ou apagar o arquivo, o contêiner vai quebrar na próxima vez que reiniciar. 
