
---
# 1 FTP: Protocolo de transferencia de arquivos

 O FTP é um protocolo para transferência de arquivos entre um cliente e um servidor, usando duas conexões TCP separadas:

1. **Conexão de controle (porta 21):** O cliente se conecta. Essa conexão é mantida aberta durante toda a sessão. Serve para enviar comandos (ex: USER, PASS, LIST, RETR, etc).
2. **Conexão de dados (porta variável):** Quando o cliente manda um comando para transferência, o servidor abre uma nova conexão. Essa nova conexão serve somente para transferir os dados do arquivo. Para transferir um outro arquivo, uma nova conexão será aberta.

Conexão "**fora da banda**": Quando se diz que o FTP tem controle "fora da banda", significa que os comandos de controle (login, listar arquivos, etc.) são enviados por uma conexão. E os dados são enviados por outra conexão separada.  

  

Atualmente, o FTP está entrando em desuso, sendo substituído pelo HTTP.