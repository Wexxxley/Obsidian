


---
Existem dois componentes principais que você precisa distinguir:

1. **Docker Engine:** É o processo que roda em segundo plano. Ele gerencia tudo: o cache local de imagens (baixando-as quando necessário), os contêineres ativos, as redes virtuais e os volumes. O Engine expõe todas as suas funcionalidades através de uma API.

2. **Docker CLI:** É a ferramenta de linha de comando que você usa no terminal O CLI é apenas um cliente. Ele não executa os contêineres. Ele apenas envia pedidos para a API do Docker Engine.    

![](../../../attachments/Pasted%20image%2020251207143012.png)

Porque essa sepração é importante?
- **Gerenciamento Remoto:** Como o CLI fala com o Engine via API, você pode usar o CLI no seu laptop para controlar um Docker Engine rodando em um servidor remoto.
- **Interfaces Gráficas:** O CLI não é o único cliente. Interfaces visuais (como o dashboard do Docker Desktop, Portainer ou lazydocker) também se conectam à mesma API para desenhar gráficos de uso de CPU, memória e logs.    

Lazydocker não é uma "GUI" tradicional, é uma TUI (Terminal User Interface). É uma interface gráfica que roda dentro do terminal.
```
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
```

![](../../../attachments/Pasted%20image%2020251207145101.png)
