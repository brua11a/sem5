#### Elementy łącza radiowego
![[Pasted image 20251224232040.png]]

Budżet energetyczny łącza radiowego jest sumą mocy, zysków i strat na drodze pomiędzy [[Odbieranie fali|nadajnikiem a odbiornikiem]], dzięki temu można określić poziom mocy odebranej przez odbiornik $P_0$. **Na pewno będzie na labach!**

Zasięg systemów telekomunikacyjnych zależy TYLKO od współczynnika sygnału do szumu.

![[Pasted image 20251224232424.png]]

Moc jest nadawana, maleje o tłumienie fidera nadajnika, rośnie o zysk energetyczny nadajnika, maleje o tłumienność trasy międzyantenowej, znowu rośnie o zysk energetyczny ale odbiornika i maleje o tłumienność fidera odbiornika. Summa summarum moc na odbiorniku wynosi $P_o=E(I)RP-L_{prop}+G_o-A_o$, gdzie $G$ może być wyrażone w dBd lub dBi (w zależności od anteny odniesienia).

#### Odebrana moc
Moc na odbiorniku $P_o$ należy odnieść do wartości szumu $N$, zależnego od temperatury, szerokości kanału, niedokładności odbiornika i czynników zewnętrznych. Wyróżnia się:
1. SNR (Signal-Nose-Ratio) przy braku zakłóceń od innych źródeł promieniowania, sam szum.
   >![[Pasted image 20251224233004.png]]
2. SNIR (Signal-Noise and Interference Radio) przy istnieniu zewnętrznych zakłóceń i szumów.
   >![[Pasted image 20251224233013.png]]

Zazwyczaj wartości SNR są podawane w postaci tabeli wartości wyrażonych w dB, gdzie są one dodawane do podstawowego szumu i traktowane jako threshold. SNR są zależne od chociażby modulacji. Wszystko poniżej tej granicy nie będzie możliwe do odebrania w zamierzony sposób.

![[Pasted image 20251224233353.png]]