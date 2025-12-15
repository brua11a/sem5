Zaczął się w 1999 roku. Pierwsza wersja posysała bo nie działały razem ze sobą produkty innych producentów. Dopiero wersja 1.2 była taka, jaką znamy. Większa przepustowość, szybsza transmisja.

Do transmisji głosu potrzebne jest pasmo 64kb (8 kB) na sekundę - wtedy jest zrozumialne. Dzisiejszy, "akceptowany" Bluetooth to wersja 2.1+. Poprawiono potem jeszcze o kanał WLAN do wysyłania danych (takich jak np. zdjęć) - raczej niezalecane, ale możliwe (24 Mb/s). Zabijało to baterię szybko, dlatego stworzono rozwiązania niskoenergetyczne/

Nowoczesne Bluetooth 4.0 (BLE, ULP, Wibree, Smart Ready, Smart) zużywa o wiele mniej mocy. Docelowo na działać w sieciach sensorycznych. 

Bluetooth pracuje w pasmie 2.4 GHz - tak samo, jak WLAN. Pojedynczy kanał ma 1MHz. Transmisja jest szybka, trudna do uchwycenia, ulotna. Kanałów jest prawie 80. Wykorzystuje "skakanie po częstotliwościach" - duplex czasowy (nadaje skacze nadaje skacze). 

Sekwencja przeskoków jest szybka - 1600 skoków na sekundę. Pomysł jest taki, żeby nie zaśmiecać całego pasma, dlatego skacze w pseudolosowy sposób. Master wysyła do slave w parzystych szczelinach a slave do mastera w nieparzystych (lub na odwrot nie zdazylem przepisac)

Po każdym skoku jest czas stabilizacji - pewnien nagłówek. Ze względu na dużą ilość skoków dzieje się to bardzo często. Skoki dają odporność na transmisję i wytrzymałość sygnału.

#### Stos protokołów
1. Controller
   >Fizyczne urządzenie zainstalowane na hoście, często w jakiś sposób zintegrowane. 
2. Host
   >Implementacja protokołu na urządzeniu.
3. Protokoły transportowe (na poziomie kontrolera i na poziomie kontrolera+hosta)
4. Protokoły pośredniczące (OBEX, SDP)
5. Grupa aplikacji (wykorzystują profile definiujące wykorzystanie standardu)

#### Uwierzytelnianie
Odpowiedzialny za to jest kontroler połączenia, który szuka wspólnego klucza. Podczas pierwszego połączenia jest wyświetlany (czasem) PIN do weryfikacji. Po uwierzytelnieniu połączenie jest zastawiane na podstawie nowego klucza połączenia.

#### Typy fizycznych łączy
1. SCO
   >- master decyduje o wszystkim - zestawianie i rozłączanie połączenia
   >- dla transmisji głosu
   >- master rezerwuje szczeliny czasowe dla niezawodności
   >- full duplex, p2p
2. ACL

W warstwie fizycznej mają tą samą przepustowość ale FEC może wprowdzać ograniczenia. 

#### Topologie
1. P2P (najczęstsza) - master i slave
2. Pikosieć - master i duzo slave'ów, zagreowana przepustowość
3. Rozproszona - grupa pikosieci połączonych wspólnym węzłem

Wszędzie jest raczej topologia gwiazdy, ale jeśli jest potrzeba komunikacji slave-slave to tworzy się nowa pikosieć gdzie inicjator staje się "lokalnym" masterem.

#### Tryby
Decyduje o tym Master
1. SNIFF - "co kilkanascoe milisekund macie sie budzic czy was nie wywoluje", najmniej energooszczedny
2. HOLD - w tym trybie urządzenie może być w jednej pikosieci w trybie HOLD a w drugiej aktywne, wstrzymywanie na okres czasu
3. PARK - beacon budzi raz na kilka minut, traci adres i dostaje adres "zaparkowania", działa dla urządzen nie wysylajacych dane na zywo tylko jakies cos raz na jakis czas. Najbardziej energooszczedne.