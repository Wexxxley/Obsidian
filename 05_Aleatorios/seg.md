

internet kali

sudo ip addr flush dev eth0
sudo ip addr add 10.0.2.15/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 10.0.2.2
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
ping 8.8.8.8

Internet debian

sudo ip addr flush dev enp0s3
sudo ip addr add 10.0.2.15/24 dev enp0s3
sudo ip link set enp0s3 up
sudo ip route add default via 10.0.2.2
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf



VBoxManage modifyvm "Kali" --nic1 intnet --intnet1 "labseguranca"
VBoxManage modifyvm "Debian" --nic1 intnet --intnet1 "labseguranca"

```
sudo ip addr flush dev eth0
sudo ip addr add 192.168.1.10/24 dev eth0
sudo ip link set eth0 up
```

```
sudo ip addr flush dev enp0s3
sudo ip addr add 192.168.1.1/24 dev enp0s3
sudo ip link set enp0s3 up
```

```
ping 192.168.1.1
```

