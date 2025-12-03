---
tags:
  - konfiguracja
---
Do stworzenia standardowej nazwanej listy ACL posłuży polecenie:

`R1(config)#`**`ip access-list standard`** *`access-list-name`*
1. **`ip access-list`** - parametr obowiązkowy (**UWAGA - pojawia się słowo `ip`**)
2. **`standard`** - typ listy nazwanej, tutaj standardowa
3. *`access-list-name`* - nazwa listy ACL

To polecenie dopiero tworzy listę ACL, po wpisaniu go znak zachęty się zmieni na `R1(config-std-nacl)#` i będzie można konfigurować kolejne ACE dotyczące tej listy - `deny`, `permit`, `remark` wraz z odpowiednimi źródłowymi adresami IP i maskami blankietowymi jak w [[Numerowane standardowe listy ACL|numerowanych]] listach. 

Największa różnica między nazwanymi a numerowanymi listami ACL jest to, że NAJPIERW tworzy się ACL, a dopiero POTEM dodaje kolejne zasady. Funkcjonalnie ostatecznie działa to tak samo.

___

Żeby zastosować standardową nazwaną listę ACL na interfejsie, należy wejść w interfejs na routerze i wydać polecenie:

`R1(config-if)#` **`ip access-group`** *`access-list-name`* **`{in | out}`**
1. **`ip access-group`** - parametr wymagany
2. *`access-list-name`* - nazwa listy ACL
3. a) **`in`** - zasada ma być zastosowana do [[Ruch wchodzący|ruchu wchodzącego]]
   b) **`out`** - zasada ma być zastosowana do [[Ruch wychodzący|ruchu wychodzącego]]

Do usunięcia zasady z interfejsu, wystarczy stary dobry `no`, konkretnie `no ip access-group`.

___

![[Pasted image 20250512172434.png]]

##### Konfiguracja przykładowego ACL:
```
R1(config)# ip access-list standard PERMIT-ACCESS
R1(config-std-nacl)# remark ACE pozwala przejsc do Internetu hostowi 192.168.10.10
R1(config-std-nacl)# permit host 192.168.10.10
R1(config-std-nacl)# remark ACE pozwala przejsc do Internetu kazdemu w LAN 2
R1(config-std-nacl)# permit 192.168.20.0 0.0.0.255
R1(config-std-nacl)# exit
R1(config)#
```

##### Zastosowanie go na interfejsie:
```
R1(config)# interface Serial 0/1/0
R1(config-if)# ip access-group PERMIT-ACCESS out
R1(config-if)# end
R1#
```