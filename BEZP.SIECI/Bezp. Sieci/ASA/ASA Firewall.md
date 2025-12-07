**ASA (Adaptive Security Appliance)** to rodzina dedykowanych [[Architektura firewall|firewalli]] a nie sam moduł routera jak np. [[ZPF]]. Lepsze dla większych sieci. Wybór konkretnego modelu (np. Firepower 1000, 2100, 4100, 9300) ASA będzie zależał od zapotrzebowań i budżetu.

Np. Firepower 5500-X to stanowy firewall wspierający NGIPS, Advanced Malware Protection oraz Aplication control and URL filtering. Opcje wspierane na danym ASA będą zależały również od licencji.

Dedykowane firewalle traktuje interface "wewnętrzne" i połaczene z nimi sieci jako zaufane a wszystkie inne ("zewnętrzne") jako niezaufane. Każdy interface ma też powiązany ze sobą [[ASA security level]], na podstawie których implementowane są polityki. 

### Cechy ASA

Wspierane jest SDN z wirtualizacją sieci poprzez **ASAv**. Pojedynczy ASA może służyć jako kilka wirtualnych urządzeń, gdzie każde z nich jest określane jako "security context" - każde ma swoje zasady, interfejsy itd.

![[Pasted image 20251204160044.png]]

Kolejny feature ASA to high availability + failover - jak Firewall się zepsuje to ruch jest przeprowadzany przez zapasowy Firewall. Dwa identyczne ASA mogą zostać sparowane (active + standby). 

![[Pasted image 20251204160053.png]]

Dodatkowo, na ASA działa granularna kontrola dostępu na bazie tożsamości. Bazuje to na powiązaniu między adresem IP a Active Directory. 

![[Pasted image 20251204160135.png]]

Wszystkie modele ASA wspierają podstawowe [[IPS]], a część z nich wspiera też te bardziej rozwinięte poprzez integrację ze specjalnymi modułami - AIP. Ochrona przed malware jest wykonywana przez CSC. Jest wiele innych modułów.

![[Pasted image 20251204160450.png]]

