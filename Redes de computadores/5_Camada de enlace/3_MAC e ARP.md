
---

### **1. Endereço MAC/LAN/FÍSICO**
- Usado para levar o datagrama de uma interface física a outra na mesma rede.
- Endereços MAC tem 48 bits. Cada placa de rede no mundo possui seu end físico
- É gravado na memória fixa ROM do adaptador de rede.
- A alocação de endereços MAC é administrada pelo IEEE.
- O fabricante compra porções do espaço de endereço MAC. 
- Endereçamento MAC possui portabilidade, ou seja, sua máquina pode ter o mesmo end MAC mesmo em redes diferentes. Para isso, não pode ter duas máquinas com o mesmo end físico.
- Se for preciso mudar o end MAC, os drivers omitem o end da ROM e usam outro.