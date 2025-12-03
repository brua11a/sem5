---
tags:
  - konfiguracja
---
[[Lista ACL|Listy ACL]] mogą też służyć do filtrowania ruchu pochodzącego z portów VTY, żeby ograniczyć zdalny dostęp administracyjny. Może to być dowolny typ listy. Żeby je zastosować, należy wybrać konkretne linie VTY (zazwyczaj po prostu wszystkie) i wydać na nich polecenie:

`R1(config-line)#`**`access-class`** *`{access-list-number | access-list-name}`* **`{in | out}`**
1. **`access-class`** - parametr obowiązkowy
2. a) *`access-list-number`* - numer listy ACL
   b) *`access-list-name`* - nazwa listy ACL
3. a) **`in`** - zasada ma być zastosowana do [[Ruch wchodzący|ruchu wchodzącego]] (prawie zawsze używana jest ta opcja)
   b) **`out`** - zasada ma być zastosowana do [[Ruch wychodzący|ruchu wychodzącego]]