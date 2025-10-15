###### **Łącze "w górę" (UL) (*Uplink*)**
Od urządzeń końcowych do stacji bazowych.

###### **Łącze "w dół" (DL) (*Downlink*)**
Od stacji bazowej do urządzeń końcowych, często większa przepustowość.

###### **Zwielokrotnianie kanału**
Dzieli dostępne zasoby pojemnościowych stacji bazowej pomiędzy obsługiwane terminale, np. pasmo routera bezprzewodowego na różne kanały. *Lotnisko ma swoje częstotliwości, policja ma swoje, nikt sobie nie przeszkadza*.
Techniki: FDM, TDM, CDM.

###### **FDD (*Frequency Division Duplex*)**
Duplex częstotliwościowy - pasmo jest dzielone na dwa fragmenty o równej częstotliwości, gdzie jedno jest w dół (szybsze) a drugie w górę (wolniejsze). 
Użytkownikowi przyznaje się kanał $f_k$, który jest parą kanałów odległych od siebie o **odstęp duplexowy** $Df$. Dzięki temu transmisja może iść w dwie strony. Dobre dla ruchu symetrycznego, gdzie obydwa pasma są wykorzystywane

###### **TDD (*Time Division Duplex*)**
Duplex czasowy - całe dostępne pasmo jest w danej szczelinie czasowej jest dedykowane do ruchu UL lub DL. Dobre dla ruchu asymetrycznego, gdzie nie zawsze pasmo jest równomiernie wykorzystywane. 

###### **CDMA (*Code Division Multiple Access*)**
Każdemu użytkownikowi dostaniemy cały kanał na cały czas z tym, że użytkownicy są rozróżniani poprzez rozproszenie sygnału i tylko poprawny kod po drugiej stronie pozwala odzyskać sygnał (???). Rozwiązanie to nie działa do końca ponieważ kody zostawały wykorzystane, przez co pasmo się zapełniało i rozproszony sygnał mieszał się przez co: *zamiast 0 pojawiały się 1 i tworzył się szum przez co Kowalski na 3G zamiast 2MiB miał 1MiB a potem jeszcze mniej jak sąsiedzi też sobie montowali CDMA*.

