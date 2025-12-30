![[Pasted image 20251228200456.png]]

Antena to element przekształcające napięcie lub prąd zmienny o częstotliwości radiowej na wejściu na falę EM i kierujący ją na określonym kierunku przestrzeni i vice versa. Każdy odcinek przewodnika z płynącym prądem zmiennym może być niezamierzoną anteną.

#### Parametry anten
**Obwodowe:**
- **impedancja wejściowa, rezystancja promieniowania** – impedancja widziana na zaciskach anteny; rezystancja promieniowania opisuje część mocy zamienianą na falę elektromagnetyczną
- **dopasowanie do linii transmisyjnej** – stopień zgodności impedancji anteny i linii (np. współczynnik fali stojącej, SWR), wpływa na straty odbić
- **zakres częstotliwości pracy** – pasmo, w którym antena zachowuje akceptowalne parametry (dopasowanie, zysk, charakterystyka)

**Polowe:**
- **charakterystyka promieniowania** – przestrzenny rozkład mocy promieniowanej w funkcji kierunku
- **szerokość wiązki głównej** – kąt między punktami spadku mocy (zwykle −3 dB) w głównym listku promieniowania
- **polaryzacja** – orientacja wektora pola elektrycznego fali (liniowa, kołowa, eliptyczna)
- **współczynnik antenowy** – miara relacji między polem elektrycznym a napięciem na wyjściu anteny (istotny w pomiarach)
- **kierunkowość** – zdolność anteny do skupiania promieniowania w określonym kierunku. Określa sumarycznie własności kierunkowe anteny - stosunek maksymalnej gęstości promieniowania do średniej gęstości promieniowania. Jest jednoznacznie określona przez jej charakterystykę promieniowania. Nie uwzględnia strat mocy w antenie.
  >![[Pasted image 20251228203007.png]]
- **sprawność energetyczna** – stosunek mocy wypromieniowanej do mocy doprowadzonej do anteny
- **zysk energetyczny** – iloczyn kierunkowości i sprawności; porównanie do anteny izotropowej. Gęstość promieniowania wydzielana w kierunku dzielona przez maksymalną gęstość promieniowana wytwarzana przez wzorcową antenę przy tej samej mocy.
  >![[Pasted image 20251228203232.png]]
- **długość lub powierzchnia skuteczna** – miara „efektywnego rozmiaru” anteny w odbiorze, związana z jej zdolnością przechwytywania energii fali

#### Charakterystyka anten
Charakterystykę promieniowania anteny rozpisuję się w układzie biegunowym i kartezjańskim. Są podawane dwa prostopadłe przekroje - E i H. Określa ona własności anteny poprzez wyznaczenie rozkładu natężenia pola E na powierzchni kuli o dużym promieniu. **Definiuje się szerokość wiązki głównej (kąt połowy mocy, zawarty między kierunkami promieniowania dla których gęstość spada o 3dB w płaszczyznach wektora E i H) i kąt zerowy (kąt, dla którego promieniowanie spada do zera).**

![[Pasted image 20251228202655.png]]

Charakterystyki promieniowania anten zależą od wielkości anten w stosunku do długosci fali:
$\lambda[m]=\frac{300}{f[MHz]}$.

#### Współczynnik antenowy
Anteną pomiarową właściwie mierzymy napięcie. Współczynnik antenowy AF to relacja napięcia mierzonego na wyjściu anteny w stosunku do natężenia pola E/M oddziałowującego na tą antenę.

![[Pasted image 20251228204406.png]]
