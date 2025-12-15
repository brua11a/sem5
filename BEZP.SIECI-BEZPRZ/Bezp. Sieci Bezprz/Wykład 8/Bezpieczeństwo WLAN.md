Nieautoryzowany dostęp - przechwycenie danych, przeszukiwanie pamięci itp.
Naruszenie integralności
Naruszenie lub nieprawidłowe użycie usług sieciowych
Nieautoryzowany dostęp do usług

Większość problemów wynika z tego, że jest współdzielone łącze, ogólnodostępne. Nie możemy postawić szafy i dać kabli jak w klasycznej sieci Ethernetowej.

*Mobilność i dostępność Wi-Fi jest jego największą wadą :/*

#### Pierwsze zabezpieczenia
Wyłączenie rozgłaszania SSID (nic nie daje), filtrowanie dostępu (autoryzacja wybranych MAC, wątpliwa obrona), izolacja klientów sieci bezprzewodowej wg. specjalnej konfiguracji na punkcie dostępowym (klienci nie mogą się ze sobą porozumiewać).

Pierwsze godne uwagi rozwiązania to szyfrowanie WEP, WPA, WPA2, a także metody enterprise takie jak w pełni izolowane sieci WiFi z otwartym dostępem (np. RADIUS) czy standard 802.11x.

#### Architektury
**Sieć domowa:**
1. Internet ma działać szybko
2. Internet ma po prostu działać
3. Za resztę odpowiada ISP
4. Urządzenia sieciowe w sieci domwowej.
Stosuje się PSK, szyfrowanie WPA2/WPA3. Złamanie wspólnego klucza powoduje kompromitację całej sieci. W WPA3 każdy ma inny handshake, zatem przechwycenie naszego handshake atakującemu de facto nic nie da.

**Sieć enterprise:**
1. Internet ma działać szybko
2. Internet ma po prostu działać
3. Za resztę odpowiada **administrator**
4. Urządzenia sieciowe w sieci firmowej.
Punkt dostępowy jest pośrednikiem pomiędzy klientem a serwerem, a nie AP odpowiada za wszystko. Indywidualne klucze, więcej komponentów, implementacja AAA. Przechwycenie jednych poświadczen nie kompromituje całej sieci.

Metody uwierzytelniania WPA2-Enterprise ma dwa sposoby - mnie i bardziej bezpieczny.

Mniej bezpieczny - zewnętrzny tunel TLS do przesyłania danych uwierzytelniających, bardzo popularny, polega na challenge-response. Łatwe łamanie brute force i ataki słownikowe. Słaby ale lepszy od Personal rozwiązań. Przechwycenie handshake łamie autentykację.

Bardziej bezpieczny - EAP-TLS - wykorzystuje certyfikaty cyfrowe, wymieniane pomiędzy urządzeniami. Bardzo bezpieczny ale skomplikowany w zarządzaniu.

W WPA3 pojawiły się dodatkowe Enterprise zabezpieczenia - SAE (każda sesja uwierzytelniania jest unikalna), OWE (automatycznie szyfrowany ruch w otwartych sieciach). Zarówno źródło jak i cel się uwierzytelniają dzięki SAE. 

#### Atak
Potrzebna karta sieciowa z trybem "monitor". Nie każdy ruch w szyfrowanej sieci jest szyfrowany. Należy wybrać odpowiednią kartę z odpowiednim chipsetem.

Typowe narzędzie - Kismet, pokazuje informacje na temat sieci, takie jak adresy MAC i kanały. Wsparcie dla GPS, szczegółowe informacje itd.
Było na labach - `aircrack`, wykorzystywany często *under the hood*

**WEP** - wspólny klucz dla wszystkich, szyfr symetryczny strumieniowy RC4. Ciąg jest tworzony na podstawie klucza WEP i wektora inicjującego. Największa wada - IV ma 24 bity. Statystycznie, po 5000 pakietach mamy 50% szansy na złamanie. Za szybko wektor się powtarza. Dostęp  jest zabezpieczany poprzez samo SSID albo klucz. 

**WPA** - pojawił się praktycznie od razu ze względu na problemy WEP. Było to przejście pomiędzy WEP a WPA2 - dopiero WPA2 był rzeczywiście w miarę bezpieczny. W WPA można się autentykować poprzez PSK (WPA-PSK) lub poprzez poświadczenia login+hasło (WPA-Enterprise). W WPA każdy pakiet jest szyfrowany innym kluczem, gdzie każda para urządzeń klient + AP używa innego klucza. Samo złamanie klucza nie powoduje pełnej kompromitacji, tylko tego jednego użytkownika. Klucze "końcowe" tworzone poprzez 4-WAY handshake, te wyżej są wspólne (chociaż to zależy czy PSK czy Enterprise).

Na czas sesji PTK i GTK się nie zmieniają. Do szyfrowania pojedynczych wiadomości stosuje się TKIP, poza kluczem i adresem nadawcy dodaje się sekwencję, na postawie tego powstaje klucz osobny dla kazdej wiadomosci. Potem to "trafia do WEP". W WPA2 wprowadzono jeszcze CCMP - mechanizm wykorzystujący AES, wymagał już osobnego hardware. 

Przy atakach na WPA "poluje się" na wartości wykorzystywane w 4-WAY handshake. Atak polega na PMK i PTK zgadując PSK, czyli 8-63 znaków ASCII.

W WPA3 wprowadzono 4 dodatkowe kroki wzmacniające generowanie kluczy i szyfrowanie - SAE commit i confirm w dwie strony. Generowanie dwóch liczb losowych i wymiana. PMK zmienia się co chwilę, jest wyliczany, nie wymyślono jeszcze efektywnego ataku. Jedyne znane ataki na WPA3 to downgrade i side-channel.

Co jest nie tak z WPS? Loguje się pinem 8 znaków gdzie ostatni znak to kontrola a 7 pozostałych nie jest sprawdzanych na raz. Zamiast tego najpierw sprawdza sie 4 potem 3. 10^7 >>>> 10^3+ 10^4.