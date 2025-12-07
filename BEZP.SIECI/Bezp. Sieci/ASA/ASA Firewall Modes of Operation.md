### Routed mode

Dwa lub więcej interface oddzielają sieci (warstwa 3, domeny rozgłoszeniowe). Przejście przez ASA działa jak przejście przez router, wspierany jest NAT pomiędzy połączonymi sieciami. Każdy interface jest w innej podsieci i wymaga adresu IP z zakresu tej podsieci.

![[Pasted image 20251204161359.png]]
### Transparent mode

"Bump in the wire" - ASA działa jako urządzenie warstwy 2, przez co nie jest wykonywany odpowiednik przejścia przez router. Firewall ma wtedy adres IP tylko po to, by zarządzań nim zdalnie. Jest to teoretycznie wygodne, ale nie wspiera dynamicznego routingu, [[VPN]], QoS ani DHCP Relay.

![[Pasted image 20251204161541.png]]