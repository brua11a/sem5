Dzisiaj trudne!! Powtórz w domu.

System identyfikacji pracuje zawsze na bazie danych $M$ wzorców biometrycznych. Każdy z tych wzorców jest przypisywany do elementu zbioru tożsamości $T$, gdzie jedna tożsamość może mieć kilka wzorców. System ma za zadanie stwierdzić, czy podana biometryka $B$ należy do bazy $M$ i wskazać potencjalnych kandydatów, bądź dać informację $B \not\in M$. 

#### Zgodność z biometryką $B$ można przedstawić jako:
1. **Listę kandydatów wraz z punktacją**
   >Ustawia się próg decyzyjny $T$ - wszystko "poniżej" iluśtam % dopasowania jest odrzucane.
2. **Listę rang $C$**
   >Permutacja zbioru tożsamości z $M$, kandydaci dopasowani od najbardziej do najmniej podobnych do wzorca. Ogranicza się do top $N$ rang i odrzuca te poniżej.
3.  **Rozwiązanie hybrydowe**
   >Najlepiej zrobić tak, że "szybkim algorytmem" przy pomocy rang z bazy $M$ wyznacza się top $N$ próbek $B$ najbardziej podobnych do wzorca, a następnie dopiero dla tych $N$ kandydatów **(czyli nie całej bazy $M$)** jest liczona punktacja jakimś dokładniejszym algorytmem. Jednocześnie warto zachować próg $T$ aby odrzucić sytuacje, w których wszystkie top $N$ kandydatów jest niewystarczająco podobnych do wzorca. Ranga 1 nie oznacza do
   >
   >![[Pasted image 20260128121731.png]]

#### Świat/system otwarty i zamknięty
Świat otwarty zakłada, że prawdziwej osoby może nie być w bazie $M$, czyli system musi mieć możliwość odrzucenia wszystkich.

Świat zamknięty zakłada, że wszyscy potencjalni użytkownicy systemu już zostali zarejestrowani, zatem podczas klasyfikacji któryś kandydat musi odpowiadać wzorcowi.

#### RPM (Rank Probability Mass)
RPM to funkcja rozkładu prawdopodobieństwa rangi $r$, która informuje o tym jak system identyfikacji nadaje rangi. Wynik funkcji $\text{RPM}(r)$ to szansa na to, że prawidłowa próbka $B$ po porównaniu ze wzorcem pojawi się na $r$ miejscu, czyli $\text{RPM}(2)=0.4$ oznacza, że dla tego systemu prawdziwa próbka w 40% przypadków zostanie uznana za "drugą najbardziej podobną do wzorca".

$\text{RPM}(r)=P(r),r=1,...,m$ 

Dla każdej zarejestrowanej (czyli istniejącej w bazie $M$ i odpowiadającej tożsamości $T$) biometryki $B$ jest $P(r)$ szansy na to, że wystąpi ona na $r$ pozycji. $\sum^m_{r=1}P(r)=1$

![[Pasted image 20260128122847.png]]

Jeśli próbki $B$ po porównaniu ze wzorcem (de facto *samym sobą*) consistently dają wysokie rangi (5, 7, 10) to system jest słaby. Jeśli te same próbki dają niskie rangi (1, 2, 3) to system jest dobry. Intuicyjnie, jeśli system porównując mnie ze wszystkimi innymi uzna, że ja jestem top 1, top 2, top 3 **najbardziej podobną osobą do samego siebie** to raczej działa poprawnie. 
#### CMC (Cumulative Match Curve)
Jest to suma częściowych RPM - czyli $\text{CMC}(2)$ to $\text{RPM}(1)+\text{RPM}(2)$. Tworzy to rosnące "schodki", które mówią: "jaka jest szansa na to, że próbka $B$ odpowiadająca wzorcowi trafi do top $N$?"

![[Pasted image 20260128131011.png]]

RMP można oszacować empirycznie jako $P(k)$ dla bazy danych zawierającej biometryki testowe. Wtedy, $P(k)=\frac{|L_k|}{|L|}$, gdzie $L$ to zbiór wszystkich testów identyfikacyjnych, a $L_k$ to podzbiór testów, w których prawdziwa tożsamość miała dokładnie rangę $k$. WAŻNE: $L<M$.

![[Pasted image 20260128131503.png]]
# Rangi itp. są lepiej opisane w [[Biometria_ćwiczenie_RPM_CMC_Final-1.pdf]]