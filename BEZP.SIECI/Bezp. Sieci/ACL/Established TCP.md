---
tags:
  - konfiguracja
---
TCP podtrzymuje połączenie i może pełnić rolę zapory stanowej dzięki słowu kluczowemu **`established`**. Dzięki niemu jeśli ruch TCP wyjdzie z routera, to może do niego wrócić, ale nie daje to jednocześnie wstępu z zewnątrz pozostałym pakietom.

Ruch wygenerowany z hosta z zewnątrz nie dotrze do sieci wewnętrznej, ale ruch wygenerowany w sieci wewnętrznej dosięgnie hosta z zewnątrz i wróci bez problemu.

![[Pasted image 20250512184141.png]]

```
R1(config)# access-list 120 permit tcp any 192.168.10.0 0.0.0.255 established
R1(config)# interface g0/0/0
R1(config-if)# ip access-group 120 out
R1(config-if)# end
R1# show access-lists
Extended IP access list 110
     10 permit tcp 192.168.10.0 0.0.0.255 any eq www
     20 permit tcp 192.168.10.0 0.0.0.255 any eq 443 (657 matches)
Extended IP access list 120
     10 permit tcp any 192.168.10.0 0.0.0.255 established (1166 matches)
R1#
```

ACL 110 pozwala wyjść z sieci dowolnemu ruchowi do dowolnej sieci i portu `www`, a ACL 120 pozwala mu wrócić. Bez słowa `established` ta zasada pozwalałaby każdemu ruchowi TCP wejść do sieci wewnętrznej LAN 1.