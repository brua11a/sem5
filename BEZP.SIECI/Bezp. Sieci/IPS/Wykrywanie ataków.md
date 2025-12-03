Sam [[Architektura firewall|firewall]] może nie wystarczyć do ochrony sieci, zatem inne rozwiązanie może być warte rozważenia.

Jednym z pomysłów zapobiegania i wykrywania ataków może być manualne sprawdzanie logów na żywo przez administratora, ale źle się to skaluje i nie działa dobrze. Logi nadal są ważne, ale raczej do analizy później - co się stało i jak bardzo jest źle.

Zamiast tego stosuje się IPS i IDS. Obydwa mogą być routerem z odpowiednią konfiguracją, specjalnym urządzeniem lub modułem.

![[Pasted image 20251126115028.png]]

#### IDS
Samo wykrywanie powinno być automatyczne - przy pomocy **IDS (Intrustion Detection System)**, który analizuje kopię ruchu idącego do urządzenia końcowego. IDS analizując ruch szuka tzw. sygnatur, podobnie jak antywirus, ale działa offline. Zaletą tego rozwiązania jest to, że IDS nie wpływa na performance sieci. Niestety, potrafi ono jedynie wykrywać atak na kopii ruchu, a nie zapobiegać mu ani odpowiedzieć.
#### [[IPS]]
**IPS (Intrusion Prevention System)** to dodatkowe urządzenie, które blokuje m.in. malware, ataki zero day etc. Potrafi ono zarówno wykrywać jak i na niego odpowiedzieć, np. odrzucić malicious pakiety. Wadą jest to, że wpływa na performance sieci - skan powoduje opóźnienia.