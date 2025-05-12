
Status: #Concluded 

---
# Multiplexação e Demultiplexação

**Multiplexação** é uma técnica que permite transmitir múltiplos fluxos de dados por um único canal de comunicação, otimizando o uso de recursos. Ela combina vários sinais em um só meio físico ou lógico, permitindo que diferentes comunicações compartilhem a mesma infraestrutura.
 
**Multiplexação (no host emissor):**
   - Processo de coletar dados de múltiplos sockets (aplicações)
   - Envelopar cada um desses dados com cabeçalhos (adicionando informações como portas de origem/destino)
   - Enviar os pacotes resultantes para a rede através da camada IP
  
**Demultiplexação (no host receptor):**
   - Processo de receber segmentos da camada IP
   - Examinar os cabeçalhos para determinar o socket correto (aplicação de destino)
   - Entregar os dados ao socket apropriado

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdPhDFrSx342Atfr92nKXoKF8XNOCDqkF-gVg2htsm6_OJSmsCDmMKYJTREXJZxHj5XeIz_xi4gayEgbVuR8Vw02z3R87Yy5vRcGVuMCyVvDutWrhL5j7GrG_5DVWQAFF82Ku1W?key=HrOhHC0_-ked6RNCpQ0o3PZn)
1. No host emissor, múltiplas aplicações enviam dados através de sockets diferentes.
2. O multiplexador combina esses fluxos, adicionando informações de porta
3. Os pacotes são enviados via IP para o destino
4. No receptor, o demultiplexador examina as portas e entrega os dados ao socket correto.  
