Pozwala ograniczyć [[Ataki na ARP|zatrucie i fałszowanie ARP]]. Wymaga włączonego [[DHCP snooping]] globalnie i na VLAN. Dopiero, gdy na wybranych portach jest włączony DHCP snooping, można skonfigurować DAI. Trzeba wyznaczyć zaufane interfejsy. Rule of thumb - porty do urządzeń końcowych są niezaufane. 

![[Pasted image 20251129211900.png]]

```
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# ip arp inspection vlan 10
S1(config)# interface fa0/24
S1(config-if)# ip dhcp snooping trust
S1(config-if)# ip arp inspection trust
```

DAI można konfigurować tak, by sprawdzał:
* **Docelowy MAC** (`dst-mac`) - sprawdza, czy docelowy MAC w nagłówku Ethernet odpowiada docelowemu MAC w wiadomości ARP.
* **Źródłowy MAC** (`src-mac`) - sprawdza, czy adres MAC źródłowy w nagłówku Ethernet odpowiada adresowi źródłowemu MAC nadawcy w wiadomości ARP.
* **Adres IP** (`ip`) - sprawdza komunikat ARP pod kątem nieprawidłowych i nieoczekiwanych adresów IP, w tym adresów 0.0.0.0, 255.255.255.255 i wszystkich adresów multicastowych IP.

Jedną lub więcej z tych opcji wybierasz poprzez `ip arp inspection validate`. Robisz to globalnie dla całego urządzenia. Żeby wybrać kilka na raz, napisz je w jednej linijce.