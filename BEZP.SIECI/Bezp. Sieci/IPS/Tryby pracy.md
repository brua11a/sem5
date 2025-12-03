**Zarówno [[Wykrywanie ataków|IDS]] jak i [[IPS]] (NIPS konkretnie) mogą pracować w trybach:**

#### promiscuous (passive) mode
Analizowana jest kopia ruchu przechodzącego przez sensor. Dzięki temu analiza nie wpływa na rzeczywisty ruch sieciowy. Niestety, to rozwiązanie nie jest w stanie "zablokować" pakietu gdy uznany zostanie za szkodliwy - on już poleciał dalej. Jest to szczególnie prawdziwe dla krótkich ataków, wykorzystujących mało danych.

![[Pasted image 20251126122222.png]]
#### inline (inline interface pair) mode
IPS znajduje się bezpośrednio pomiędzy połączeniem między dwoma docelowymi hostami, dzięki czemu może "przechwycić" ruch i przekazać go dalej na podstawie zasad. Analiza może zostać wykonana na warstwach od 3 do 7, co daje jeszcze większe możliwości niż jakikolwiek firewall.

![[Pasted image 20251126122246.png]]