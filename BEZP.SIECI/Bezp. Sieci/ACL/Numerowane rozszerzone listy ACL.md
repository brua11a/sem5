---
tags:
  - konfiguracja
---
Do stworzenia rozszerzonej numerowanej listy ACL posłuży polecenie:

`R1(config)#`**`access-list`** *`access-list-number`* **`{deny | permit | remark}`** *`protocol source source-wildcard [operator {port}] destination destination-wildcard [operator {porty}]`* **`[established] [log]`**
1. **`access-list`** - parametr obowiązkowy
2. *`access-list-number`* - numer z zakresu 100-199 lub 2000-2699, określa listę ACL której dotyczy ten konkretny ACE
3. a) **`deny`** - jeśli warunek został spełniony, przepuść dalej
   b) **`permit`** - jeśli warunek został spełniony, odrzuć ruch
   c) **`remark`** *`text`* - opcjonalnie dodaj tekst opisujący ten fragment ACL, kończy polecenie
4. ==*`protocol`* - nazwa lub numer typu protokołu sieciowego, zazwyczaj `tcp` (6), `udp` (17) lub `ip` (dla `ip` dotyczy całego ruchu sieciowego, można rozumieć jako "dowolny protokół sieciowy")==
5. *`source`* - adres IP źródła, na podstawie którego ruch jest akceptowany lub odrzucany, można użyć słowa `any` lub `host` w tym miejscu
6. *`source-wildcard`* - maska blankietowa stosowana do adresu źródła określająca zakres adresów, którego dotyczy ten ACE
7. ==*`operator`* - porównuje porty źródłowe i/lub docelowe, żeby były mniejsze (`lt`), większe (`gt`), równe (`eq`), nierówne (`neq`) czemuś lub w jakimś `range` (zakres domknięty)==
8. ==*`port`* - numer lub nazwa portu TCP lub UDP (np. `http` albo `80`)==
9. ==*`destination`* - adres IP docelowy, na podstawie którego ruch jest akceptowany lub odrzucany, można użyć słowa `any` lub `host` w tym miejscu==
10.  ==*`destination-wildcard`* - maska blankietowa stosowana do adresu docelowego określająca zakres adresów, którego dotyczy ten ACE==
11. ==*`operator`* - porównuje porty źródłowe i/lub docelowe, żeby były mniejsze (`lt`), większe (`gt`), równe (`eq`), nierówne (`neq`) czemuś lub w jakimś `range` (zakres domknięty)==
12. ==*`port`* - numer lub nazwa portu TCP lub UDP (np. `http` albo `80`)==
13. ==**`established`** - w ruchu TCP pozwala na powrót ruchu, który wyszedł nie pozwalając jednocześnie wejść tak o od zewnątrz (wyjaśnione lepiej [[Established TCP|tutaj]])==
14. **`log`** - pozwala logować momenty, w których ACE zostaje dopasowany (czyli adres z zakresu określonego w ACL próbował się przedostać przez router)

W przeciwieństwie do standardowych list, gdzie określana jest tylko sieć źródłowa, tutaj dodatkowo określany jest protokół, port źródłowy (chociaż ten dużo rzadziej), sieć docelowa, port docelowy (ten dużo częściej), a dodatkowo ewentualnie czy ruch jest `established`.

Jeśli w ten sposób konfigurujemy listę ACL, musimy za każdym razem jasno podawać której listy dotyczy polecenie. Dodatkowo, należy pamiętać o zakresach, żeby nie zrobić przypadkiem listy standardowej lub vice versa.

___

Żeby zastosować rozszerzoną numerowaną listę ACL na interfejsie, należy wejść w interfejs na routerze i wydać polecenie:

`R1(config-if)#` **`ip access-group`** *`access-list-number`* **`{in | out}`**
1. **`ip access-group`** - parametr wymagany
2. *`access-list-number`* - numer listy ACL
3. a) **`in`** - zasada ma być zastosowana do [[Ruch wchodzący|ruchu wchodzącego]]
   b) **`out`** - zasada ma być zastosowana do [[Ruch wychodzący|ruchu wychodzącego]]

Do usunięcia zasady z interfejsu, wystarczy stary dobry `no`, konkretnie `no ip access-group`.

___

![[Pasted image 20250512183609.png]]

##### Przykładowa konfiguracja:
```
R1(config)# access-list 110 permit tcp 192.168.10.0 0.0.0.255 any eq www
R1(config)# access-list 110 permit tcp 192.168.10.0 0.0.0.255 any eq 443
R1(config)# interface g0/0/0
R1(config-if)# ip access-group 110 in
R1(config-if)# exit
R1(config)#
```