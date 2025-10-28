Systemy krótkozasięgowe pracują w pasmach takich, jak na slajdzie.
Są to pasma ISM - pasma przemysłowe, naukowe i medyczne, nielicencjonowane.
1. RFID (13553 kHz, błąd na slajdzie)
2. IoT (LPWAN, SRD)
3. WLAN, Bluetooth, ZigBee
Dwa pierwsze pasma są dość wąskie (13-14kHz, 3MHz), zatem te systemy nie będą bardzo wydajne - twierdzenie Shannona - "jeśli mamy kanał o pewnej szerokości pasma to można na tego podstawie policzyć z jaką maksymalnie szybkością można wysyłać bezbłędnie informacje". 
W pozostałych pasmo ma szerokość 100MHz lub 150MHz - w tych systemach jest "tłoczno", dlatego dla dużych systemów lepiej wybrać pasmo 5GHz. Są wyższe pasma stworzone "na zaś" i raczej nie są używane.

ISM - 2.4GHz
UNII - 5GHz

**Na paśmie 2.4GHz można nadawać pod warunkami:**
- musi być wykorzystywana technika rozproszenia widma (skakanie po częstotliwościach, kluczowanie bezpośrednie, modulacja "chirp"), robi się tak, ponieważ nie zajmuje się wtedy całego pasma na raz
- można stosować Indoor i Outdoor
- każdy system skaczący po częstotliwościach w tym paśmie musi mieć minimum 15 kanałów, każdy po 1MHz

Każdy system ma maskę promieniowania - kształt widma sygnału. "Widmo nie może być szersze niż ten 1MHz, ewentualnie na poziomie -20dB lub -40dB". Jeśli karta radiowa nie spełnia wymagania to nie może wyjść na rynek.

Są jeszcze ogólne ograniczenia:
- czas przebywania na pojedynczym kanale $t_{dwell}<=400[ms]$
- ETSI: każdy kanał powtórzony co najmniej raz na $4*t_{dwell}*N_{kanałów}$
- FCC: średnia $t_{dwell} < \frac{0.4s}{30s}$ 
- wszystkie kanały z dostępnej puli muszą być jednakowo prawdopodobne
- Skuteczna Izotropowa Moc Promieniowania (EIRP) nie może przekraczać
  > - $20dBm$ w Polsce (ETSI)
  > - w Ameryce (FCC) bardziej skomplikowane
  
Jeśli chodzi o pasmo 5GHz, jest lepiej ale wykorzystywane jest też szersze pasmo, "nie ma miejsca na dole". 

Bluetooth jest "skaczącym po kanałach" w sposób pseudolosowy protokołem. Jest 79 kanałów (po 1MHz), sekwencje urządzeń są różne żeby nie dochodziło do kolizji. Skok jest 1600x na sekundę. 

Oprócz skakania mamy rozpraszanie/kluczowanie bezpośrednie - bierzemy sobie strumień danych o jakimś czasie trwania, bierzemy sekwencję rozpraszającą i mnożymy (XOR). Sekwencję bitów zapisujemy w o wiele gęstszej sekwencji, zo rozprasza sygnał. Efekt jest taki, że energia wypełnia większy zakres częstotliwości ale jest "niższa", zatem możliwa jest koegzystencja systemów. Podczas skupienia (korekcji) szumy są rozpraszane. Jest to dobre jeśli mamy synchronizację, dobrze skorygowane zegary itd. - w chujowych systemach ten typ rozpraszania nie działa poprawnie. 

Kolejna technika to OFDM (Orthogonal Frequency Division Multiplexing) - rozkładanie transmisji na wiele mniejszych transmisji. Używany wszędzie. Odporny na zakłócenia międzysymbolowe, selektywne. Lepszy od FDM (każdy system w innym kanale), w OFDM każda transmisja nakłada na siebie w połowie - nie jest to duży problem.

"Chirp" - zera i jedynki stają się impulsami o długości {0;T} z narastającą dla 1 lub opadającą dla 0. Narosty mogą być liniowe lub wykładnicze. Technika jest odporna na wielodrogowość, bardzo odporna na wiele zakłóceń. Wada to mała przepustowość. Nadaje się do systemów telemetrycznych i do lokalizacji. 

Ostatni system to UWB (Ultra-Wideband), prehistoryczny. Ma więcej niż 0.5Ghz (wg. Amerykanów). Poza szerokością musi spełnić warunek stosunku bandwidth do częstotliwości. Żeby wygenerować system szerokopasmowy, trzeba mieć bardzo krótki/szybki impuls.  