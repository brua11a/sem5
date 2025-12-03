---
tags:
  - konfiguracja
---
Rozszerzone [[Lista ACL|listy ACL]] składają się z ACE pozwalających filtrować ruch na podstawie źródłowego i docelowego adresu IP, a także typu protokołu, źródłowego i docelowego portu i więcej. Wszystko, co da się zrobić [[Standardowe ACL|standardowymi ACL]] da się zrobić rozszerzonymi, ale rozszerzone listy potrafią o wiele więcej, zatem są częściej używane. 

#### Przykładowy ACE do listy ACL Rozszerzonej:
```
R1(config)# access-list 100 permit tcp 192.168.10.0 0.0.0.255 any eq www
R1(config)#
```
- `access-list 100` to numer listy ACL - tutaj 100
- `permit` to zezwolenie, by ruch przeszedł dalej
- `tcp` określa typ protokołu
- `192.168.10.0` to sieć z której ruch ma być zezwolony
- `0.0.0.255` to [[maska blankietowa]], która mówi: "dowolne adresy, które zaczynają się na `192.167.10`, ostatni oktet może być czymkolwiek"
- `any` to sieć, do której ruch ma być zezwolony, czyli określa adres docelowy, alias `any` odpowiada `[cokolwiek] 255.255.255.255`
- `eq www` określa port docelowy, tutaj HTTP (`80`)

Czyli: "Zezwól przejść dalej ruchowi pochodzącemu z sieci `192.168.10.0/24` idącego do dowolnej sieci (`any`) jeśli jego docelowy port to `80`, odrzuć wszystko inne" 

Rozszerzone ACL powinny być umieszczane jak najbliżej źródła. Dzięki możliwości określenia adresu docelowego, portu itd. można odciąć niepożądany ruch od razu zanim zbliży się do celu tym samym nie kompromitując pozostałych pakietów. 

![[Pasted image 20250509164029.png]]

Na przykładzie tutaj jest kilka rozwiązań i wiele z nich będzie poprawne, ale najlepszym jest postawienie ACL na interfejsie WCHODZĄCYM do R1 z sieci `192.168.11.0/24` żeby nie filtrować niepotrzebnie ruchu, dla którego nie przewidujemy filtrów jak przy postawieniu ACL na interfejsie WYCHODZĄCYM z routera - dla tego rozwiązania należałoby dodatkowo dodać coś w stylu `permit ip any any` by nie blokować pozostałego ruchu, a tylko FTP i TELNET z `192.168.11.0/24` do `192.168.30.0/24`.

[[Numerowane rozszerzone listy ACL]] przyjmują numery z zakresu `100-199` oraz `2000-2699`.

[[Nazwane rozszerzone listy ACL]] mogą mieć dowolną nazwę, a przy ich tworzeniu używamy polecenia `ip access-list extended EXT_NAME`. 