---
tags:
  - konfiguracja
---
Do stworzenia standardowej numerowanej listy ACL posłuży polecenie:

`R1(config)#`**`access-list`** *`access-list-number`* **`{deny | permit | remark}`** *`source [source-wildcard]`* **`[log]`**
1. **`access-list`** - parametr obowiązkowy
2. *`access-list-number`* - numer z zakresu 1-99 lub 1300-1999, określa listę ACL której dotyczy ten konkretny ACE
3. a) **`deny`** - jeśli warunek został spełniony, przepuść dalej
   b) **`permit`** - jeśli warunek został spełniony, odrzuć ruch
   c) **`remark`** *`text`* - opcjonalnie dodaj tekst opisujący ten fragment ACL, kończy polecenie
4. *`source`* - adres IP źródła, na podstawie którego ruch jest akceptowany lub odrzucany, można użyć słowa `any` lub `host` w tym miejscu
5. *`source-wildcard`* - maska blankietowa stosowana do adresu źródła określająca zakres adresów, którego dotyczy ten ACE
6. **`log`** - pozwala logować momenty, w których ACE zostaje dopasowany (czyli adres z zakresu określonego w ACL próbował się przedostać przez router)

Jeśli w ten sposób konfigurujemy listę ACL, musimy za każdym razem jasno podawać której listy dotyczy polecenie. Dodatkowo, należy pamiętać o zakresach, żeby nie zrobić przypadkiem listy rozszerzonej lub vice versa.

___

Żeby zastosować standardową numerowaną listę ACL na interfejsie, należy wejść w interfejs na routerze i wydać polecenie:

`R1(config-if)#` **`ip access-group`** *`access-list-number`* **`{in | out}`**
1. **`ip access-group`** - parametr wymagany
2. *`access-list-number`* - numer listy ACL
3. a) **`in`** - zasada ma być zastosowana do [[Ruch wchodzący|ruchu wchodzącego]]
   b) **`out`** - zasada ma być zastosowana do [[Ruch wychodzący|ruchu wychodzącego]]

Do usunięcia zasady z interfejsu, wystarczy stary dobry `no`, konkretnie `no ip access-group`.

___

![[Pasted image 20250512173320.png]]

##### Konfiguracja przykładowego ACL:
```
R1(config)# access-list 10 remark ACE pozwala tylko 192.168.10.10 na dostęp do Internetu
R1(config)# access-list 10 permit host 192.168.10.10
R1(config)# access-list 10 remark ACE pozwala wszystkim hostom w LAN 2 na dostęp do Internetu
R1(config)# access-list 10 permit 192.168.20.0 0.0.0.255
R1(config)#
```

##### Zastosowanie go na interfejsie:
```
R1(config)# interface Serial 0/1/0
R1(config-if)# ip access-group 10 out
R1(config-if)# end
R1#
```