**EIRP (*Effective Isotropic Radiated Power*) i ERP (*Effective Radiated Power*)** - "co promieniujemy z danego urządzenia". Wybór zależy od anteny odniesienia - izotropowej lub dipolowej. EIRP porównuje moc do tej z idealnej anteny izotropowej. ERP odnosi się do półfalowej anteny dipolowej.

Każde pasmo ma pewne unormowania - dotyczy ono tych parametrów, żeby np. ktoś nie zajął sobie całego pasma.

Pomiędzy tłumiennością antenową $\frac{EIRP}{4\pi d^2}$ a [[Wektor Poyntinga|gęstością mocy EM]] $S=\frac{E^2}{\eta}$ można wyprowadzić relację w wolnej przestrzeni: $E=\frac{\sqrt{30*EIRP}}{d}$
$d$: odległość od nadajnika
$EIRP$: całkowita skuteczna moc wypromieniowana

#### Odbiór sygnału radiowego
Powierzchnia skuteczna dla fali płaskiej - dobrze znać. $A_{sk}$
Długość skuteczna lub współczynnik antenowy - dobrze znać. $L_{sk}$ lub $AF=2/L_{sk}$
![[Pasted image 20251224214018.png]]

Parametry pola EM są przemieniane na moc w odbiorniku
$P_L=S*A_{sk}$. Obie miary nie zależą od cech anteny tylko od parametrów elektrycznych (obciążenia i zysku energetycznego, a także parametrów samej fali i ośrodka propagacyjnego).
#### ERP, EIRP, Gi, Gd
Przyjmujemy dwa rodzaje anten odniesienia:
1. **Antenę izotropową**
   >"Idealnie promieniuje w każdym kierunku" - odniesienie zysku w $G_i$ (gain isotrophic?), jest to model jedynie hipotetyczny, "kuleczka".
   >![[Pasted image 20251224221149.png]]
2. **Dipol półfalowy**
   >"Pączek, obwarzanek" - odniesienie zysku w $G_d$ (gain dipol?), nie promieniuje w kierunkach pionowych, ale w domu sygnał i tak raczej dotrze bo odbije się od ścian. Często wykorzystywana w praktyce. Promieniuje zgodnie z mocową charakterystyką kątową. 
   >![[Pasted image 20251224221358.png]]
   >Koncentracja energii EM w kierunku $F=0\textdegree$, ale brak promieniowania w osi anteny. Dipol półfalowy "promieniuje na boki" mocniej, niż izotropowy o 1,64 razy lub o 2,15dB więcej.

![[Pasted image 20251224222310.png]]

