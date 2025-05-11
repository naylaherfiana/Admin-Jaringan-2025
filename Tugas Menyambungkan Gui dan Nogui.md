# Tugas Menyambungkan Gui dan Nogui

# VM 1 (No Gui) disetel sebagai DNS

1. Set Interface
    - Adapter 1 : Bridge Adapter
    - Adapter 2 : Internal Network
2. Cek interface → ip a
3. Set IP Static `nano /etc/network/interfaces`
    
    tambahkan :
    
    `iface enp0s8 inet static`
    
    `address 192.168.200.1`
    
    `network 192.168.200.0`
    
    `network 255.255.255.0`
    
    `broadcast 192.168.200.255`
    
    `dns.nameservers 1.1.1.1`
    
4. Restart network
    - `systemctl restart networking`
5. `install iptables`
6. `echo 1 > /proc/sys/net/ipv4/ip.forward`
7. `iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`
8. `iptables -A FORWARD -i enp0s8 -o enp0s3 -j ACCEPT`
9. `iptables -A FORWARD -i enp0s3 -o enp0s8 -j ACCEPT`
10. `iptables -persistance`

# VM 2 (GUI) disetel sebagai Client

1. Set Interface
    - Adapter 1 : Internal Network
2. Set IP (Setting → Wired → IPv4)
    
    IPv4 Method = Manual
    
    Addresses
    
    - Address : 192.168.200.x
    - Netmask : 255.255.255.0
    - Gateway  192.168.200.1
    
    DNS
    
    - 192.168.200.1, 1.1.1.1
3. `set named.conf & named.conf.options` (ikuti server.world)
    
    `set named.conf.external-zoner` tambahkan `kelompokx.com` dan zone IP
    
    `set kelompokx.com` dan zone IP (TTL dst.)
    
4. `named-checkzone`
    
    `restart networking`
    
    `ping google.com`
    
    `ping kelompokx.com`
