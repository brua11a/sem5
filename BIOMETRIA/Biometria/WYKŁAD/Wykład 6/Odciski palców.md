Omawiamy "konkretną modalność biometryczną", a raczej tylko konkretne przykłady tego, jak podejść do linii papilarnych.

Zaczęło się od metody Fauldsa - polegała na analizie odcisków wszystkich 10 palców. Nie przeszło.
Potem FBI rozwinęło AFIS - automatyczna identyfikacja na bazie odcisków
2009 - india wprowadza UIDAI
2014+ - smartphone

Kiedyś zbierało się odciski tylko osób poszukiwanych, teraz mamy odciski większości osób.

##### Klasyfikacja Henry'ego
Rozważane było 10 palców i każdy odcisk zostaje przypisany do klasy, np. *Arch, Plain Arch, Ulnar Loop* itd.

##### Rodzaje czytników odcisków palców
- optyczna
- pojemnościowe
- ultradźwiękowe (mogą być bezstykowe!)
- termincze

Matryca CCD/CMOS poprzez dotknięcie palcem siatki powoduje ułożenie się ładunku na bruzdach i dolinach - zmienia się pojemność elektryczna przy dotyku. Główny parametr, który ma znaczenie to rozdzielczość.

Pomiar termiczny wykorzystuje materiały piroelektryczne, co mierzy temeraturę w strukturze bruzdowo-dolinowej. Ludzkie ciało jest przewodnikiem a więc grzeje, powietrze jest izolatorem a więc nie grzeje, a powietrze znajduje się w dolinach odcisku palca.

#### Poziomy obserwacji odcisku
1. Podstawowe - grzbiety i doliny
2. Globalne - rdzeń i osobliwości (arch, arch plain, ulnar loop)
3. Lokalne - **minucje**, detale Galtona, zakończenia i rozwidlenia linii papilarnych oraz ich ułożenie, a także charakterystyczne ich formacje
4. Szczegółowe - pory, brodawki, zmarszczki, blizny, pozwala na uwzględnienie fragmentów palca

##### Poziom globalny
Punkty osobliwe: 30% wir, 64% deltam 6% łuk
Rdzeniem jest najbardziej wysunięty na północ punkt osobliwy, służy do "wyrównania" odcisku i stworzenia punktu odniesienia.

##### Pipeline przetworzenia odcisku
Od digitalizacji do identyfikacji, stworzenia szablonu. Pomysły to:

Policz obraz kierunkowy - uśredniaj w "porcjach" np. 8x8 przebieg linii papilarnych, dzięki temu po policzeniu dla każdego bloku takiego gradientu to zobaczymy +- jak te linie przebiegają. Wtedy nie trzeba patrzeć na każdy pixel osobno tylko blok do bloku. "Na linie papilarne naniesione są pola 8x8, ukierunkowane". Do szukaniu indexów Poincare wykonywane jest 8 obliczen, które pozwala zidentyfikować obszar. DOCZYTAJ BO ODLECIALEM. "Cztery sumowania jakieś założenie prosty algorytm nie wymaga fancy działań, działa szybko". Na poziomie lokalnym można wtedy wyróżnić różne struktury.

##### Generyczny schemat:
1. Odcisk surowy
2. Filtr/normalizacja
   >Zależy nam na tym, żeby mieć odcisk w notacji o pozycji ustalonej N-S. Może nam zależeć na uwypukleniu grzbietów i dolin (selektywność kierunkowa i częstotliwościowa, transformaty Fouriera, przekształcenie falkowe) a także wyrównanie jasności i ostrości obrazu (histogram, filtr Laplace'a). Wyrównanie histogramu może polegać na "rozciągnięciu" nasycenia na całe spektrum przestrzeni tonalnej.
3. Wzmocniony obraz odcisku
4. Binaryzacja wg. **LOKALNEGO** progu - próg adaptywny lokalny, patrzy się fragment po fragmencie i ustala próg na podstawie średniego nasycenia.
5. Monochrom
6. Ścinanie krawędzi
7. Obraz odcisku pocieniony

#### Wykrywanie minucji
Jak już mamy binarny obraz to wystarczy przeszukać pixele. Czarny - na linii, biały - nie na linii. Jeśli ma dwóch sąsiadów, jest w środku linii. Jeśli ma tylko jednego sąsiada, to jest to grzbiet. Jeśli ma więcej niż dwóch sąsiadów, mamy rozwidlenie.
Da się też estymować z obrazu w skali szarości, ale jest to o wiele trudniejsze.

Przed analizą należy jednak zespolić obraz, ponieważ filtracja i ścinanie tworzy artefakty. Jednym z zalecanych działań jest wycięcie wszystkiego, co jest na krawędzi obrazu, bo tam będzie dużo dużo błędów.

Należy też brać od uwagę, że przecięta osoba ma 10-100 minucji (realistycznie 30-40), zatem 100+ nie ma znamion autentycznego odcisku. Trzeba testować żywotność i autentyczność danych.

Nie bawimy się obrazami, które są ciężkie, tylko weksportowanymi cechami w szablonie - na przykład typ minucji 3b, wspolrzedne x y 9b 9b, kąt 8b. Taki szablon będzie miał około 40b ldla każdej minucji.

#### Jak oceniać podobność odcisków do siebie
Staramy się dopasowywać wzorce punktowe. Im więcej się uda dopasować między wzorcem a szablonem tym lepiej, na podstawie progu (np. 20 pasujących minucji) jest podejmowana decyzja. 

Popularna metoda to Transformata Hough'a, która polega na szukaniu *maksimum tablicy akumulatorowej*. Należy sprawdzić, czy dwa kąty znajdują się w pewnym dopuszczalnym "okręgu", czy odległość między punktami wzorca i porównawczy jest w dopuszczalnym range.

Czy pierwszą minucję da się porównać z drugą minucją? Czy mają podobny kąt i podobne współrzędne?
Każda próbka $m_i$ z wzorca $W$ ma współrzędne i kąt $m_i=\{x_i,y_i,\phi_i\}$.
Podobnie z próbkami $m'_i$ z wzorca porównawczego $P$.

$s(m'_j,m_i)=\sqrt{(x'_j-x_i)^2-(y'_j-y_i)^2} \leq r_0$
$d(m'_j,m_i) = \text{min}(|\phi_j'-\phi_i|, 360^o - |\phi_j'-\phi_i|) \leq \phi_0$

**Czyli ustalamy progi:**
- jaki dystans $r_0$ dopuszczamy między minucjami
- jaki obrót $\phi_0$ dopuszczamy między minucjami
- ile minucji wymagamy $D_n = \text{THRESHOLD}$

Zależy nam na dopasowaniu minucji w sposób taki, żeby wynik był jak najlepszy - maksymalne, najlepsze dopasowanie. Funkcja zwraca ilość pasujących minucji w najlepszym wypadku. Może działać poprzez sprawdzenie "każdy z każdym" i czasem nawet się tak robi.

Deformacje liniowe są dla nas "spoko" bo nie zmieniają odległości między punktami, ale deformacje nieliniowe są problemem. Przez nie wzorzec może zostać zdeformowany jeśli nie przewidujemy takiej sytuacji. Sposobem jest np. ustalenie jakiegoś tolerance box dookoła minucji.