#### Kolejne wskaźniki systemów biometrycznych
1. **ROC** (Receiver Operating Characteristic)
   >Krzywa ROC **łączy FAR (1-FAR) i FRR w jedną krzywą**, pokazując jak te dwa błędy zmieniają się wraz ze zmianą progu decyzyjnego. Pole pod krzywą to miara jakości klasyfikacji, gdzie 1.0 to idealny klasyfikator a 0.5 to klasyfikator losowy. Im większe pole tym lepiej. **Ideał to lewy górny róg.**
   >
   >![[Pasted image 20260128131928.png]]
1. **DET** (Detection Error Tradeoff)
   >Wartości estymatorów błędów FAR i FRR wyrażone w skali odwrotnej. **Ideał to lewy dolny róg - minimum FAR i FRR.**  
   >
   >![[Pasted image 20260128132025.png]]

![[Pasted image 20260128132048.png]]

Są to lepsze metryki od ERR, ponieważ zazwyczaj patrzymy na całe spektrum FRR i FAR. Te funkcje opisują zależność FRR względem FMR i vice versa, dlatego są sobie odwrotne.

Te krzywe są wygodne ponieważ mogę sobie wyhalucynować jakiś score FRR lub FAR i rzutując na wykres dostaję ten drugi - "oczekuję konkretnego FAR, jaka będzie tego konsekwencja dla FRR?".

Do porównywania klasyfikatorów używa się **AUC (Area Under Curve)**. Jeśli dwa klasyfikatory się przecinają, wybór jest indywidualny w zależności od tego, jakiego FRR lub FAR oczekujemy - wtedy znowu należy wykonać rzut. Nie interesuje nas średni punkt pracy - interesuje nas KONKRETNY punkt pracy, zatem należy znać szczegóły - jak system zachowuje się przy danych parametrach.

#### Powrót do matematyki
Miara $d'$ (d-prim) mówi na ile dwa rozkłady są "wspólne" a na ile "rozdzielne" - jak daleko od siebie są środki "górek" rozkładów w porównaniu z tym, jakie są "szerokie". Im większe tym lepsze.
$d'$ mierzy jak daleko od siebie leżą średnie rozkładów genuine i impostor względem ich rozrzutów.

$d' = \frac{\mu_m - \mu_n}{\sqrt{\delta_m^2 + \delta_n^2}}$

Gdzie $\mu$ to średnia a $\delta$ to odchylenie.

Dla tych samych $d'$ mogą nadal być inne krzywe, czyli dwa systemy mogą być inaczej użyteczne. Ocena pracy komparatorów znowu jest czymś indywidualnym.