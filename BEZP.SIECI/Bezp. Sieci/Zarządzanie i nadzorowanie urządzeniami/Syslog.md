Pozwala na zcentralizowane zarządzanie logami - serwer syslog może zbierać wiadomości wysyłane przez urządzenia w sieci - mniej lub bardziej krytyczne. 

Można też wysyłać logi "do samego siebie", do wewnętrznego buffera, aby przeczytać je przez CLI na urządzeniu.

Można też zrobić tak, że część wiadomości jest wysyłana, a część przechowywana - wszystko zależy od konfiguracji. Zazwyczaj wyznacznikiem tego, co wysyłać a co nie jest *severity level*.

| Severity      | Numer |
| ------------- | ----- |
| Emergency     | 0     |
| Alert         | 1     |
| Critical      | 2     |
| Error         | 3     |
| Warning       | 4     |
| Notification  | 5     |
| Informational | 6     |
| Debugging     | 7     |
Poziomy 0-4 to błędy software i hardware, czyli wpływające negatywnie na działanie urządzenia.
Poziom 5 to ważne, ale normalne eventy, takie jak włączenie lub wyłączenie interfejsu.
Poziom 6 to po prostu informacje.
Poziom 7 zwraca informacje wygenerowane poprzez komendy z `debug`

Przykładowy syslog informujący o tym, że łącze EtherChannel zostało włączone może wyglądać tak:

```
%LINK-3-UPDOWN: Interface Port-channel1, changed state to up
```

Gdzie `LINK` to obiekt/facility code, `3` to poziom ważności, zaś `UPDOWN` to _nazwa mnemoniczna obiektu

W logach nie ma domyślnie czasu, można to zmienić komendą `service timestamps log datetime`, ale zadziała to tylko jeśli ustawimy jawnie zegar ręcznie albo poprzez [[NTP]].

```
R1# configure terminal
R1(config)# interface g0/0/0
R1(config-if)# shutdown
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to administratively down
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to down
R1(config-if)# exit
R1(config)# service timestamps log datetime
R1(config)# interface g0/0/0
R1(config-if)# no shutdown
*Mar  1 11:52:42: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to down
*Mar  1 11:52:45: %LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up
*Mar  1 11:52:46: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0,
changed state to up
R1(config-if)#
```

### Wysyłanie logów do serwera
1. `Router(config)#` **`logging host`** *`hostname/ip-addr`*
   > Określa dokąd logi maja być wysyłane (do serwera syslog)
2. *Opcjonalne:* `Router(config)#` **`logging trap`** `level`
   >Określa od którego severity level w dół mają być wysyłane logi na podany wcześniej adres (domyślnie jest to *debugging*, czyli wysyłane jest WSZYSTKO, zakres 0-7)
3. *Opcjonalne:* `Router(config)#` **`logging source-interface`** *`interface`*
   >Nadaj pakietom syslog określony adres źródłowy NIEWAŻE JAKI ON BĘDZIE W RZECZYWISTOŚCI
4. *Opcjonalne:* `Router(config)#` **`logging on`**
   >Domyślnie włączone, ale można być explicit.