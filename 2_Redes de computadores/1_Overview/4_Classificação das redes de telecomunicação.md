Status: #Concluded 

---
# 1 Classificação das redes de telecomunicação

 As redes de telecomunicações são usadas para enviar informações de um lugar para outro. Existem duas formas principais de fazer isso:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrpsk2pcZg2bZCYft-rNZ43B5YAuxybec7EKzdSY0f5xYFLIvS1hMefUAnQ8dQfLuOmnvLCR5uFYznekSpy_RtdlH6g-CgSc6g1lU4eCRl3ZevwA2e_UmYmTf7LBbblStBQFdHAw?key=HrOhHC0_-ked6RNCpQ0o3PZn)

---
# 1.1 Redes de Comutação de Circuitos

  Na comutação de circuitos, um ==caminho exclusivo é reservado e usado até o fim da comunicação.== Imagine que você está fazendo uma ligação telefônica tradicional. Quando você liga para alguém, a rede cria um caminho exclusivo entre você e a outra pessoa, que será mantido durante toda a ligação. 

 **Multiplexação** é uma ==técnica que permite transmitir múltiplos fluxos de dados por um único canal de comunicação, otimizando o uso de recursos==. Ela combina vários sinais em um só meio físico ou lógico, permitindo que diferentes comunicações compartilhem a mesma infraestrutura.
 
1. **FDM (Multiplexação por Divisão de Frequência)**: Cada usuário recebe uma frequência diferente para falar.  

2. **TDM (Multiplexação por Divisão de Tempo):** O mesmo canal é compartilhado por vários usuários, mas cada um pode falar em momentos diferentes.

==*Pode causar desperdícios de recursos visto que o canal pode ficar ocioso.==

---
# 1.2 Redes de Comutação de Pacotes

Na comutação de pacotes, os dados são divididos em pacotes pequenos e enviados de forma independente, sem caminho fixo. 

1. **Redes de CVs (Circuitos Virtuais):** Antes de enviar os pacotes, um caminho virtual é criado e mantido durante a comunicação, mas não é fisicamente fixo, caso necessário o caminho pode sofrer alterações.

2. **Redes de Datagramas**: Cada pacote pode viajar por um caminho diferente, chegando ao destino em ordem ou fora de ordem. 


