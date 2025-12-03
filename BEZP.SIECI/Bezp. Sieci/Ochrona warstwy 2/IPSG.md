Służy do zapobieganiu [[Bezpieczeństwo warstwy 2|address spoofingowi]]. Działa podobnie do [[DAI]], ale ocenia każdy pakiet, a nie tylko pakiety ARP. Ponownie jak DAI, **IPSG (IP Source Guard)** również wymaga włączonego [[DHCP snooping]]. 

IPSG zazwyczaj ustawia się na niezaufanym portom dostępowym i trunk. Na początku cały ruch poza DHCP jest blokowany, aż powstanie przypisanie adresu do portu - PVACL (Per-Port VLAN ACL). Przypisanie powstaje gdy zostanie skonfigurowane manualnie albo serwer DHCP przyzna poprawny adres. Każdy adres poza tym z **przypisanym adresem IP (ewentualnie też MAC)** zostanie zablokowany.

### Konfiguracja

![[Pasted image 20251129212415.png]]

```
*** włączony wcześniej DHCP snooping globalnie
S1(config)# interface range fastethernet 0/1 - 2
S1(config-if-range)# ip verify source
S1(config-if-range)# end
S1#
```

