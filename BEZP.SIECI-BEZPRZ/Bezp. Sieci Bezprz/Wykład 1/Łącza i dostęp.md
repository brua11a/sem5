###### **Łącze "w górę" (UL) (*Uplink*)**
Od urządzeń końcowych do stacji bazowych.
![[Pasted image 20251223234915.png]]
###### **Łącze "w dół" (DL) (*Downlink*)**
Od stacji bazowej do urządzeń końcowych, często większa przepustowość.
![[Pasted image 20251223234926.png]]
### Zwielokrotnianie kanału
Dzieli dostępne zasoby pojemnościowych stacji bazowej pomiędzy obsługiwane terminale, np. pasmo routera bezprzewodowego na różne kanały. Wymagany, gdy jedna osoba próbuje przekazywać kilka różnych osobnych sygnałów na raz. *Lotnisko ma swoje częstotliwości, policja ma swoje, nikt sobie nie przeszkadza*.

###### **FDD (*Frequency Division Duplex*)**
Duplex częstotliwościowy - pasmo jest dzielone na dwa fragmenty o równej szerokości, gdzie jedno jest w dół (szybsze) a drugie w górę (wolniejsze). 

Użytkownikowi przyznaje się kanał $f_k$, który jest parą kanałów odległych od siebie o **odstęp duplexowy** $Df$. Dzięki temu transmisja może iść w dwie strony. Dobre dla ruchu symetrycznego, gdzie obydwa pasma są wykorzystywane

![[Pasted image 20251223235142.png]]
###### **TDD (*Time Division Duplex*)**
Duplex czasowy - całe dostępne pasmo jest w danej szczelinie czasowej jest dedykowane do ruchu UL lub DL. Dobre dla ruchu asymetrycznego, gdzie nie zawsze pasmo jest równomiernie wykorzystywane. 

![[Pasted image 20251223235205.png]]

### Zwielokrotnianie dostępu
Gdy jest więcej terminali niż dostępnych kanałów do stacji bazowych, konieczne jest zwielokrotnienie dostępu. Terminale rywalizują o wspólne zasoby transmisyjne (czas, częstotliwość, kod). Jest ono wymagane, gdy wiele użytkowników chce jednocześnie korzystać z tego samego medium transmisyjnego.

###### **FDM/FDMA (*Frequency Division Mupltiplexing / Frequency Division Multiple Access***
Kanał częstotliwościowy jest dzielony na mniejsze, niepokrywające się pasma. Każdy użytkownik otrzymuje własne pasmo częstotliwości na cały czas trwania połączenia.

###### **TDM/TDMA (*Time Division Mupltiplexing / Time Division Multiple Access***
Kanał jest współdzielony w czasie. Użytkownicy nadają naprzemiennie w krótkich szczelinach czasowych (slotach), które cyklicznie się powtarzają. Każdy terminal korzysta z pełnego pasma częstotliwości, ale tylko przez przydzielony mu czas.
###### **CDMA (*Code Division Multiple Access*)**
Wszyscy użytkownicy korzystają jednocześnie z całego pasma i całego czasu, lecz są rozróżniani za pomocą unikalnych kodów rozpraszających. Sygnał każdego użytkownika jest rozpraszany w szerokim paśmie, a po stronie odbiornika tylko poprawny kod pozwala odzyskać właściwy sygnał, podczas gdy pozostałe traktowane są jako szum. 

![[Pasted image 20251224000125.png]]

Rozwiązanie to nie działa do końca ponieważ kody zostawały wykorzystane, przez co pasmo się zapełniało i rozproszony sygnał mieszał się przez co: *zamiast 0 pojawiały się 1 i tworzył się szum przez co Kowalski na 3G zamiast 2MiB miał 1MiB a potem jeszcze mniej jak sąsiedzi też sobie montowali CDMA*.

