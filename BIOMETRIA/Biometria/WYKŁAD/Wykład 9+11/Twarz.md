Ostatnia modalność, którą będziemy omawiać

Jest szczególnie istotna, ponieważ używanie twarzy do identyfikacji jest intuicyjne dla ludzi. Potrafimy rozpoznawać twarze o wiele lepiej od innych biometryk. Mamy jednak bias związany z "prototypem" osób, które znamy, a biometryka ma być reprezentatywna. Ludzki mózg wykrywa też twarze tam, gdzie ich nie ma - biometryka ponownie nie chcemy żeby tego robiła.

#### Wpływ czynników
1. **Czynniki psychofizyczne** - emocje, starzenie, choroby.
2. **Modyfikacje** - makijaż, okulary, zarost.
3. **Typowość** - prototyp twarzy i odstępstwa.
   >Każdy człowiek ma inny prototyp twarzy, jest on subiektywny i zależy od doświadczenia (aka ludzi, z którymi przebywamy).
4. **Czynniki fotometryczne** - oświetlenie, pozycja, odległość.

**Człowiek zapamiętuje cechy charakterystyczne, a nie całe twarze.**

#### Automatyczne rozpoznanie twarzy
Biometria nieinwazyjna - pobieranie próbki może dziać się "przy okazji". Czujniki nie są drogie, kamery są wszędzie. Jesteśmy przyzwyczajeni do monitoringu itp. a więc nikt nie protestuje przeciwko tej biometryce. Jest to też dosyć efektywne obliczeniowo i lekkie. 

#### Ataki
Morphing pozwala stworzyć dokument tożsamości, który będzie podobny do nas, ale też do kogoś jeszcze. Automatyczny system jest podatny na takie rozwiązania. Zazwyczaj nie ufa się zdjęciu, tylko człowiekowi, który przyszedł - żywy człowiek przed tobą to *grand truth*.

#### Wyzwania
Pierwszym z nich są niedogodności i przeszkody - poza twarzy, oświetlenie, wyraz, przesłonięcia, okulary, włosy na twarzy. Należy też pamiętać o czynnikach biologicznych, takich jak starzeniu, wypadkach i chorobach.

Próbki inaczej będą wyglądały w środowisku kontrolowanym, inaczej w niekontrolowanym. Z tego też powodu, zarówno szablon jak i próbka muszą zostać znormalizowane - podobna poza, "prostowanie" obrazu. Normalizacja pozy pozwala na podstawie zdjęcia twarzą do przodu zrobić zdjęcie z boku.

![[Pasted image 20260128162201.png]]

#### Poszukiwanie zbioru twarzy
**Koncepcja analityczna** bazuje na cechach strukturalnych twarzy. Człowiek na tym polega bardzo mocno. Bez problemu rozpoznajemy cechy twarzy niezależnie od oświetlenia, wyrazu twarzy, pozycji itp. Wykorzystywane są tutaj **metody bazujące na geometrii twarzy** - kontury, położenie oczu, nosa, ust, kształt oczu, nosa, ust... Nie jest sprawdzany rzeczywisty dystans tylko proporcja odległości pomiędzy konkretnymi punktami - dzięki temu zachowuje się odporność na skalowanie obrazu.

![[Pasted image 20260128163955.png]]

Twarz ma określoną ilość landmarków, a także indeksy antopometryczne - to nie odległości same w sobie, to raczej będzie np. "odległość między oczami w proporcji do odległości między oczami a ustami", co pozwala skalować obraz a i tak identyfikować osobę. Takich indeksów może być DUŻO. "Stałym" landmarkiem są uszy, a także lewy kącik ucha - nie ruszają się. Zamknięte oczy to bardzo mała odległość między powiekami.

**Koncepcja holistyczna** rozpoznaje twarz na bazie całościowego obrazu twarzy bez wyodrębniania cech strukturalnych. Może polegać na analizie przykładów twarzy i nie-twarzy. Takie rozwiązanie jest wykorzystywane przy *falkach HAAR*. Potem, do detekcji może zostać użyta **metoda Viola-Jones.**

#### Viola-Jones
https://www.youtube.com/watch?v=uEJ71VlUmMQ
Polega ona na koncepcji holistycznej - twarz lub nie-twarz. Cały obraz jest analizowany w poszukiwaniu twarzy o różnych położeniach i rozmiarach. Zdjęcie "skanuje" się oknem o zmiennym rozmiarze, w którym stosowana jest kaskada detektorów HAAR. HAAR sekwencyjnie porównuje jasności pomiędzy wyznaczonymi elementami obrazu.

![[Pasted image 20260128193945.png]]

Oznacza to, że jeśli jakiś detektor po drodze w danym oknie stwierdzi "tu nie ma twarzy" to poszukiwanie w tym oknie się skończy i idzie się dalej. Po przejściu przez wszystkie detektory kaskadowe, znalezieniu wszystkich oczekiwanych cech, dostaje się rezultat: "tu może być twarz".

![[Pasted image 20260128193605.png]]

Takie pierwsze odfiltrowanie kaskadą HAAR jest szybkie i pozwala na odrzucenie większości nie-twarzy. Po tej wstępnej klasyfikacji można użyć silniejszych metod.

Zaczyna się od najpostszych możliwych cech HAAR - tych "najlepszych", najlepiej odróżniających twarze od nie-twarzy. Im dalszy stopień kaskady tym bardziej rygorystyczne są cechy. Silny klasyfikator jest kombinacją liniową poszczególnych słabych klasyfikatorów HAAR: 

$H(u)=\sum^S_{s=1}\alpha_sh_s(u)$
$h_s(u):$ pojedynczy słaby klasyfikator HAAR
$\alpha_s:$ waga tego klasyfikatora
$S:$ liczba słabych klasyfikatorów

https://www.youtube.com/watch?v=zokoTyPjzrI

Ważna cecha tej metody to **obraz zintegrowany** - suma poszczególnych wielkości w pikselach. Dzięki obrazowi zintegrowanemu, obliczanie różnic między jasnymi i ciemnymi obszarami w cechach HAAR (np. prostokąty białe minus czarne) jest szybkie.. Cechy HAAR są skalowane tak, aby wykryć twarze o różnych rozmiarach i przesuwane od lewego górnego rogu.

![[Pasted image 20260128194310.png]]
![[Pasted image 20260128194416.png]]
#### Ada Boost
Ada Boost (Adaptive Boosting) to algorytm uczenia maszynowego, który tworzy silny klasyfikator poprzez połączenie wielu słabych klasyfikatorów w kaskadzie. Dla każdego stopnia kaskady dobiera się cechę i wagę. Każdy kolejny klasyfikator koryguje błędy poprzedniego, nie-twarze z poprzednich kroków są ignorowane.

Na początku akceptuje się dosyć dużo potencjalnych błędów i ustawia się niskie FRR ($\approx10^{-6}$), w kolejnych stopniach próg jest podwyższony, aby zmniejszyć FAR. **Ostatecznie, Ada Boost służy do wybierania najlepszych cech HAAR i określenia ich wagi.**

#### Inne metody
1. **Indeksy antopometryczne**
   >Jeśli mówimy o landmarkach to ważne tu są morphy. Standardowo, 44/68 punkty charakterystyczne twarzy, 58 indeksów. Jest norma.
2. **Lokalne wzorce binarne LBP/LBPH**
   >Wykorzystywany w wielu metodach identyfiakcji obrazów. Leciutka. Jest odporna na zmianę jasności. Jeśli prześwietlimy obraz, LBP sobie poradzi.
   >
   >Działa na bardzo małych blokach i analizuje obraz w odcieniach szarości. Powstaje 256 wzorców binarnych, na podstawie których "jeździ się" po obrazie. Piksel środkowy, referencyjny, jest porównywany z sąsiadami. Cały blok jest opisywany jedną liczbą - zamiast przechowywać informacje o 9 pixelach, wystarczy 1.
   >
   >![[Pasted image 20260128195550.png]]
   >
   >Wzorcem jest stwierdzenie, czy w danych miejscach występują krawędzie i jak szybko się zmieniają. Histogram mówi ile jest wzorców binarnych na danym obrazie lub w danym segmencie. Podział obrazu na segmenty dla wiele małych histogramów. Zdefiniowano wzorce jednorodne - dwa przejscia z 0 w 1 lub z 1 w 0.  
   >https://www.youtube.com/watch?v=wpAwdsubl1w
3. **Transformacje cech niezmiennych w skali**
4. **HoG - histogram gradientów zorientowanych**
5. **Twarze Fishera**

#### Eigenfaces - twarze własne
Bazę $N$ obrazów twarzy o wymiarach $J*K$ da się zareprezentować przez wektory $x_1,...,x_n \in R^m,m=JK$. Zbiór obrazów scharakteryzujemy jako centrum. Rozrzut wokół niego wykorzystuje średnią i sumę kwadratów odchyłek. W takim razie twarz średnia $\bar{x}=\frac{1}{n}\sum^n_{i=1}x_i$, czyli po prostu suma ze wszystkich wektorów reprezentujących bazę twarzy.

![[Pasted image 20260128200804.png]]

Baza $N$ ($x_1,...,x_M$) obrazów, gdzie każdy z nich tworzy wektor w przestrzeni $R^m,m=JK$ - jeden wektor o $JK$ wymiarach na twarz.

![[Pasted image 20260128200816.png]]

Można "policzyć średnią twarz" $\mu$, którą można "odjąć" od twarzy z bazy $N$ i dzięki temu każda z twarzy może być zapisywana jako odchylenie od twarzy średniej. Pozwala to zachować dużo miejsca, ponieważ zapisuje się jedynie cechy charakterystyczne (odstępstwa $\hat{x}$).

![[Pasted image 20260128201403.png]]
![[Pasted image 20260128201309.png]]![[Pasted image 20260128201318.png]]

https://www.youtube.com/watch?v=jQOZrXZTXcw
https://www.youtube.com/watch?v=JqEI0-RCC8w
https://www.youtube.com/watch?v=lhMIoikBCDA