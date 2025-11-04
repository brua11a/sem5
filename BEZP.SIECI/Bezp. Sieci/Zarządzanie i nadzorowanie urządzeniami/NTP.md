Czas można po prostu sobie ustawić manualnie (`clock set czas`), ale zazwyczaj lepiej jest mieć autorytet, który synchronizuje czas między urządzeniami. Temu służy chociażby **NTP** (*Network Time Protocol*). Klienci NTP są zsynchronizowani względem *autorytatywnego źródła*.

```
R1# show clock detail
20:55:10.207 UTC Fri Nov 15 2019
Time source is user configuration

R1(config)# ntp server 209.165.200.225
R1(config)# end
R1# show clock detail
21:01:34.563 UTC Fri Nov 15 2019
Time source is NTP
```

Źródła czasu w NTP są hierarchiczne, gdzie każdy poziom jest nazywany *stratum*. Każde *stratum* jest definiowane przez ilość skoków od *autorytatywnego źródła*.

**Stratum 0** oznacza autorytatywne źródło czasu. Mogą nim być zegarki GPS lub atomowe. Są najbardziej trafnym źródłem informacji o czasie. Nie są to koniecznie urządzenia sieciowe, lecz wyspecjalizowane urządzenia do mierzenia czasu.

**Stratum 1** składa się z urządzeń sieciowych bezpośrednio podłączonych do stratum 0. Są głównym standardem czasu dla urządzeń stratum 2.

**Stratum 2** to urządzenia sieciowe, które są klientami stratum 1 i serwerami dla stratum 3. I tak dalej.

Takich możliwych przeskoków 15, po 16 już nie ma synchronizacji.

```
R1# show ntp associations  
  address         ref clock       st   when   poll reach  delay  offset   disp
*~209.165.200.225 .GPS.           1     61     64   377  0.481   7.480  4.261
* sys.peer, # selected, + candidate, - outlyer, x falseticker, ~ configured
```

Urządzenie z poprzedniej konfiguracji korzysta z czasu nadanego przez serwer ze stratum 1 (ten bierze czas z GPS), ale...

```
R1# show ntp status
Clock is synchronized, stratum 2, reference is 209.165.200.225
nominal freq is 250.0000 Hz, actual freq is 249.9995 Hz, precision is 2**19
ntp uptime is 589900 (1/100 of seconds), resolution is 4016
```

...konfiguracja pokazuje, że ono samo jest w stratum 2. Kolejne urządzenia mogą korzystać z tego urządzenia jako z serwera NTP stratum 2, tym dołączając do stratum 3 itd.