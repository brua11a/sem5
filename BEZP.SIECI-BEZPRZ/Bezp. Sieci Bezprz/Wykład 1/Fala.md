#### Fala idealna
W przypadku idealnym fala elektromagnetyczna to propagująca się fala sinusoidalna. Zmienne pole elektryczne tworzy zmienne pole magnetyczne, a to pole magnetyczne wytwarza zmienne pole elektryczne i tak w kółko na zmianę. Tak się dzieje aż fala "wygaśnie" - zostanie np. stłumiona. 

![[Pasted image 20251223230338.png]]

Pole elektryczne i pole magnetyczne są prostopadłe wobec siebie. Mają wzajemną orientację wobec siebie oraz względem kierunku propagacji fali $\vec{k}$ - iloczyn wektorowy.

![[Pasted image 20251224141734.png]]

$$
\begin{align*}
& z: \text{odległość wzdłuż kierunku propagacji fali (oś } z\text{)} \\
& t: \text{czas} \\
& a_x: \text{wektor jednostkowy w kierunku osi } x \text{ (kierunek polaryzacji pola } E\text{)} \\
& a_y: \text{wektor jednostkowy w kierunku osi } y \text{ (kierunek pola } H\text{)} \\[6pt]
& E(z,t): \text{natężenie pola elektrycznego w punkcie } z \text{ i czasie } t \\
& H(z,t): \text{natężenie pola magnetycznego w punkcie } z \text{ i czasie } t \\[6pt]
& E_0: \text{maksymalna amplituda (wartość szczytowa) pola elektrycznego} \\
& \eta: \text{impedancja ośrodka} \\[6pt]
& \omega: \text{częstość kołowa fali } (\omega = 2\pi f) \\
& \beta: \text{stała fazowa, szybkość zmian fazy fali EM w ośrodku} \\[6pt]
& \cos(\omega t - \beta z): \text{człon oscylacyjny opisujący falę biegnącą wzdłuż osi } z
\end{align*}
$$

#### Fala realna - w ośrodku stratnym
W rzeczywistości fala znajduje się w [[Parametry fali EM|ośrodku stratnym]] ($\sigma>0$), przez co maleje **amplituda** - fala doświadcza tłumienia. Przez to przy odbiorniku maleje co najmniej amplituda, a w gorszym przypadku też faza itd.

![[Pasted image 20251223230518.png]]

**Różnica:** We wzorze pojawia się $e^{-\alpha z}$. Wynika z równań Maxwella, konkretnie prawa Ampere'a. **$\alpha$ to stała tłumienia**, oznacza zanik amplitudy wraz z odległością.

Stała tłumienia (W OŚRODKU STRATNYM) jest większa dla wyższych częstotliwości i konduktywności - amplituda zanika szybciej. 

![[Pasted image 20251224142758.png]]

**Stała fazowa $\beta$**  oznacza jak szybko będzie zmieniała się długość fali - jak szybko zmienia się $\lambda$, im większa przenikalność magnetyczna $\mu$ tym dłuższa fala, dzięki temu można zmniejszyć rozmiar anten.

![[Pasted image 20251224143644.png]]
![[Pasted image 20251224144419.png]]

We wzorze na pole magnetyczne pojawia się przesunięcie fazowe $\theta_\eta$ między $E$ a $H$. 
### Propagacja w swobodnej/wolnej przestrzeni (ideał):
$$FLS[dB] = 32.44 + 20log(f_{MHz})+20log(d_{km})$$
Na 1m tłumienie to około $40dB$ - tłumienie ma "ostry start" ale później strata jest mniejsza. Tłumienie amplitudy fali EM wynika z wykładniczej natury stałej tłumienia $\alpha$. 

![[Pasted image 20251224143037.png]]

"Swobodna przestrzeń" w tym kontekście to: *nie wystarczy Line of Sight, potrzebna jest propagacja w elipsoidzie, co najmniej 90% elipsoidy musi być wolne*.

