---
tags:
  - konfiguracja
---
Do stworzenia rozszerzonej nazwanej listy ACL posłuży polecenie:

`R1(config)#`**`ip access-list extended`** *`access-list-name`*
1. **`ip access-list`** - parametr obowiązkowy (**UWAGA - pojawia się słowo `ip`**)
2. **`extended`** - typ listy nazwanej, tutaj rozszerzona
3. *`access-list-name`* - nazwa listy ACL

To polecenie dopiero tworzy listę ACL, po wpisaniu go znak zachęty się zmieni na `R1(config-ext-nacl)#` i będzie można konfigurować kolejne ACE dotyczące tej listy - `deny`, `permit`, `remark` wraz z odpowiednimi parametrami jak w [[Numerowane rozszerzone listy ACL|numerowanych]] listach.

Największa różnica między nazwanymi a numerowanymi listami ACL jest to, że NAJPIERW tworzy się ACL, a dopiero POTEM dodaje kolejne zasady. Funkcjonalnie ostatecznie działa to tak samo.

___

Żeby zastosować rozszerzoną nazwaną listę ACL na interfejsie, należy wejść w interfejs na routerze i wydać polecenie:

`R1(config-if)#` **`ip access-group`** *`access-list-name`* **`{in | out}`**
1. **`ip access-group`** - parametr wymagany
2. *`access-list-name`* - nazwa listy ACL
3. a) **`in`** - zasada ma być zastosowana do [[Ruch wchodzący|ruchu wchodzącego]]
   b) **`out`** - zasada ma być zastosowana do [[Ruch wychodzący|ruchu wychodzącego]]

Do usunięcia zasady z interfejsu, wystarczy stary dobry `no`, konkretnie `no ip access-group`.

___

![[Pasted image 20250512191411.png]]

##### Konfiguracja - ruch wychodzący HTTP/HTTPS
```
R1(config)# ip access-list extended SURFING
R1(config-ext-nacl)# Remark Permits inside HTTP and HTTPS traffic
R1(config-ext-nacl)# permit tcp 192.168.10.0 0.0.0.255 any eq 80
R1(config-ext-nacl)# permit tcp 192.168.10.0 0.0.0.255 any eq 443
R1(config-ext-nacl)# exit
R1(config)#
```

##### Konfiguracja - ruch established
```
R1(config)# ip access-list extended BROWSING
R1(config-ext-nacl)# Remark Only permit returning HTTP and HTTPS traffic
R1(config-ext-nacl)# permit tcp any 192.168.10.0 0.0.0.255 established
R1(config-ext-nacl)# exit
```

##### Zastosowanie list do interfejsu - ruch wchodzący i wychodzący
```
R1(config)# interface g0/0/0
R1(config-if)# ip access-group SURFING in
R1(config-if)# ip access-group BROWSING out
R1(config-if)# end
```