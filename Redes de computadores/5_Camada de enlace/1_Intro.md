
---

A camada de enlace tem a responsabilidade de transferir um datagrama de um nó para o nó
vizinho sobre um enlace. Enlace é um canal de comunicação que conecta nós(hospedeirso e roteadores) vizinhos.

- **Enlaces com fio:** Utilizam um **meio físico**, como cabos (par trançado, coaxial, fibra óptica), para transmitir dados entre dispositivos. A transmissão ocorre por meio de sinais elétricos ou luz.
- **Enlaces sem fio (wireless):** Não utilizam cabos físicos, usam ondas eletromagnéticas (como rádio, micro-ondas, infravermelho) para transmitir dados pelo ar. Sempre possui interferências.

### **Serviços da camada de enlace**

1. **Enquadramento**: 
	- Encapsula datagramas em quadros acrescentando cabeçalhos.
	- Implementa acesso ao canal se o meio é compartilhado. Isso significa que, se vários dispositivos estão usando o mesmo meio de comunicação o enquadramento garante que apenas um dispositivo transmita por vez para evitar colisões
	- endereços físicos/MAC usados nos cabeçalhos para Identificar a fonte e o destino.
2. **Entrega confiável** entre dois equipamentos fisicamente conectados:
	- Entrega confiável é muito associado ao TCP.
	- Raramente usado em enlaces com baixa taxa de erro (como fibra óptica).
	- Enlaces sem fio: altas taxas de erro.