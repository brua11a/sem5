Największa różnica pomiędzy ASA ACL a tymi [[Lista ACL|zwykłymi]] to to, że używane są normalne maski zamiast maski blankietowej, a także listy są zdecydowanie częściej nazwane a nie numerowane.

ACL na ASA mogą służyć do filtrowania zarówno ruchu ruchu "przechodzącego" przez firewall (**Through-traffic filtering**) ale także ruchu skierowanego do tego firewall (**To-the-box-traffic filtering**, management access rule).

Dodatkowo, należy pamietać o [[ASA security level]], które same w sobie już blokują już zezwalają na ruch nawet bez jakiejkolwiek ACL - domyślnie ruch z niskiego do wysokiego security nie jest dozwolony, ale w drugą stronę tak. 

#### Typy ASA ACL
1. **Rozszerzone ACL.**
   >Najczęstszy typ. Takie same jak zwykłe [[nazwane rozszerzone listy ACL]]. Uzywany do kontroli dostępu, zasad [[AAA]], rozpoznawania adresów w NAT, ustanowienia dostępu [[VPN]], rozpoznawania ruchu do MPF
   >
   >![[Pasted image 20251206170324.png]]
   >
   >Z wykorzystaniem [[Object Groups]], synthax zmienia się:
   >
   >![[Pasted image 20251206171211.png]]
   >![[Pasted image 20251206171620.png]]
   >```
   >NETSEC-ASA(config)# object-group network NET-HOSTS  
NETSEC-ASA(config-network-object-group)# description OG matches PC-A and PC-B  
NETSEC-ASA(config-network-object-group)# network-object host 209.165.201.1  
NETSEC-ASA(config-network-object-group)# network-object host 209.165.201.2  
NETSEC-ASA(config-network-object-group)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# object-group network SERVERS  
NETSEC-ASA(config-network-object-group)# description OG matches Web / Email Servers  
NETSEC-ASA(config-network-object-group)# network-object host 209.165.202.131  
NETSEC-ASA(config-network-object-group)# network-object host 209.165.202.132  
NETSEC-ASA(config-network-object-group)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# object-group service HTTP-SMTP tcp  
NETSEC-ASA(config-service-object-group)# description OG matches SMTP / WEB traffic  
NETSEC-ASA(config-service-object-group)# port-object eq smtp  
NETSEC-ASA(config-service-object-group)# port-object eq www  
NETSEC-ASA(config-service-object-group)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# access-list ACL-IN remark Only permit PC-A / PC-B -> Internal Servers  
NETSEC-ASA(config)# access-list ACL-IN extended permit tcp object-group NET-HOSTS object-group SERVERS object-group HTTP-SMTP
NETSEC-ASA(config)# access-group ACL-IN in interface OUTSIDE
   >```
1. **Standardowe ACL**
   >UWAGA: nie określa adresu źródłowego jak normalne [[standardowe ACL]] tylko adres DOCELOWY. Najczęściej używany w OSPF lub filtrach [[VPN]]. Nie można ich używać do filtrowania ruchu na interface.
2. **EtherType ACL**
   >Może zostać skonfigurowane jedynie jeśli ASA pracuje w trybie [[ASA Firewall Modes of Operation|transparentnym]]
3. **Webtype ACL**
   >Do filtrowania ruchu clientless [[SSL TLS]] [[VPN]]. Blokuje na podstawie np. URL lub adresów docelowych.
4. **IPv6 ACL**
   >Do filtrowania dostępu ruchu sieciowego IPv6

#### Aplikowanie ACL
> `ciscoasa(config)# access-group id { in | out } interface if_name [ per-user-override | control-plane ]`

![[Pasted image 20251206170905.png]]

Należy zwrócić uwagę na to, że operacja jest wykonywana w konfiguracji globalnej a nie interface
