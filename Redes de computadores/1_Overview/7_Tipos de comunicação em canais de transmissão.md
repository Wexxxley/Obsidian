

---
### **1. Simplex**
- Comunicação **unidirecional**. Os dados **fluem apenas em uma direção**.
- Exemplo: televisão, rádio.
    
- Características:
    - Um dispositivo **transmite** e o outro apenas **recebe**. Sem retorno de informação.
        

```
[Transmissor] ---> [Receptor]
```

---

### 2. **Half-Duplex (Semi-Duplex)**

- Comunicação em **duas direções**, mas **não simultânea**.
    
- Em um dado momento, **apenas um lado transmite**, o outro apenas escuta.
    
- Exemplo: walkie-talkie, rádios amadores.
    
- Características:
    
    - O canal é **compartilhado**.
        
    - Necessário controle para alternar entre enviar e receber.
        

```
[Dispositivo A] <---/---> [Dispositivo B]
```

- (ou transmite, ou recebe)
    

---

### 3. **Full-Duplex (Duplex Completo)**

- Comunicação em **duas direções ao mesmo tempo**.
    
- Ambos os dispositivos podem **enviar e receber simultaneamente**.
    
- Exemplo: chamadas telefônicas, redes Ethernet modernas.
    
- Características:
    
    - **Maior eficiência** e desempenho.
        
    - Necessário hardware que suporte comunicação simultânea.
        

```
[Dispositivo A] <---> [Dispositivo B]
(ao mesmo tempo)
```

---

### Comparativo Resumido

|Modo|Direção|Comunicação Simultânea?|Exemplo|
|---|---|---|---|
|Simplex|Unidirecional|Não|Televisão, rádio|
|Half-Duplex|Bidirecional|Não|Walkie-talkie|
|Full-Duplex|Bidirecional|Sim|Telefone, Ethernet|

---

### Extra: Outros conceitos relacionados

#### a) **Modo Assíncrono**

- Comunicação sem sincronização de relógios entre remetente e receptor.
    
- Utiliza bits de início/parada.
    
- Exemplo: RS-232.
    

#### b) **Modo Síncrono**

- Comunicação com relógios sincronizados.
    
- Dados transmitidos em blocos contínuos.
    
- Exemplo: Ethernet, redes modernas.
    

#### c) **Canal ponto a ponto**

- Canal dedicado entre duas entidades.
    

#### d) **Canal broadcast**

- Canal onde uma mensagem enviada é recebida por todos os dispositivos da rede.
    
- Exemplo: redes Wi-Fi, LANs antigas com hubs.
    

---

Quer que eu te faça um esquema visual didático de todos esses modos em uma imagem?  
Se quiser, apenas diga "**sim, esquema.**"