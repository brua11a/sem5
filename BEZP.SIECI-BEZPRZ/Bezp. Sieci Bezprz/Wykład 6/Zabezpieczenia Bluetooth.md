### Głównie wprowadzone w Bluetooth 5.0
1. **LE 2M + LE Coded PHY** - nowa warstwa fizyczna, szybkość transmisji 2Msym/s czyli w praktyce 2Mbit/s
   >Wszystkie implementacje BLE obslugują co najmniej LE 1M, od 5.0 LE 2M. Do detekcji błędów w LE 2M używa się 24-bit CRC. Warstwa fizyczna LE ma duży zasięg, nawet do 350m.
   >Detekcja błędów domyślnie jest ale korekcja nie. Pojawia się dopiero w LE Coded PHY (S=2 lub S=8), gdzie używa się FEC do korekcji. Do pakietów dodawana jest informacja nadmiarowa. Metody z FEC są wolniejsze, ale bardziej niezawodne. 
2. **Extended Advertising** - w wersji 4.x wprowadzono rozgłaszanie ("reklamy") na kanałach 37-39, ale w Bluetooth 5.0 do advertisement mozna uzyc wszystkich 40 kanalow
   >W BLE pakiety mają 47B i są rozgłaszane na kanałach 37, 38 i 39 - bez parowania. W BT 5.0 dodano 8 nowych PDU związanych z rozgłaszaniem - pozwala przesyłać więcej danych i unikać "tłoku w kanałach", używać harmonograów i w kanałach głównych są przesyłane tylko nagłówki. W BLE 5.0 pakiety mają 255B, gdzie user data jest w kanałach 0-36 a w 37-39 są dane nagłówkowe - w nagłówkach jest "wskaźnik" do user data. Pakiety można łączyć wskaźnikami w łańcuchy.
   >Transmisja danych rozgłoszeniowych wykorzystuje llosowe opóźnienie 0-10ms, dzieki czemu unika sie kolizji. Wprowadzono też synchronizację czasową, dzięki czemu urządzenia mogą "spać" pomiędzy momentami w ktorych nic sie nie dzieje - oszczedza energie
3. **Slot Availability Mask**
   > Mozliwe jest zakłócanie się modułu z radiem LTE pracującym w sąsiednim paśmie. "Za silny sygnał z boku może sprawiać, że urządzenie nie będzie w stanie pracować, potęguje się przy systemach małej i dużej mocy". Radia w telefonach komórkowych 5G mogą nadawać do 1V - BLE pracujący na 1mV zostanie zamordowany. Żeby temu zapobiec, nadano maskę slotów SAM - definiuje kiedy kto może nadawać na podstawie kodów 0 1 2 3 gdzie każdy od ma jakieś znaczenie (można o tym myśleć jak o masce bitowej uprawnień "wysyłaj-niewysylaj" `00` `01` `10` `11`).
4. **Improved frequency hopping**
   >Zamiast skakania losowego, wewnątrz połączenia Bluetooth można definiować jaka usługa "gdzie skacze" - w jakimś zakresie kanałów, najlepiej niepowtarzającym się.
   
### Bluetooth 5.1
Rozszerzone o lokalizację. Wprowadzone jest pozycjonowanie z użyciem siły sygnału do określania odległości. Urządzenia Bluetooth mogą teraz określać kierunek transmisji. Są dwie metody lokalizowania obiektów:
- AoA - kąt nadejścia
- AoD - kąt odbioru
Obydwa działają sensownie. W Bluetooth 5.1 wprowadzono dodatkowe PDW - stos `1` nazywany CTE (Constant Tone Extension), dzięki czemu częstotliwość i długość fali są stałe. Próbki są przesyłane w górę stosu za pośrednictwem HCI, gdzie do obliczenia kierunku używa się wybranego algorytmu. Nie jest to stricte ustandaryzowane, w standardzie jest samo przekazywanie w górę. 

Ulepszono też buforowanie GATT. Bluetooth w każdej wersji ma protokół GATT - służy do pozyskiwania atrybutów do usług - jakie ma uslugi co one potrafia ajkie sa wlasciwosci jakie sa obostrzenia co do autporyzacji itd. Jak klient sie łączy z naszym serwerem to zaczyna uzywac ATT od odpytywania. To jest ok jak cos sie zmienia. Te tabele atrybutow sa jednak stale - serwer tradycyjnie musi pamietac ktory klient co pamieta itd. Jest to problem, zużywa to energię. Np. jeśli twoj telefon laczy sie ze sluchawkami i wie o nich wszystko to i tak odpyta sluchawki o wszystkie jej cechy, bez sensu.

W 5.1 wprowadzono sposob pominiecia tego - klient moze pominac wykrywanie uslug jesli nic sie nie zmienilo, a to ze nic sie nie zmienilo jest sprawdzane hashem. Ten sam hash -> klient wie wszystko i nie musi sie o nic pytac. 

Kolejna cecha: randomizacja rozglaszania, randomizacja kanału. Pomimo Improved Frequency Hopping dodano losowe opóźnienie od 10ms pomiędzy rozgłoszeniami. W BT 5.1 mozna wybierać kanały losowo co zmniejsza prawdopodobienstwo kolizji - wieksza szansa ze bedzie skakac po sekwencji roznych kanalow a nie tej samej sekwencji.

Dodatkowo: ulepszenie rozgłaszania. Nie wszystkie urządzenia są na tyke wydajne by się zsynchronizować. Wprowadzono w zwiazku z tym PAST (Periodic Advertising Sync Transfer) - synchronizacji dokonuje silniejsze urządzenie.

Drobne ulepszenia:
- HCI Support for Debug Keys in LE Secure Connections - zakodowanie kluczy do debugowania
- Sleep Clock Accuracy Update Mechanism
- Interaction Between QoS and Flow Specification
- Specify the behavior when rules are violated

### Bluetooth 5.2
NAJWIEKSZY DODATEK - **EATT**

Pozwala na równolegle wiele odpytywań - wielu serwerów na raz. Zamiast blokującego kolejkowania jest możliwość jednoczesnej transakcji. 

LE Power Control umożliwia zarządzanie energią poprzez dynamiczne ????
Wprowadzono trzy nowe PDU, dzięki czemu Master może zarządać od Slave zmianę trybu pracy - zaoszczędzić moc. Klient też odpowiada ramką, w którem jest np. jest min-max moc, ile zmienil itd.

Ostatnia cecha: Low Energy Audio. Kanały izochroniczne - zsynchronizowane, pozwala na lepsze wykorzystanie Bluetooth do przesyłania dźwięku. Grupa znajomych może słuchać tego samego. Można ustawić "ważność" grupy broadcastowej - jeśli klient "nie słyszy" to to nie będzie powtórzone, co ma znaczenie w szczegolnosci broadcastow. 

### Bluetooth 5.3 
Kowal omija bo nie zrobił slajdów XD

