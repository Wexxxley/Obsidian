
#Concluded 

---
### **1. Monitoramento e Inspeção

- Listar ativos:    
    'docker container ls

- Listar TODOS (ativos e parados):
    
    docker container ls -a
    
- Listar apenas os IDs (útil para scripts):
    
    docker container ls -q
    
- Ver logs (Saída do terminal):
    
    docker container logs <nome_ou_id>
    
    - `-f`: (Follow) Fica "assistindo" os logs em tempo real (igual `tail -f`).
        
- Ver processos internos:
    
    docker container top <nome_ou_id>
    
    (Mostra os processos Linux rodando dentro daquele contêiner).
    
- Ver consumo de recursos (CPU/RAM):
    
    docker container stats
    
    (Mostra uma tabela viva de consumo de memória e processador).
    
- Inspecionar detalhes técnicos:
    
    docker container inspect <nome_ou_id>
    
    (Retorna o JSON completo com IP, volumes montados, variáveis de ambiente, etc).
    

---

### **2. Ciclo de Vida (Parar, Iniciar e Interagir)**

- Parar educadamente (SIGTERM):
    
    docker container stop <nome_ou_id>
    
    (O app tem 10s para salvar e fechar. É o recomendado).
    
- Matar forçadamente (SIGKILL):
    
    docker container kill <nome_ou_id>
    
    (Puxa o cabo da tomada. Use apenas se o contêiner travou).
    
- Iniciar um contêiner parado:
    
    docker container start <nome_ou_id>
    
- Reiniciar (Stop + Start):
    
    docker container restart <nome_ou_id>
    
- Executar comando dentro de um contêiner vivo:
    
    docker container exec -it <nome_ou_id> bash
    
    (Entra no terminal do contêiner. Se for Alpine Linux, use sh em vez de bash).
    

---

### **3. Limpeza de Contêineres (Remoção)**

- Apagar um contêiner:
    
    docker container rm <nome_ou_id>
    
    (Só funciona se o contêiner estiver parado/Exited).
    
- Forçar a remoção (Rodando ou Parado):
    
    docker container rm -f <nome_ou_id>
    
    (Mata o contêiner e apaga a camada de escrita imediatamente).
    

#### **Automação e Scripts de Limpeza (Shell Linux)**

O uso de `$()` executa o comando de dentro primeiro e passa o resultado para o comando de fora.

- **Parar TODOS os contêineres de uma vez:**
    
    Bash
    
    ```
    docker stop $(docker container ls -q)
    ```
    
- **Apagar TODOS os contêineres (Limpeza total):**
    
    Bash
    
    ```
    docker container rm -f $(docker container ls -aq)
    ```
    
- Apagar contêineres específicos (Filtro avançado):
    
    Ex: Apagar apenas os que usam imagens diamol:
    
    Bash
    
    ```
    docker container rm -f $(docker container ls -aq -f ancestor=diamol/*)
    ```
    

---

### **4. Gerenciamento de Imagens**

Lembre-se: Imagens são os **moldes** (read-only).

- Baixar imagem (sem rodar):
    
    docker image pull <nome_da_imagem>
    
- Listar imagens baixadas:
    
    docker image ls
    
- Listar com filtro:
    
    docker image ls -f reference='diamol/*'
    
- Renomear (Taggear) imagem:
    
    docker image tag <imagem_atual> <novo_nome_ou_usuario/repo:versao>
    
    (Cria uma referência nova apontando para a mesma imagem).
    
- Apagar imagem:
    
    docker image rm <nome_da_imagem>
    
    (Falha se houver um contêiner, mesmo parado, usando essa imagem).
    
- Forçar apagamento da imagem:
    
    docker image rm -f <nome_da_imagem>
    

---

### **5. A "Arma Nuclear" (Limpeza do Sistema)**

Em vez de criar scripts complexos, o Docker tem um comando nativo para limpar o lixo.

- Limpeza segura (Prune):
    
    docker system prune
    
    - Apaga contêineres parados.
        
    - Apaga redes não usadas.
        
    - Apaga imagens _dangling_ (aquelas `<none>` sem nome).
        
    - Apaga cache de build.
        
- Limpeza TOTAL (Cuidado!):
    
    docker system prune -a --volumes
    
    - O `-a` apaga até imagens que têm nome mas não estão sendo usadas por nenhum contêiner agora.
        
    - O `--volumes` apaga volumes não usados (perigo de perda de dados).

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
