#TCP-CONNECT scan blokkolás (SYN csomagok; stealth scan vagy half-open scan; be nem fejezett TCP kapcsolódás)
iptables -A INPUT -p tcp --syn -j DROP

#TCP-SYN scan blokkolás (csak SYN csomagok)
iptables -A INPUT -m conntrack --ctstate NEW -p tcp --tcp-flags SYN,RST,ACK,FIN,URG,PSH SYN -j DROP

#TCP-FIN scan blokkolása (csak FIN csomagok)
iptables -A INPUT -m conntrack --ctstate NEW -p tcp --tcp-flags SYN,RST,ACK,FIN,URG,PSH FIN -j DROP

#TCP-ACK scan blokkolása (csak ACK csomagok)
iptables -A INPUT -m conntrack --ctstate NEW -p tcp --tcp-flags SYN,RST,ACK,FIN,URG,PSH ACK -j DROP


#TCP-NULL scan blokkolás (csomag jelzők nélkül)
iptables -A INPUT -m conntrack --ctstate INVALID -p tcp --tcp-flags ! SYN,RST,ACK,FIN,URG,PSH SYN,RST,ACK,FIN,URG,PSH -j DROP

#Block "Karácsonyfa" TCP-XMAS scan blokkoása (csomagok FIN, URG, PSH jelzővel)
iptables -A INPUT -m conntrack --ctstate NEW -p tcp --tcp-flags SYN,RST,ACK,FIN,URG,PSH FIN,URG,PSH -j DROP


#DOS - Teardrop blokkolása
iptables -A INPUT -p UDP -f -j DROP


#DDOS - Smurf blokkolása
iptables -A INPUT -m pkttype --pkt-type broadcast -j DROP
iptables -A INPUT -p ICMP --icmp-type echo-request -m pkttype --pkttype broadcast -j DROP
iptables -A INPUT -p ICMP --icmp-type echo-request -m limit --limit 3/s -j ACCEPT


#Block DDOS - Fraggle blokkolás
iptables -A INPUT -p UDP -m pkttype --pkt-type broadcast -j DROP
iptables -A INPUT -p UDP -m limit --limit 3/s -j ACCEPT


#DDOS - UDP-flood (Pepsi) blokkolás
iptables -A INPUT -p UDP --dport 7 -j DROP
iptables -A INPUT -p UDP --dport 19 -j DROP

#DDOS - SMBnuke blokkolás
iptables -A INPUT -p UDP --dport 135:139 -j DROP
iptables -A INPUT -p TCP --dport 135:139 -j DROP

#DDOS - Connection-flood blokkolás
iptables -A INPUT -p TCP --syn -m iplimit --iplimit-above 3 -j DROP


#DDOS - Jolt blokkolás
iptables -A INPUT -p ICMP -f -j DROP
