


---

O Docker é uma plataforma para executar aplicações em unidades leves chamadas **containers**. Você junta a aplicação com todas as suas dependências, permitindo que ela rode da mesma maneira em qualquer lugar, no seu pc, no data center ou cloud.

### 1 Conceitos Técnicos Essenciais

- **Containers são efêmeros (Throwaway:** Diferente de servidores que você "cuida", containers são leves e descartáveis. Você pode rodar dezenas no seu laptop e eles não deixam rastro quando removidos.
    
- **Dependência de Plataforma:** Um container empacota binários e dependências. Isso significa que um container Linux não roda nativamente no Windows e vice-versa.
    
- **Isolamento vs. Orquestração:** O Docker em si gerencia containers em _uma_ máquina. Para conectar vários servidores e ter alta disponibilidade, você precisa de um **orquestrador** (como Kubernetes).


---

## Resumo: Capítulo 2 - Entendendo o Docker e o "Hello World"

Aqui começamos a parte prática. O objetivo deste capítulo é desmistificar o que realmente acontece quando você roda um container.

### 2.1 O Fluxo "Build, Share, Run"

O primeiro exercício é rodar o clássico "Hello World".

Comando: docker run diamol/ch02-hello-diamol:2e10.

O que acontece nos bastidores (o output do terminal revela o fluxo) 11:

1. **Check Local:** O Docker verifica se você já tem a imagem (o pacote da aplicação) na sua máquina. Se não tiver (`Unable to find image...`), ele vai buscar.
    
2. **Pull (Download):** O Docker baixa a imagem de um registro público (Docker Hub). Note que ele baixa em "camadas" (layers), não um arquivo único gigante12.
    
3. **Run (Execução):** O Docker cria um container a partir dessa imagem e inicia a aplicação.
    
4. **Output:** A aplicação roda (neste caso, um script que imprime "Hello from Chapter 2!"), exibe informações do sistema (Hostname, IP) e encerra 13.
    

Se você rodar o comando novamente, será instantâneo, pois a imagem já está no cache local (não precisa fazer o download/pull novamente)14.

### 2.2 Teoria: O que é um Container vs. Máquina Virtual (VM)

Esta é a parte teórica mais importante para sua base em CC.

O container funciona como uma "caixa" onde a aplicação roda. Dentro dessa caixa, a aplicação "acha" que tem um computador só para ela, com seu próprio **Hostname**, **Endereço IP** e **Disco**15.

A grande diferença arquitetural entre Containers e VMs é o **compartilhamento de recursos**:

|**Característica**|**Máquina Virtual (VM)**|**Container**|
|---|---|---|
|**Sistema Operacional**|Cada VM tem seu próprio SO completo (pesado, ocupa GBs de RAM/Disco)16161616.|Todos os containers compartilham o **mesmo Kernel do SO** do host17.|
|**Isolamento**|Isolamento físico via Hypervisor.|Isolamento lógico via recursos do Kernel (Namespaces/Cgroups)18.|
|**Desempenho**|Menor densidade (menos apps por servidor).|Alta densidade (muitos apps leves no mesmo servidor)19.|

**Conclusão:** Os containers resolvem o conflito entre **isolamento** (necessário para segurança e estabilidade) e **densidade** (necessário para eficiência de custos e recursos). Você consegue rodar 5 a 10 vezes mais containers do que VMs no mesmo hardware20.

---

Próximo passo:

Quer continuar com o restante do Capítulo 2 (seções 2.3 e 2.4), onde aprenderemos a conectar interativamente dentro de um container (como se fosse SSH) e a hospedar um site real, ou prefere pular para a criação das suas próprias imagens no Capítulo 3?