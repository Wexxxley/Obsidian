
---
Essa imagem ilustra o processo de **fragmentação e remontagem de datagramas IP**, que ocorre quando um pacote IP precisa atravessar enlaces com **diferentes tamanhos máximos de transmissão (MTU - Maximum Transmission Unit)**.

![Pasted image 20250523105949](../../attachments/Pasted%20image%2020250523105949.png)

- Um datagrama IP grande (4.000 bytes) **não cabe** em um enlace com MTU de 1.500 bytes.
- Nesse caso, o **roteador fragmenta** o datagrama em **três partes menores** para que cada uma caiba no enlace.
- Cada fragmento tem seu próprio cabeçalho IP com informações para identificação e ordenação.
- A **remontagem** **só acontece no destino final**.

![Pasted image 20250523110136](../../attachments/Pasted%20image%2020250523110136.png)

4000 = 20 + 1480 --> Dado original

1500 = 20 + 1480  --> Fragmento 1
1500 = 20 + 1480  --> Fragmento 2
1040 = 20 + 1020  --> Fragmento 3


