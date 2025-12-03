**IPS (Intrusion Prevention System)** to dodatkowe urządzenie, które blokuje m.in. malware, ataki zero day etc. Potrafi ono zarówno wykrywać jak i na niego odpowiedzieć, np. odrzucić malicious pakiety. Wadą jest to, że wpływa na performance sieci - skan powoduje opóźnienia.

**Składa się z:**
1. IPS detection and enforcement engine
   >Przychodzący ruch jest porównywany z sygnaturami ataku zapisanymi w [[Sygnatury|attack signatures]] package
2. IPS attack signatures package
   >Komicznie wielka lista sygnatur ataku, porównywane z pakietami przechodzącymi przez IPS

#### Host-based IPS
Jest to software wgrany a hoście służący do analizy ruchu sieciowego wchodzącego do urządzenia. Pozwala na obronę tego hosta przed malware, wirusami, działa też trochę jak firewall. Jeśli jednak w sieci chcielibyśmy pełną obronę, musielibyśmy zainstalować taki IPS na każdym urządzeniu końcowym, gdzie może pojawić się problem związany z kompatybilnością z systemem operacyjnym. Host-based IPS też nie może zobaczyć całej sieci i zdarzeń się w niej dziejących, zatem nie daje pełnego obrazu sytuacji.

#### Network-based IPS
Może być zaimplementowany na urządzeniu z dodatkowym software IPS ([[Router jako IPS|jak router]]) lub dodatkowym dedykowanym sprzęcie. Poprzez rozstawienie sensorów w odpowiednich miejscach, pozwala na lepszą analizę i ochronę sieci. Pozwala na łatwiejszą rozbudowę sieci o nowsze hosty, zachowując przy tym bezpieczeństwo i dostępność. 