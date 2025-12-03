Router można skonfigurować tak, aby działał jednocześnie jako klasyczny router oraz jako [[Tryby pracy|Inline]] Network [[IPS]].  
Takie rozwiązanie pozwala obniżyć koszty oraz ułatwia projektowanie infrastruktury.

W tym trybie router może m.in.:
- wysyłać logi do serwera [[syslog]],
- odrzucać pakiety,
- resetować połączenia,
- blokować źródła ruchu

### Cisco IPS (starsze rozwiązanie)

Cisco IPS to wcześniejsza technologia stosowana przez Cisco. Działała bezpośrednio w systemie operacyjnym urządzenia i **współdzieliła zasoby** z pozostałymi funkcjami routera.

### Cisco/External [[Snort IPS]] (nowsze rozwiązanie)

Obecnie zamiast Cisco IPS używa się głównie **Snort IPS**. Największa różnica to to, że **Snort Engine** uruchamia _virtual service container_ - czyli odizolowaną maszynę/kontener działający na routerze, w której wykonywane są operacje IPS

W przeciwieństwie do Cisco IPS, Snort w tym modelu **nie współdzieli zasobów** z resztą systemu, co poprawia stabilność, wydajność i bezpieczeństwo. Snort może działać jako IPS lub IDS, zależy od konfiguracji.

![[Pasted image 20251126124600.png]]

External Snort IPS Server rózni się od tego Ciscowego tym, że wymaga [[Tryby pracy|promiscuous mode]] i zewnętrznego Snort IDP/IPS