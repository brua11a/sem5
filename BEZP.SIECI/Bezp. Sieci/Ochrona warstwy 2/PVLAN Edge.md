**[[Prywatne VLANy|PVLAN]] Edge** służy po to, by w niszowych przypadkach dwa urządzenia podłączone do tego samego switcha NIGDY nie wymieniały się ramkami - unicast, broadcast ani multicast.

**Protected Port** nigdy nie przekazuje ruchu do innego portu również oznaczonego jako protected port. Jedynie ruch kontrolny (control traffic) jest przekazywany. Ruch między protected portem a nie-protected portem działa normalnie.

![[Pasted image 20251129163725.png]]
#### Konfiguracja
Wystarczy na interfejsie wpisać:
> `S1(config-if) switchport protected`