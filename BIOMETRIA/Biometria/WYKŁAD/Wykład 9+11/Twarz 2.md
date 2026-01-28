[[Twarz]]

Twarz ma określoną ilość landmarków, a także indeksy antopometryczne - to nie odległości same w sobie, to raczej będzie np. "odległość między oczami w proporcji do odległości między oczami a ustami", co pozwala skalować obraz a i tak identyfikować osobę. Takich indeksów może być DUŻO. "Stałym" landmarkiem są uszy, a także lewy kącik ucha - nie ruszają się. Zamknięte oczy to bardzo mała odległość między powiekami.

#### Problemy

Sama detekcja twarzy - wiele podejść. Na wykładzie omawiane są też piramidy obrazów (przesuwane okna po obrazie), "głosowanie" sieci neuronowych, ale przede wszystkim metoda Viola-Jones.

Analiza obrazu w oknach o różnych położeniach - te okra są przesuwane po całym obrazie i skalowane aż "cechy" zostaną znalezione. Odpowiada na pytanie "twarz/nie-twarz". Po przejściu przez proste klasyfikatory pojedyncze, wykorzystuje bardziej skomplikowane. Zaczyna się od cech HAAR - porównanie jasności między konkretnymi elementami obrazu, potencjalnie twarzy. Te cechy HAAR są badane sekwencyjnie w różnych położeniach i rozmiarach. Jeśli odpowiedź klasyfikatora jest "git, twarze mogą tak wyglądać" to idzie się dalej aż do momentu w którym znajdzie się cechę twarzy, której na obrazie nie znaleziono. Po przejściu przez cały proces, dostaje się odpowiedź "to prawdopodobnie jest twarz".

Prosty klasyfikator wykonuje pierwsze filtrowanie. 
https://www.youtube.com/watch?v=uEJ71VlUmMQ

Zaczyna się od najpostszych możliwych cech HAAR - tych "najlepszych", najlepiej odróżniających twarze od nie-twarzy. Im dalszy stopień kaskady tym bardziej regorystyczne są cechy. 

Ważna cecha tej metody to obraz zintegrowany - suma poszczególnych wielkości w pikselach. Cechy HAAR są skalowane tak, aby wykryć twarze o roznych rozmiarach i przesuwane od lewego gornego rogu.

#### Ada Boost
Niski FRR dla pierwszych stopni klasyfikacji HAAR (około 10^(-6)). Pierwszy stopień kaskady odrzucał 60% nie-twarzy, ostatecznie FAR 0.3%. 

#### Inne metody
1. Indeksy antopometryczne
   >Jeśli mówimy o landmarkach to ważne tu są morphy. Standardowo, 44/68 punkty charakterystyczne twarzy, 58 indeksów. Jest norma.
2. Lokalne wzorce binarne LBP/LBPH
   >Wykorzystywany w wielu metodach identyfiakcji obrazów. Leciutka. Jest odporna na zmianę jasności. Jeśli prześwietlimy obraz, LBP sobie poradzi. Działą na bardzo małych blokach i analizuje obraz w odcieniach szarości. Powstaje 256 wzorców binarnych, na podstawie których "jeździ się" po obrazie. Piksel środkowy, referencyjny, jest porównywany z sąsiadami. Cały blok jest opisywany jedną liczbą - zamiast przechowywać informacje o 9 pixelach, wystarczy 1. Wzorcem jest stwierdzenie, czy w danych miejscach występują krawędzie i jak szybko się zmieniają. Histogram mówi ile jest wzorców binarnych na danym obrazie lub w danym segmencie. Podział obrazu na segmenty dla wiele małych histogramów. Zdefiniowano wzorce jednorodne - dwa przejscia z 0 w 1 lub z 1 w 0.  
   >https://www.youtube.com/watch?v=wpAwdsubl1w
3. Transformacje cech niezmiennych w skali
4. HoG - histogram gradientów zorientowanych
5. Twarze Fishera

# UZUPELNIJ MATERIALY OD WODO PRZEJRZYJ W DOMU