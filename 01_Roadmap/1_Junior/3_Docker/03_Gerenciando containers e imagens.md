
#Concluded 

---
### **1. Monitorando containers** 

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
    - Apaga todos os contêineres baseados em imagens específicas.
    - **`-f ancestor=...` (filter):** Seleciona apenas contêineres criados a partir de imagens que começam com esse nome.

---
### **4. Gerenciando Imagens**

- **`docker image ls`**
    - Lista as imagens baixadas.
    - **`-f reference='diamol/*'` (filter):** Mostra apenas imagens que começam com esse nome.
        
- **`docker image rm <Nome>`**    
    - Apaga a imagem do disco.
    - **`-f` (force):** Obriga a apagar a imagem mesmo se existir um contêiner (parado ou rodando) usando ela.

---
### **5. Limpeza Geral**

- **`docker system prune`**
    - Faz uma faxina segura: remove contêineres parados, redes não usadas e imagens sem nome.
    - **`-a` (all):** Remove também imagens não usadas (limpa o cache de imagens).

