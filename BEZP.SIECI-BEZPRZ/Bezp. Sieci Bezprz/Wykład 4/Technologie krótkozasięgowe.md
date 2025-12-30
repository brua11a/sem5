#### Pasmo 2.4 GHz
![[Pasted image 20251225154910.png]]

**Na paśmie 2.4GHz można nadawać pod warunkami:**
1. Musi być wykorzystywana technika rozproszenia widma ([[skakanie po częstotliwościach]] FH, [[kluczowanie bezpośrednie]] DS, modulacja "chirp"). Robi się tak, ponieważ nie zajmuje się wtedy całego pasma na raz.
2. Można stosować Indoor i Outdoor.
3. Każdy system skaczący po częstotliwościach w tym paśmie musi mieć minimum 15 kanałów, każdy po 1MHz

**Są jeszcze ogólne ograniczenia dla 2.4 GHz:**
- czas przebywania na pojedynczym kanale $t_{dwell}<=400[ms]$
- ETSI: każdy kanał powtórzony co najmniej raz na $4*t_{dwell}*N_{kanałów}$
- FCC: średnia $t_{dwell} < \frac{0.4s}{30s}$ 
- wszystkie kanały z dostępnej puli muszą być jednakowo prawdopodobne, skoki wg. sekwencji pseudolosowej
- Skuteczna Izotropowa Moc Promieniowania ([[Odbieranie fali|EIRP]]) nie może przekraczać 20dBm w Polsce (ETSI), w Ameryce (FCC) bardziej skomplikowane
  > ![[Pasted image 20251225200532.png]]
#### Pasmo 5 GHz
Jeśli chodzi o pasmo 5GHz, jest lepiej ale wykorzystywane jest też szersze pasmo, "nie ma miejsca na dole". Maksymalna wartość EIRP na niskim paśmie to 23 dBm, na wysokim paśmie 30 dBm.

![[Pasted image 20251225201953.png]]
#### [[Bluetooth]]
Bluetooth jest "skaczącym po kanałach" w sposób pseudolosowy protokołem. Jest 79 kanałów (po 1MHz), sekwencje urządzeń są różne żeby nie dochodziło do kolizji. Skok jest 1600x na sekundę. 