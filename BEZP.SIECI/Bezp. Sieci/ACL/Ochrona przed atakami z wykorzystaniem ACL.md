Dzięki głównie [[Rozszerzone ACL|rozszerzonym ACL]] można podnieść bezpieczeństwo swojej sieci, zapobiegając niektórym atakom.

#### Spoofing
Większość ataków DoS/DDoS to jakiś rodzaj spoofigu, na przykład adresu IP. Żeby ograniczyć takie przypadki, można zablokować dostęp z sieci zewnętrznej niektórym adresom - takim, których i tak być nie powinno "z zewnątrz". Są to:
- `0.0.0.0`
- adresy prywatne
- multicasty
- automatycznie wygenerowane adresy `169.254.0.0/16`
- broadcasty
- loopbacki

![[Pasted image 20251125154107.png]]

```
R1(config)# access-list 150 deny ip host 0.0.0.0 any  
R1(config)# access-list 150 deny ip 10.0.0.0 0.255.255.255 any
R1(config)# access-list 150 deny ip 127.0.0.0 0.255.255.255 any
R1(config)# access-list 150 deny ip 172.16.0.0 0.15.255.255 any
R1(config)# access-list 150 deny ip 192.168.0.0 0.0.255.255 any
R1(config)# access-list 150 deny ip 224.0.0.0 15.255.255.255 any
R1(config)# access-list 150 deny ip host 255.255.255.255 any
R1(config)# interface S0/0/0
R1(config-if)# ip access-group 150 in
```

#### Ograniczanie dostępu do usług
Jeśli przewidujemy wykorzystanie jedynie niektórych usług w naszej sieci, to wystarczy zablokować wszystko inne. Z koniecznych rzeczy mamy DNS, SSH, Syslog, może SNMP, wszystko inne jest opcjonalne i zależne od implementacji. Można tez ograniczyć usługi do konkretnych adresów w taki sposób, żeby np. tylko admin miał dostęp do protokołów zarządzania.

![[Pasted image 20251125154953.png]]

```
R1(config)# access-list 180 permit udp any host 192.168.20.2 eq domain  
R1(config)# access-list 180 permit tcp any host 192.168.20.2 eq smtp
R1(config)# access-list 180 permit tcp any host 192.168.20.2 eq ftp
R1(config)# access-list 180 permit tcp host 200.5.5.5 host 10.0.1.1 eq 22  
R1(config)# access-list 180 permit udp host 200.5.5.5 host 10.0.1.1 eq syslog
R1(config)# access-list 180 permit udp host 200.5.5.5 host 10.0.1.1 eq snmptrap
R1(config)# interface S0/0/0
R1(config-if)# ip access-group 180 in
```

#### Ataki na ICMP
ICMP echo może służyć do rekonesansu i floodowania - czyli DoS, a także przy pomocy ICMP redirect można modyfikować tablicę routingu. Z tego powodu warto jest zablokować te wiadomości "z zewnątrz". 
Wiele elementów ICMP za to jest potrzebnych do diagnostyki, np:
- ICMP Echo - ping, ale tylko na zewnątrz
- ICMP Echo Reply - odpowiedź na ICMP Echo, host z sieci może pingować na zewnątrz i ping wróci
- Source Quench - odpowiedź z prośbą o zmniejszenie prędkości wysyłania wiadomosci
- Różne błędy

![[Pasted image 20251125155455.png]]
**Z sieci "na zewnatrz":**
```
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any echo
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any parameter-problem
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any packet-too-big  
R1(config)# access-list 114 permit icmp 192.168.1.0 0.0.0.255 any source-quench
R1(config)# access-list 114 deny icmp any any
R1(config)# permit ip any any
R1(config)# interface G0/0
R1(config-if)# ip access-group 114 in
```

**"Z zewnątrz" do sieci:**
```
R1(config)# access-list 112 permit icmp any any echo-reply
R1(config)# access-list 112 permit icmp any any source-quench  
R1(config)# access-list 112 permit icmp any any unreachable
R1(config)# access-list 112 deny icmp any any  
R1(config)# access-list 112 permit ip any any
R1(config)# interface S0/0/0
R1(config-if)# ip access-group 112 in
```

#### Ataki na SNMP
Wyłącz go po prostu
```
Router(config)# no snmp-server
```
