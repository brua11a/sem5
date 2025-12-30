#### Pojedyncza ścieżka
Odpowiedź impulsowa -> pokazuje jak zmienia się sygnał po przejściu przez kanał, po policzeniu transformaty Fouriera dostaniemy transmitancję i dowiemy się na jakich częstotliwościach coś się dzieje z sygnałem.
![[Pasted image 20251225135706.png]]

#### Wielodrogowość
Przy propagacji wielodrogowej mamy falę idącą "bezpośrednio" i "pośrednio" (odbita), ta druga podróżuje dłużej i prawdopodobnie zostaje zniekształcona. Im większa wielodrogowość tym większa nieprzewidywalność. Transmitancja robi się bardziej "pofalowana", nieprzewidywalna. 

Sygnał bezpośredni i wielodrogowy będą ze sobą sumowane, co można opisać wzorem:
$$
E_{\text{tot}}=\sum^N_{i=0}E_i*e^{j\theta_i}
$$
![[Pasted image 20251225135819.png]]
![[Pasted image 20251225135840.png]]
![[Pasted image 20251225140155.png]]

#### Wpływ propagacji wielodrogowej
W sytuacji idealnej (sygnał trafia do kanału z jedną ścieżką) to sytuacja jest prosta. Widmo wysłanego i odebranego sygnału będzie takie samo.
![[Pasted image 20251225140957.png]]

Dla większej ilości ścieżek już transmitancja na pewno $H(f)\neq1(f)$, zatem widmo odebranego sygnału $Y(f)$ będzie mocniej deformowane w stosunku od wysyłanego $U(f)$.
![[Pasted image 20251225141107.png]]

Z wielodrogowością jest związane pojęcie rozproszenia czasowego - $\tau$. Każde środowisko propagacyjne ma inną specyfikę - inaczej będzie wracał sygnał z gór, inaczej z miasta, inaczej ze wsi.
![[Pasted image 20251225141918.png]]
![[Pasted image 20251225142033.png]]

![[Pasted image 20251225141428.png]]
Na rysunku są różne szerokości pasma. Odpowiedź kanału radiowego $H(f)$ w funkcji częstotliwości nazywamy transmitancją kanału. Ruch powyżej dopuszczalnego poziomu zaników 3dB znajduje się w paśmie koherencji $B_x(\Delta f)$.

Jeśli widmo naszego sygnału *mieści się w listku transmitancji bez zaniku to jest spoko*, zatem zależy nam na tym, żeby stracić jak najmniej sygnału
![[Pasted image 20251225141648.png]]

Sygnał "wystający" poza transmitancję zostaje "przycięty". Najgorsza sytuacja to taka, w której widmo sygnału jest "szersze" od transmitancji, przez co sygnał zostanie przycięty nierównomiernie.
![[Pasted image 20251225141750.png]]

Wiele technologii polega na tym, że wysyła bardzo wąsko, bardzo krótko i bardzo szybko - dzięki temu unika się tego problemu.

