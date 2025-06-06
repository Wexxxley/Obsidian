
---
### **DropTail (FIFO)**
- É o tipo clássico de fila, configurado por padrão nos roteadores. 
- A memória que deve ser alocada para a fila depende da capacidade(bps) e do atraso de propagação do enlace: ==M = Capacidde x Atraso de propagaçaõ== 
- Em enlace de 1 Gbps com atraso de propação de 20 ms deve ter uma fila com tamanho de 1 Gbps x 0,02 s = 20 Mb = 2,5 MB
- Memórias muito grandes podem causar atrasos, e muito pequanas ocorre muita perda de pacotes.

 Round-Robin (RR)
 Weighted Round-Robin (WRR)
 Stochastic Fair Queuing (SFQ)
 Random Early Detection (RED)
 Hierárquica