---
tags:
  - konfiguracja
---
Standardowe [[Lista ACL|listy ACL]] składają się z ACE pozwalających filtrować ruch jedynie na podstawie źródłowego adresu IP pakietu. 

#### Przykładowy ACE do listy ACL standardowej:
```
R1(config)# access-list 10 permit 192.168.10.0 0.0.0.255
R1(config)#
```
- `access-list 10` to numer listy ACL - tutaj 10
- `permit` to zezwolenie, by ruch przeszedł dalej
- `192.168.10.0` to sieć z której ruch ma być zezwolony
- `0.0.0.255` to maska blankietowa, która mówi: "dowolne adresy, które zaczynają się na `192.167.10`, ostatni oktet może być czymkolwiek"

Czyli: "Zezwól przejść dalej ruchowi pochodzącemu z sieci `192.168.10.0/24`, odrzuć wszystko inne"

Standardowe listy ACL powinny być umieszczane jak najbliżej celu - dzięki temu nie zostanie odrzucony ruch przedwcześnie. Należy pamiętać, że są one w stanie filtrować ruch tylko na podstawie adresu źródłowego, czyli jeśli umieścilibyśmy taki ACL za blisko źródła, moglibyśmy przypadkiem odfiltrować CAŁY ruch pochodzący z tego źródła. Powoduje to, że filtrowanie samymi standardowymi ACL prowadzi do dużej ilości niepotrzebnego ruchu w sieci - pakiety muszą przedrzeć się przez całą sieć tylko po to, żeby zostać odrzuconymi tuż przed celem.   

![[Pasted image 20250509163427.png]]

Na przykładzie należy postawić listę ACL w miejscu zaznaczonym kółkiem - interfejs WYJŚCIOWY R3 do sieci `192.168.30.0/24`, czyli `g0/0/0` - by nie odrzucać przy okazji ruchu do sieci `192.167.31.0/24` jak przy umieszczeniu listy na interfejsie WEJŚCIOWYM routera (`s0/1/1`).

[[Numerowane standardowe listy ACL]] przyjmują numery z zakresu `1-99` oraz `1300-1999`.

[[Nazwane standardowe listy ACL]] mogą mieć dowolną nazwę, a przy ich tworzeniu używamy polecenia `ip access-list standard STD_NAME`. 