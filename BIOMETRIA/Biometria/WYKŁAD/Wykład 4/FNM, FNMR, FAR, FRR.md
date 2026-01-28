![[Pasted image 20260128114240.png]]
#### Podstawowe wskaźniki
**Na poziomie algorytmu klasyfikacji (samego komponentu systemu biometrycznego):**
- **FMR** (False Match Rate)
- **FNMR** (False Non-Match Rate)

**Na poziomie działania całego systemu (cały system biometryczny)**
- **FAR** (False Acceptance Rate)
- **FRR** (False Rejection Rate)

Często mogą być tożsame, ale niekoniecznie.

Są jeszcze zdarzenia pozytywne: True Positive i True Negative - w związku z tym True Acceptance Rate.

![[Pasted image 20260128123559.png]]

**Błędy na poziomie rejestracji i przetwarzania danych:**
- **FTA** (Fail to Acquire) - próbki nie udało się pobrać, np. dlatego, że czytnik jest brudny
- **FTE** (Fail to Enroll) - jakość danych jest na tyle słaba, że nie są one przetwarzane

Często przy takich błędach system zwraca informacje typu "spróbuj jeszcze raz". Ilość prób powinna być ograniczona, a także powinien być zdefiniowany failover.
Te błędy można wliczać do FRR albo nie - należy to określić definicyjnie.

Czynniki opisane wcześniej dotyczą jedynie sytuacji, w których mamy po prostu genuine użytkowników albo fałszywych użytkowników próbujących wejść swoimi danymi - low effort "ataki".

---

**EER** (Equal Error Rate) - punk przecięcia się FAR i FRR, teoretycznie optymalny ale w praktyce niewiele mówi bo system powinien być albo użyteczny albo bezpieczny. Teoretycznie im niższy wskaźnik ERR tym lepszy system.

**FMR** = $\int^{\infty}_{\delta=T}p_n(s)ds:$  suma prawdopodobienśtw "innych osób w naszej przestrzeni" od thresholdu T do końca wykresu
**FNMR**  = $\int_{\delta=-\infty}^{T}p_m(s)ds:$  suma prawdopodobienśtw "nas w cudzej przestrzeni" od początku wykresu do thresholdu T.

![[Pasted image 20260128120134.png]]

Jeśli możliwe chcemy, żeby próbki z tych wykresów się nie pokrywały - wtedy najczęściej powstają właśnie błędy.
# Powtórz kombinatoryke </3

Przykład: 1 osoba, 100 zdjęć, $C^2_{100}$, sprawdzasz jaka jest szansa, że "ja to ja" - tworzy się jakaś gęstość.
Potem 35 innych osób po 100 zdjęć próbuje "zaatakować" nasze zdjęcia - tworzy się drugi rozkład.
W praktyce oznacza to: Jaka jest szansa na to, że czyjeś dane będą go identyfikować, a jaka jest szansa, że cudze dane też mogą go identyfikować.
$$
T_1 = \{t_11,\,...,\,t_1100\}\;
T_2 = \{t_21,\,...,\,t_2100\}\;
T_3 = \{t_31,\,...,\,t_3100\}...\;
T_{35} = \{t_{35}1,\,...,\,t_{35}100\}\;
$$
Zdjęcie $t_{35}1$ jest atakowane przez wszystkie inne $34*100$ zdjęć, potem $t_{35}2$ znowu jest atakowane przez $34000$... i tak ze wszystkimi, tworzy się rozkład gęstości po lewej. "Jak bardzo osoby są podobne do innych osób"

Ta sama osoba też jest sprawdzana ze samą sobą - $t_{35}1$ z $t_{35}2$, $t_{35}1$ z $t_{35}3$... aż porówna się wszystkie. Z tego powstaje rozkład po prawej. "Jak bardzo osoba jest podobna do samej siebie"

Proces jest powtarzany dla KAŻDEGO z 35 użytkowników.

$p(s)$ na wykresie to szansa na to, że dana próbka trafi w to "miejsce", czyli jaka jest szansa na to, że losowa osoba z bazy $M$ zostanie oceniona na $s$ procent.

#### Oczekiwany błąd całkowity oraz koszt
Oczekiwany błąd całkowity uwzględnia prawdopodobieństwo wystąpienia danego zdarzenia. Wtedy stopa błędu całkowitego:

$E(T)=\text{FMR}(T)*P_i+\text{FNMR}(T)*P_g$

$P_i:$ prawdopodobieństwo, że próbka $B$ pochodzi od *impostor*
$P_g:$ prawdopodobieństwo, że próbka $B$ pochodzi od *genuine*

Udoskonalenie całkowitego błędu oczekiwanego polega na przypisaniu kosztu do błędu i wyliczeniu kosztu oczekiwanego.

$\text{KOSZT}=C_{FMR}*\text{FMR}(T)*P_i+C_{FNMR}*\text{FNMR}(T)*P_g$