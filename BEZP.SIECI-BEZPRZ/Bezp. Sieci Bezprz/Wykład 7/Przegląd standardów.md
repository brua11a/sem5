Pierwsze standardy są stare - nie omawiamy.

Pierwszy sensowny standard to standard b (IEEE 802.11b) z 1999 roku. Stosował DSSS i kształt widma jest inny - ze względu na rozproszenie widma, maskę, dodatkowe kodowanie. Szerszy kanał, zaokrąglony na bokach.

Dzisiaj jeśli zobaczymy standard a to raczej ag (IEEE 802.11a -> IEEE 802.11ag). Jako pierwszy pojawił się w paśmie 5GHz. Nie było to wtedy dobrze rozwinięty zatem wrócono do 2.4GHz.

Standard g (IEEE 802.11g) jest starszy, ale raczej powszechnie dopuszczany. Działa tak, jak a, ale w paśmie 2.4GHz - dosłownie jedyną zmianą jest pasmo.

Prawdziwe WLAN takie jakie znamy dzisiaj zaczęły się od Wi-Fi 4, standard n (IEEE 802.11n). Kontrolował OFDM, większa przepustowość, szerokość kanału, technika MIMO. Oferował przepustowości do 600 Mb/s w zależności od odstępu ochronnego (nagłówka, można ustawić, większe dal sygnałów wielodrogowych, nawet 800ns, inaczej 400ns). Im wyższa modulacja tym mniejsza czułość i sygnał musi być silniejszy. MIMO powoduje problemy z działaniem ze starymi standardami - jeden "delikwent" spowalnia całą sieć

802.11ac wspiera Multi User MIMO - część anten może być przeznaczona dla starych użytkowników, a reszta dla nowych używających MIMO. Nowe modulacje, nowe szerokości kanału, osiem strumieni przestrzennych.

Opracowywaniem WLAN zajmuje się:
- IEEE (standard, akurat ten dotyczy warstwy fizycznej i łącza danych, dodatkowo CSMA/CA)
- WLANA (informacje techniczne)
- Wi-Fi Alliance (przydziela znaczki)

W paśmie 2.4GHz jest 14 kanałów. Są oddalone od siebie 5MHz, a same w sobie mają ~2400MHz. 

IEEE 802.11x standaryzuje topologie sieci WLAN:
- Niezależna Podstawowa Grupa Sieciowa IBSS (tryb ad hoc, dwóch klientów bez punktu dostępowego jest połączonych ze sobą bezpośrednio). Do identyfikacji urządzeń w sieci służy SSID
- Rozszerzona Grupa Sieciowa ESS (tryb infrastrukturalny, z AP). Może być z CSMA/CA albo managed ("zarządzany"). Punkt dostępowy (AP) NIE jest routerem - AP to brama pomiędzy interface bezprzewodowym a przewodowym, interface bezprzewodowy będzie w tej samej sieci co klienci. Istnieje jeszcze ESS z bezprzewodowym DS - "tryb infrastrukturalny". System dystrybucji stanowi łącze radiowe pomiędzy dwoma punktami dostępowymi AP.

#### Struktura ramki (PMD_PDU)
1. Preambuła PLCP - szacowany czas zajęcia kanału, synchronizacja, detekcja sygnału, częstotliwość transmisji
2. Nagłówek PLCP - informacje o przepustowości

CSMA/CA jest rozwinięciem CSMA/CD - nie są wykrywane kolizje tylko jest ono zapobiegane, nie są wysyłane dane jeśli kanał jest zajęty. Wykonywany jest nasłuch obcych transmisji i wstrzymanie własnej w razie wykrycia obcej.
Dostępem zarządza DCF (wymagana) i PCF (opcjonalna) - pewna rywalizacja.
*Opisane na slajdach, trudno opisac bez obrazkow*

QoS - znany z sieci
#### 802.1e - EDCF
Niższy numerek -> ważniejsza kategoria, wyższa klasa. Numer 0 ma VoIP i routing, numer 1 ma video. QoS wiąże się z procesem rywalizacji, zamiast krótkiego odstępu międzyramkowego są przedziały AIFS związane z klasą ruchu - "ważniejszy" ruch losuje numer z mniejszego przedziału. Każdy z tych czasów jednak jest dłuższy niż DIFS, zatem klienci nieobsługujący QoS też mogą brać udział w sieci. Wprowadzenie EDCF powoduje powstanie czterech kolejek. 

#### Kanały
Na paśmie 2.4GHz zazwyczaj używa się 3 pasm - <1, 6, 11> lub <2, 7, 12> itp., stały odstęp. Dla 802.11b separacja musi wynosić co najmniej 25MHz, co tworzy zakłócenia poniżej -35dB. Najgorsza sytuacja to taka, gdy kanały nachodzą na siebie CZĘŚCIOWO, już lepiej gdy nachodzą całkowicie.

