Aby wykrywać anomalie w ruchu sieciowym, trzeba najpierw ustalić **baseline**, czyli wzorzec normalnego działania sieci. Wymaga to odpowiedniego monitorowania – punktem odniesienia mogą być m.in. [[Wykrywanie ataków|IDS]] lub [[SNMP]]
Zanim jednak ruch zostanie przeanalizowany, musi zostać przechwycony. W tym celu stosuje się dwa główne mechanizmy.
#### Network taps
[[Tryby pracy|Pasywne inline]] urządzenie, które przekazuje ruch **wraz z errorami** do urządzenia analitycznego, a jednocześnie nie blokuje normalnego ruchu. Nie wpływa na działanie sieci, a w razie awarii zostaje przezroczysty.
Do urządzenia monitorującego jest wysyłany zarówno *transmit* jak i *receive*, czyli analityk widzi na żywo ruch z obydwu stron.

![[Pasted image 20251127004236.png]]

#### Traffic mirroring, np. z Switch Port Analyzer
Pozwala na skopiowanie ramek otrzymanych na wybranych portach albo VLANach do innego portu SPAN. Źródeł może być wiele. Nie jest to osobne urządzenie a jedynie funkcja switcha.

![[Pasted image 20251127004720.png]]

Powiązanie pomiędzy source portem a destination portem to *SPAN session*. 

##### Konfiguracja
Określ jakie interfejsy będą źródłowe (będą z nich dane wysyłane do analizy) a który docelowy (będą do niego wysyłane zebrane dane).

![[Pasted image 20251127005925.png]]

```
S1(config)# monitor session 1 source interface fastethernet 0/1
S1(config)# monitor session 1 destination interface fastethernet 0/2
```

Do weryfikacji użyj `show monitor`

```
S1# show monitor
Session 1
---------
Type                   : Local Session
Source Ports           :  
    Both               : Fa0/1
Destination Ports      : Fa0/2
    Encapsulation      : Native
          Ingress      : Disabled
 
 
S1#
```