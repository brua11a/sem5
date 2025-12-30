#### Zaniki dużej skali:
**Tłumienie medianowe** (swobodna przestrzeń, inne modele propagacyjne). Opisuje średnie zachowanie sygnału na dużych odległościach (kilkudziesięciu kilometrach).

**Zaniki przesłaniania** (przesłony takie jak budynki, wzgórza, korytarze). Dodają losowości wokół tłumienia medianowego. Skutkiem jest to, że dwa urządzenia o tej samej odległości mogą mieć różne poziomy sygnału.

![[Pasted image 20251225153323.png]]
#### Zaniki małej skali:
Nie do końca nad nimi panujemy i nie do końca je modelujemy, spowodowane np. [[Ścieżki propagacji|wielodrogowością]]. Mówimy o skali długości fali, milisekund, herców.
- Zaniki płaskie - całe pasmo tłumione jednakowo.
- Zaniki selektywne częstotliwościowo - różne częstotliwości, różne tłumienia
- Zaniki szybkie
- Zaniki wolne

#### Modele
**LOS (*Line of Sight*)** oraz **NLOS (*Non-Life of Sight*)** to również modele propagacyjne. W zależności od nich powstają:
- **Kanał AWGN** - najbardziej optymistyczny, brak wielodrogowości, sam LOS, zaniki małej skali, jedyny szum to biały szum Gaussa.
- **Kanał Rayleigha** - najbardziej pesymistyczny, sam NLOS, bardzo skomplikowany, składa się z wielu losowych ścieżek, duża bitowa stopa błędu.
  >![[Pasted image 20251225152034.png]]
- **Kanał Rice'a** - zarówno jeden dominujący LOS jak i kilka słabszych NLOS, niewielkie wahania wokół wartości średniej $\mu$, pomiędzy AWGN a Rayleigh'em. Definiowany przez $K=\frac{P_{LOS}}{P_{NLOS}}$ Przy małych wartościach $K\rightarrow0$ dąży do Rayleigha, przy dużych $K\rightarrow \infty$ dąży do AWGN.
  >![[Pasted image 20251225152047.png]]

![[Pasted image 20251225152012.png]]

![[Pasted image 20251225152637.png]]

Do obliczeń często wykorzystuje się też model symulacyjny, w którym nie liczymy ani tego ani tamtego tylko dokładamy biały szum - każdy system można przeanalizować pod względem rosnącego szumu.

**Bitowa stopa błędu $BER$** to prawdopodobieństwo wystąpienia błędu w kanale AWGN. Jest przemnażane przez prawdopodobieństwo błędu w kanale Rice'a. 

![[Pasted image 20251225152716.png]]