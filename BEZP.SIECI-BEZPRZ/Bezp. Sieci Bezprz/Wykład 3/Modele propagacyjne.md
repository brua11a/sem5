**Zaniki dużej skali:**
- tłumienie medianowe (swobodna przestrzeń, inne modele propagacyjne)
- zaniki przesłaniania (przesłony takie jak budynki, wzgórza, korytarze)
**Zaniki małej skali:** nie do końca nad nimi panujemy i nie do końca je modelujemy
- zaniki płaskie
- zaniki selektywne częstotliwościowo
- zaniki szybkie
- zaniki wolne

**LOS/NLOS** - tez modele, LOS to Line of Sight, zazwyczaj do niego dążymy.
Są dodatkowo przypadki takie jak:
- Kanał AWGN - najbardziej optymistyczny
- Kanał Rayleigha (wyłącznie NLOS) - bardzo skomplikowany, najbardziej pesymistyczny
- Kanał Rice'a (LOS + NLOS) -  w miarę prosty, przy małych wartościach dąży do Rayleigha, przy dużych do AWGN

Do obliczeń często wykorzystuje się też model symulacyjny, w którym nie liczymy ani tego ani tamtego tylko dokładamy biały szum - każdy system można przeanalizować pod względem rosnącego szumu.

Bitowa stopa błędu to prawdopodobieństwo wystąpienia błędu w kanale AWGN. Jest przemnażane przez prawdopodobieństwo błędu w kanale Rice'a. 

