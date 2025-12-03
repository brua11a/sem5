Warstwa 2 jest ogólnie wąskim gardłem jeśli chodzi o zabezpieczenia, a kompromitacja warstwy 2 jest jednoznaczna z kompromitacją wszystkich wyższych (3-7). Ataków na nią jest tak dużo, że powstały całe kategorie.

| **Kategoria**                                          | **Przykład**                                          |
| ------------------------------------------------------ | ----------------------------------------------------- |
| [[Ataki na tablicę adresów MAC\|Ataki na tablice MAC]] | Zalewanie adresami MAC                                |
| [[Ataki na sieci VLAN]]                                | Ataki z przeskokiem VLAN i podwójnym znakowaniem VLAN |
| [[Ataki na DHCP]]                                      | Blokowanie i fałszowanie DHCP                         |
| [[Ataki na ARP]]                                       | ARP spoofing i zatrucie ARP                           |
| [[Ataki z podszywaniem się]]                           | Fałszowanie adresów MAC i IP                          |
| [[Ataki na STP]]                                       | Manipulacja STP                                       |
##### Ogólne, zawsze działające zasady:
1. **[[Zabezpieczanie portów|Zabezpieczaj porty]]**
   >Ogranicza zalewanie MAC i zagłodzenie DHCP
2. **DHCP Snooping** 
   >Zapobiega zagłodzeniu DHCP i podszywaniu się DHCP
3. **DAI (*Dynamic ARP Inspection*)**
   >Zapobiega fałszowaniu ARP i zatruciu ARP
4. **IPSG (*IP Source Guard*)**
   >Zapobiega fałszowaniu MAC i IP
5. **Używaj bezpiecznych wariantów protokołów (z S jak Secure w nazwie)**
   >SSH, SFTP, SSL...
6. ***Rozważ użycie sieci zarządzania poza pasmem do zarządzania urządzeniami.***
7. **Miej dedykowany VLAN do zarządzania**
8. **Używaj ACL (*Access Control Lists*)**
9. OGRANICZ UŻYCIE [[CDP]]!!!
