Obok [[Szyfrowanie haseł|zaszyfrowania haseł]] można rozważyć dodatkowe opcje, które są zalecane lecz nie-niezbędne.

#### Długość haseł
Można ustawić minimalną długość haseł na urządzeniu przy pomocy:
> `R1(config)#`**`security passwords min-length`** *`length`*

Gdzie zazwyczaj *`length`* to 8 lub 10, w zależności od company policy.
#### Blokada po nieudanych logowaniach
Pozwala spowolnić ataki brute force. Działa w "Normal mode" - router liczy ilość nieudanych loginów w określonymzakresie czasu. Można ją ustawić na urządzeniu przy pomocy:
> `R1(config)#` **`login block-for`** *`seconds`* **`attempts`** *`number`* **`within`** *`seconds`*

| Tłumaczenie                | Fragment komendy                  |
| -------------------------- | --------------------------------- |
| Zablokuj na:               | **`login block-for`** *`seconds`* |
| Po ilości nieudanych prób: | **`attempts`** *`number`*         |
| Wykonanych w przeciągu:    | **`within`** *`seconds`*          |
Bez tej komendy pozostałe komendy "wzmacniające" `login` nie zadziałają, zatem jest ona konieczna.

#### Quiet mode
Przy próbie logowania zdalnego pozwala ona na zweryfikowanie adresu źródłowego i porównanie go z dostępną listą ACL, w której będą zezwolone zakresy adresów.

Jeśli ilość nieudanych loginów przekroczy pewną granicę, WSZYSTKIE próby logowanie (Telnetem, SSH, HTTP) są zablokowane na czas określony w `login block-for`. Żeby jednak nie blokować administratorów, można określić listę dozwolonych adresów jako ACL.

> `Router(config)#` **`login quiet-mode access-class`** *`{  acl-name | acl-number  }`*

```
R1(config)# ip access-list standard PERMIT-ADMIN       
R1(config-std-nacl)# remark Permit only Administrative hosts  
R1(config-std-nacl)# permit 192.168.10.10                      
R1(config-std-nacl)# permit 192.168.11.10
R1(config-std-nacl)# exit
R1(config)# login quiet-mode access-class PERMIT-ADMIN
```

#### Delay
Określa długość przerwy pomiędzy nieudanymi logowaniami. Domyślnie jest to 1 sekunda. 
> `Router(config)#` **`login delay`** *`seconds

Pozwala na zapobieganie atakom słownikowym.
#### On-success / On-failure
Logowanie udanych i nieudanych prób logowania
>`Router(config)#` **`login on-success log`** `[`**`every`** *`login`*`]`
>`Router(config)#` **`login on-failure log`** `[`**`every`** *`login`*`]`

Dzięki temu można zobaczyć czy ktoś rzeczywiście próbuje "dobić" się do naszej sieci.

Dodatkowo, można wygenerować log gdy liczba nieudanych loginów przekroczy pewną granicę.

> `Router(config)#` **`security authentication failure rate`** *`threshold-rate`* **`log`**

***log***: Syslog authentication failures if the rate exceeds the threshold

Czyli osobny log gdy będzie po prostu failure i osobny log gdy będzie więcej failure niż przewidział threshold.

#### Timeout
Zapobiega sytuacjom, w których administrator zostawia odpalony terminal i go nie pilnuje - jest to potencjalne zagrożenie gdyby ktoś niepowołany uzyskał do niego fizyczny dostęp. 
Domyślny timeout to 10 minut, ale można go zmienić przy pomocy:
> `R1(config-line)#` **`exec-timeout`** *`minutes seconds`*

Tę komendę można wykonać na liniach konsolowych, vty i aux, ale (*raczej*) nie w ogólnej konfiguracji (w przeciwieństwie do dwóch poprzednich)

### Przykłady
```
R1(config)# service password-encryption
R1(config)# security passwords min-length 8
R1(config)# login block-for 120 attempts 3 within 60
R1(config)# line vty 0 4
R1(config-line)# password cisco123
R1(config-line)# exec-timeout 5 30
R1(config-line)# transport input ssh
R1(config-line)# end
R1#
R1# show running-config | section line vty
line vty 0 4
  password 7 094F471A1A0A
  exec-timeout 5 30
  login
  transport input ssh
R1#
```

Hasła zostały zaszyfrowane słabym algorytmem, minimalna długość hasła to 8 znaków, po 3 próbach nieudanego logowania w przeciągu 60s jest wykonywana blokada na 120s, a na liniach vty 0 4 po 5min30s nieaktywności dochodzi do automatycznego wylogowania. 


```
R1(config)# login block-for 15 attempts 5 within 60
R1(config)# ip access-list standard PERMIT-ADMIN
R1(config-std-nacl)# remark Permit only Administrative hosts    
R1(config-std-nacl)# permit 192.168.10.10
R1(config-std-nacl)# permit 192.168.11.10
R1(config-std-nacl)# exit
R1(config)# login quiet-mode access-class PERMIT-ADMIN   
R1(config)# login delay 10
R1(config)# login on-success log
R1(config)# login on-failure log
R1(config)#
```

Po 5 nieudanych próbach logowania w przeciągu 60 sekund dostęp do urządzenia zostanie zablokowany dla WSZYSTKICH POZA adresami określonymi w liście ACL PERMIT-ADMIN (`192.168.10.10` i `192.168.11.10`). Dodatkowo, pomiędzy próbami logowania jest 10s przerwa oraz logowane są zarówno udane jak i nieudane próby uwierzytelnienia.