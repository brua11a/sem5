#### Zabezpieczenia typu zwierającego (*crowbar*)
Działanie elementu zabezpieczajączego polega na ograniczeniu energii przepięcia w wyniku gwałtownej zmiany swego stanu przewodzenia (ze stanu wielkiej impedancji do małej impedancji, takich jak szczeliny powietrzne). 

##### Odgromniki
Przykładem takiego zabezpieczenia są **odgromniki (*surge arresters*)**. Są one wypełnione gazem oraz zakończone elektrodami metalowymi, dzięki czemu gdy do odgromnika dotrze impuls przepięcia, dochodzi do jonizacji tego gazu. Powoduje to *wyładowanie jarzeniowe*, potem *łukowe*, co powoduje zwarcie w układzie przez obniżenie rezystancji do około $0.1\;\Omega$.

Napięcie na odgromniku w stanie wyładowania łukowego to 10-15V i pozostaje stałe. Po zaniku przepięcia odgromnik powraca do stanu nieaktywnego, w którym stanowi rezystancję w $\text{G}\Omega$. 

Odgromniki cechuje stabilność parametrów elektrycznych, wielka rezystancja w stanie nieaktywnym, mała pojemność własna, zdolność przewodzenia bardzo dużych prądów, małe wymiary. Dodatkowo, chronią one napięcia od kilkudziesięciu $\text{V}$ do kilku $\text{kV}$.

Niestety, są one wolne - opóźnienie zapłonu < $1\;\mu s$.

![[Pasted image 20260103234456.png]]

#### Zabezpieczenia typu ograniczającego (*clamp*)
Działanie elementu polega na redukcji doprowadzonego do niego przepięcia do wartości dopuszczalnej dla danego typu elementu, np. warystory, diody Zenera.

##### Warystor
Są to *spieki z tlenków metali* w kształcie krążków lub pastylek. Warystor przy odpowiednim napięciu, nazywanym "napięciem zadziałania warystora", zaczyna gwałtownie zmniejszać rezystancję. Mieści się ono w zakresie od $10\;\text{V}$ do $1000\;\text{V}$.

Napięcie zadziałania warystora jest wprost proporcjonalne do grubości pastylki, a maksymalna energia, którą może zaabsorbować warystor jest zależna od objętości elementu.

![[Pasted image 20260104000256.png]]

Dodatkowe właściwości to:
- krótki czas odpowiedzi ($\text{ns}$)
- średni prąd upływu ($<\;1\;\mu A$ przy $0.1$ napięcia zadziałania)
- duża pojemność pasożytnicza (od $1\;\text{nF}$ do $10\;\text{nF}$) i absorbowana energia (od $5\;\text{J}$ do $500\;\text{J}$)

#### Wielostopniowa ochrona przeciwprzepięciowa
W praktyce obydwa te mechanizmy są wykorzystywane ze względu na ich różne wady i zalety.

![[Pasted image 20260104001308.png]]

W tym układzie odgromnik odprowadza główną energię impulsu do uziemienia wraz ze zmniejszeniem napięcia. Następnie warystor ponownie zmniejsza amplitudę zaburzenia. Finalna podwójna dioda przepuszcza jedynie ruch o bezpiecznym poziomie. Każdy element pracuje w swoim optymalnym zakresie