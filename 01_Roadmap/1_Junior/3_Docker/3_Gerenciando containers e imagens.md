
#Concluded 

---
### **1. Monitoramento 

- **`docker container ls`**
    - Lista apenas os contêineres rodando.
    - **`-a` (all):** Mostra todos.
    - **`-q` (quiet):** Mostra apenas os IDs numéricos.
        
- **`docker container logs <ID>`**
    - Mostra o histórico de saída do terminal do contêiner.
    - **`-f` (follow):** Trava a tela e fica mostrando novos logs em tempo real.
        
- **`docker container inspect <ID>`**
    - Retorna um JSON com todos os detalhes técnicos (IP, Volumes, Variáveis de Ambiente).

---
### **2. Parando e Iniciando containers**

- **`docker container stop <ID>`**
    - Para o contêiner de forma segura.
        
- **`docker container kill <ID>`**
    - Mata o processo imediatamente. Pode corromper arquivos.
        
- **`docker stop $(docker ps -q)`**
    - O comando de dentro (`docker ps -q`) gera uma lista de IDs. O comando de fora recebe essa lista e para todos de uma vez.

---
### **3. Apagando Contêineres**

- **`docker container rm <ID>`**
    
    - Remove um contêiner do disco. Só funciona se ele estiver parado.
    - **`-f` (force):** Remove o contêiner mesmo se estiver rodando.
        
- **`docker container rm -f $(docker container ls -aq)`**
    - Apaga **todos** os contêineres do seu computador (ativos e parados).
    - **`-a`**: Pega os parados também.
    - **`-q`**: Pega só os IDs.
    - **`-f`**: Força a remoção dos que estão rodando.
        
- **`docker container rm -f $(docker container ls -aq -f ancestor=diamol/*)`**
    - **Explicação:** Apaga todos os contêineres baseados em imagens específicas.
        
    - **`-f ancestor=...` (filter):** Seleciona apenas contêineres criados a partir de imagens que começam com esse nome.
        

---

### **4. Gerenciando Imagens**

- **`docker image ls`**
    
    - Lista as imagens baixadas.
        
    - **`-f reference='diamol/*'` (filter):** Mostra apenas imagens que começam com esse nome.
        
- **`docker image rm <Nome>`**
    
    - Apaga a imagem do disco.
        
    - **`-f` (force):** Obriga a apagar a imagem mesmo se existir um contêiner (parado ou rodando) usando ela.
        
- **`docker image prune`**
    
    - Apaga imagens "dangling" (lixo/sem nome `<none>`).
        
    - **`-a` (all):** Apaga também imagens que têm nome, mas **não estão sendo usadas** por nenhum contêiner no momento.
        

---

### **5. Limpeza Geral (System Prune)**

- **`docker system prune`**
    
    - Faz uma faxina segura: remove contêineres parados, redes não usadas e imagens sem nome.
        
    - **`-a` (all):** Remove também imagens não usadas (limpa o cache de imagens).
        
    - **`--volumes`:** Remove também volumes não usados (Cuidado: apaga dados persistentes).

### **1. Gerenciando containers**

1. **Listar:** `docker container ls` mostra apenas os ativos.
    
2. **Ver processos:** `docker container top <ID>` mostra os processos rodando dentro de um contêiner específico.
    
3. **Ver logs:** `docker container logs <ID>` mostra tudo que o aplicativo escreveu na tela. Isso é crucial para debugar apps que rodam em segundo plano.
    
4. **Inspecionar:** `docker container inspect <ID>` mostra todos os detalhes técnicos (IP, caminhos de disco, variáveis de ambiente) em formato JSON.

### **2. Parando containers**

```
docker container stop <nome_ou_id>
```


Use se o contêiner travou e não responde ao stop.
```
docker container kill <nome_ou_id>
```
 Pode corromper arquivos se o contêiner estava gravando algo no disco naquele momento.    

Se você tem 10 contêineres rodando e quer parar todos para limpar a casa, não precisa digitar um por um.
```
docker stop $(docker ps -q)
```

- `docker ps -q`: Lista apenas os IDs numéricos dos contêineres ativos.
- `$()`: Pega essa lista e passa para o comando stop    



### **3. Apagando containers**

- `docker container ls`: Por padrão, este comando lista apenas os contêineres que estão rodando no momento. 
	- `-a` (all): O Docker passa a listar os que estão parados.
	- `-q` (quiet): Retorna apenas o ID do contêiner.

- `docker container rm ID`: Apaga um contêiner. 
	- `-f` (force): O Docker proíbe você de apagar um contêiner que está rodando.        

- `$()`: Chamado de substituição de comando.

- `docker container rm -f $(docker container ls -aq)`: Ele apaga absolutamente todos os contêineres da sua máquina. Se você quiser apagar apenas os contêineres da aula, precisaria usar um filtro.
	- `docker container rm -f $(docker container ls -aq -f ancestor=diamol/*)`: apague os contêineres que nasceram de imagens que começam com diamol.

---
### **4. Apagando imagens**

- `docker image ls`: Lista todas as imagens que foram baixadas ou criadas.
    - `-f` (filter):  Argumento `reference='diamol/*'` diz ao Docker: Pegue apenas as imagens cujo nome começa com diamol/.
    
- `docker image rm`: É o comando para apagar uma imagem do disco.
    - `-f` (force): Docker não apaga uma imagem se existir algum contêiner usando-a.
    
- `docker image rm -f $(docker image ls -f reference='diamol/*'-q)`: O comando interno lista os IDs das imagens que começam com "diamol". O comando externo recebe essa lista e força a remoção delas, preservando suas outras imagens.
