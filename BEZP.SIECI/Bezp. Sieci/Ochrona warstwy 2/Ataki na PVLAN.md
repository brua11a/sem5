### PVLAN Proxy Attack

![[Pasted image 20251129162110.png]]

Private VLAN (PVLAN) ma za zadanie izolować hosty znajdujące się w tym samym segmencie L2.  
Hosty typu **Isolated** nie powinny komunikować się bezpośrednio między sobą — mogą tylko z _promiscuous port_ (zwykle routerem).

Jednak sama konfiguracja PVLAN nie zapewnia pełnej izolacji, ponieważ możliwe jest ominięcie jej poprzez tzw. **PVLAN Proxy Attack**.

##### Opis ataku
1. **Isolated PC-A** tworzy pakiet IP do **Isolated PC-B**:
	- **IP źródłowe**: PC-A
	- **IP docelowe**: PC-B
2. W warstwie 2 atakujący celowo ustawia **MAC docelowy: MAC routera R1**  (czyli adres portu promiscuous)
3. Switch (S1), działając zgodnie z zasadą PVLAN pozwala na ruch Isolated -> Promiscuous więc **przekazuje ramkę do R1**, ignorując fakt, że IP docelowe należy do innego hosta isolated.
4. **Router R1** odbiera pakiet IP i **przełącza go jak normalny ruch L3** odbudowuje nową ramkę Ethernet **z MAC docelowym PC-B**
5. S1 widząc ramkę od routera (promiscuous -> isolated) **odsyła pakiet do PC-B**, mimo że PC-A i PC-B są w tej samej domenie isolated.

**Switch PVLAN nie widzi IP, a router nie widzi PVLAN, dlatego ten atak działa.**

Do zapobiegania temu atakowi wystarczy [[lista ACL]].

```
R1(config)# ip access-list extended PVLAN
R1(config-ext-nacl)# deny ip 172.16.0.0 0.0.0.255 172.16.0.0 0.0.0.255  
R1(config-ext-nacl)# permit ip any any
R1(config-ext-nacl)# interface g0/0
R1(config-if)# ip access-group PVLAN in
R1(config-if)#
```