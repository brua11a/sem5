Dzisiaj trudne!! Powtórz w domu.

##### Podstawowe wskaźniki
**Na poziomie algorytmu klasyfikacji (samego komponentu systemu biometrycznego):**
- FMR (False Match Rate)
- FNMR (False Non-Match Rate)

**Na poziomie działania całego systemu (cały system biometryczny)**
- FAR (False Acceptance Rate)
- FRR (False Rejection Rate)

Często mogą być tożsame, ale niekoniecznie.

Są jeszcze zdarzenia pozytywne: True Positive i True Negative - w związku z tym True Acceptance Rate.

**Błędy na poziomie rejestracji i przetwarzania danych:**
- FTA (Fail to Aquire) - próbki nie udało się pobrać, np. dlatego, że czytnik jest brudny
- FTE (Fail to Enroll) - jakość danych jest na tyle słaba, że nie są one przetwarzane

Często przy takich błędach system zwraca informacje typu "spróbuj jeszcze raz". Ilość prób powinna być ograniczona, a także powinien być zdefiniowany failover.
Te błędy można wliczać do FRR albo nie - należy to określić definicyjnie.

Czynniki opisane wcześniej dotyczą jedynie sytuacji, w których mamy po prostu genuine użytkowników albo fałszywych użytkowników próbujących wejść swoimi danymi - low effort "ataki".

**EER** (Equal Error Rate) - punk przecięcia się FAR i FRR, teoretycznie optymalny ale w praktyce niewiele mówi bo system powinien być albo użyteczny albo bezpieczny. Teoretycznie im niższy wskaźnik ERR tym lepszy system.

FMR = $\int^{\infty}_{\delta=T}p_n(s)ds$  -> suma prawdopodobienśtw "innych osób w naszej przestrzeni" od thresholdu T do końca wykresu
FNMR  = $\int_{\delta=-\infty}^{T}p_m(s)ds$ -> suma prawdopodobienśtw "nas w cudzej przestrzeni" od minus nieskończoności do thresholdu T.

![[Pasted image 20251105134003.png]]

Jeśli możliwe chcemy, żeby próbki z tych wykresów się nie pokrywał
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
Zdjęcie $t_{35}1$ jest atakowane przez wszystkie inne $34*100$ zdjęć, potem $t_{35}2$ znowu jest atakowane przez $34000$... i tak ze wszystkimi, tworzy się rozkład gęstości po lewej.
Ta sama osoba też jest sprawdzana ze samą sobą - $t_{35}1$ z $t_{35}2$, $t_{35}1$ z $t_{35}3$... aż porówna się wszystkie. Z tego powstaje rozkład po prawej.
Proces jest powtarzany dla KAŻDEGO z 35 użytkowników.

$p(s)$ na wykresie to szansa na to, że dana próbka trafi w to "miejsce", czyli jaka jest szansa na to, że losowa osoba z bazy zostanie oceniona na $s$ procent.

#### Kolejne wskaźniki systemów biometrycznych
1. ROC (Receiver Operating Characteristic)
2. DET (Detection Error Tradeoff)

Są to lepsze metryki od ERR, ponieważ zazwyczaj patrzymy na całe spektrum FRR i FAR. Te funkcje opisują zależność FRR względem FMR i vice versa, dlatego są sobie odwrotne.

Te krzywe są wygodne ponieważ mogę sobie wyhalucynować jakiś score FRR lub FAR i rzutując na wykres dostaję ten drugi.

Do porównywania klasyfikatorów używa się AUC (Area Under Curve). Jeśli dwa klasyfikatory się przecinają, wybór jest indywidualny w zależności od tego, jakiego FRR lub FAR oczekujemy - wtedy znowu należy wykonać rzut. Nie interesuje nas średni punkt pracy - interesuje nas KONKRETNY punk pracy, zatem należy znać szczegóły - jak system zachowuje się przy danych parametrach.

#### Powrót do matematyki
Miara $d'$ (d-prim) mówi na ile dwa rozkłady są "wspólne" a na ile "rozdzielne" - jak daleko od siebie są środki "górek" rozkładów w porównaniu z tym, jakie są "szerokie". Im większe tym lepsze.
$d'$ mierzy jak daleko od siebie leżą średnie rozkładów genuine i impostor względem ich rozrzutów.

$d' = \frac{\mu_m - \mu_n}{\sqrt{\delta_m^2 + \delta_n^2}}$

Gdzie $\mu$ to średnia a $\delta$ to odchylenie.

Dla tych samych $d'$ mogą nadal być inne krzywe, czyli dwa systemy mogą być inaczej użyteczne. Ocena pracy komparatorów znowu jest czymś indywidualnym.