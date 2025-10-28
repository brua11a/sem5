Wykład o **propagacji**

Trzy podstawowe parametry decydujące o własnościach elektrycznych i magnetycznych ośrodka propagacyjnego:
- $\mu$ przenikalność magnetyczna $[H/m]$
  >$\mu = \mu_0 * \mu_{wz}$ 
- $\epsilon$ przenikalność elektryczna $[F/m]$
  > $\epsilon = \epsilon_0 * \epsilon_{wz}$
- $\sigma$ konduktywność $[S/m]$

Najlepsze warunki to "fala elektromagnetyczna porusza się z prędkością światła"

**Ze względu na te parametry rozróżniamy:**
- dielektryki bezstratne - energia pozostaje, ideał
- dielektryki stratne - energia jest zamieniana w ciepło
- przewodniki - 
- paramagnetyki - przenikalność mag. względna jest większa od 1 (gdy przyłoży się zewnętrzną falę magnetyczną to zacznie się przyciąganie)
- diamagnetyki - na odwrót, czy przyłoży się falę to zacznie odpychać
- ferromagnetyki - silne właściwości magnetyczne

Prędkość poruszania fali w danym ośrodku to: $v=\frac{1}{\sqrt{\mu*\epsilon}}$
Wzór można przekształcić do: $v=\frac{c}{\sqrt{\mu_{wz}*\epsilon_{wz}}}$

Dla każdego ośrodka innego niż próżnia szybkość rozchodzenia się fali EM jest mniejsza niż prędkość światła
Wniosek: długość fali $\lambda$ i jej częstotliwość $f$ w każdym ośrodku łączy relacja: $v = \lambda*f$
Czyli $\lambda*f=\frac{c}{\sqrt{\epsilon_{wz}}}$
Czyli $\lambda = \frac{1}{\sqrt{\epsilon_{wz}}}*\lambda_0$

Fala elektromagnetyczna składa się z wektora pola elektrycznego E i pola magnetycznego H, znając jeden można wyliczyć drugi. Są pojebane wzory.
W tych wzorach są **stała tłumienia $\alpha$** (jak fala jest tłumiona w danym ośrodku propagacyjnym, jeśli materiał "bardziej przewodzi" to więcej energii przeradza się w ciepło i amplituda fali maleje) i **stała fazowa $\beta$** (jak szybko będzie zmieniała się długość fali - jak szybko zmienia się $\lambda$, im większa przenikalność magnetyczna $\mu$ tym dłuższa fala, dzięki temu można zmniejszyć rozmiar anten).

Odpowiedź impulsowa -> pokazuje jak zmienia się sygnał po przejściu przez kanał, po policzeniu transformaty Fouriera dostaniemy transmitancję i dowiemy się na jakich częstotliwościach coś się dzieje z sygnałem.

Przy propagacji wielodrogowej mamy falę idącą "bezpośrednio" i "pośrednio" (odbita), ta druga podróżuje dłużej i prawdopodobnie zostaje zniekształcona. Im większa wielodrogowość tym większa nieprzewidywalność. Transmitancja robi się bardziej "pofalowana", nieprzewidywalna. 

W sytuacji idealnej (sygnał trafia do kanału z jedną ścieżką) to sytuacja jest prosta. Dla większej ilości ścieżek już transmitancja na pewno będzie $H(f)\neq1(f)$, zatem widmo odebranego sygnału $Y(f)$ będzie mocniej deformowane w stosunku do wysyłanego $U(f)$.

Z wielodrogowością jest związane pojęcie rozproszenia czasowego - $\tau$. Każde środowisko propagacyjne ma inną specyfikę. Jeśli widmo naszego sygnału "mieści się w listku transmitancji bez zaniku to jest spoko", zatem zależy nam na tym, żeby stracić jak najmniej sygnału - sygnał "wystający" poza transmitancję zostaje "przycięty". Najgorsza sytuacja to taka, w której widmo sygnału jest "szersze" od transmitancji, przez co sygnał zostanie przycięty nierównomiernie. Wiele technologii polega na tym, że wysyła bardzo wąsko, bardzo krótko i bardzo szybko - dzięki temu unika się tego problemu.

