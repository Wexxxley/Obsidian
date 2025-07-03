
---

Enquanto os novos sistemas habilitados para IPv6 podem enviar, rotear e receber datagramas IPv4, os sistemas habilitados para IPv4 não podem manusear datagramas IPv6. 

1. **Tunelamento:** O tunelamento permite que dois nós IPv6 se comuniquem usando datagramas IPv6 mesmo que existam roteadores IPv4 intermediários. A ideia é:
    - Um nó IPv6 encapsula o datagrama IPv6 inteiro dentro do campo de dados de um datagrama IPv4. 
    - Um valor é atribuído **no campo "Protocolo" do cabeçalho IPv4** que atua como um sinal para o nó receptor.
    - Os roteadores IPv4 intermediários tratam esse pacote como um datagrama IPv4 comum.
    - Quando o nó IPv6 no lado recebe o datagrama, ele o desencapsula. O datagrama IPv6 é então roteado normalmente para seu destino final.

![Pasted image 20250531084114](../../attachments/Pasted%20image%2020250531084114.png)