https://www.youtube.com/watch?v=xD88Qs_DZp4

Omawiamy "konkretną modalność biometryczną", a raczej tylko konkretne przykłady tego, jak podejść do linii papilarnych.

![[Pasted image 20260128114327.png]]

Zaczęło się od metody Henry'ego Fauldsa - polegała na analizie odcisków wszystkich 10 palców i przypisywanie ich do klasy, osobliwości (*Arch, Plain Arch, Ulnar Loop* itd). Nie przeszło.
Potem FBI rozwinęło AFIS - automatyczna identyfikacja na bazie odcisków. 2009 - Indie wprowadzają UIDAI. 2014+ - na smartphone Apple pojawia się dotykowy Apple Pay.

![[Pasted image 20260128144427.png]]

Kiedyś zbierało się odciski tylko osób poszukiwanych, teraz mamy odciski większości osób.
#### Rodzaje czytników odcisków palców
1. **Optyczne**
   >Zdjęcia palca przyłożonego do sensora. Grzbiety absorbują światło, doliny odbijają. Wady: zanieczyszczenia, łatwy do oszukania, mała odporność mechaniczna, duża powierzchnia czytnika.
2. **Pojemnościowe**
   >Zasada działania opiera się na różnicach pojemności w zależności od odległości pomiędzy czujnikiem a doliną/grzbietem. Wady: małą odporność na wyładowania elektrostatyczne, łatwy do oszukania
   >
   >Matryca CCD/CMOS poprzez dotknięcie palcem siatki powoduje ułożenie się ładunku na bruzdach i dolinach - zmienia się pojemność elektryczna przy dotyku. Główny parametr, który ma znaczenie to rozdzielczość.
1. **Ultradźwiękowe (mogą być bezstykowe!)**
   >Bazują na zjawisku rozpraszania kontaktowego. 10-krotnie lepsza jakość pomiaru.
2. **Termiczne**
   >Różnica temperatur pomiędzy grzbietami a powietrzem złapanym w doliny. Sensor typu przemiatającego. Obraz składany jest z wąskich fragmentów. Mały rozmiar sensora. Wady: szybkie wyrównanie temperatur pomiędzy palcem a czujnikiem. Zalety: duża odporność na oszustwa.
   >
   >Pomiar termiczny wykorzystuje materiały piroelektryczne, co mierzy temeraturę w strukturze bruzdowo-dolinowej. Ludzkie ciało jest przewodnikiem a więc grzeje, powietrze jest izolatorem a więc nie grzeje, a powietrze znajduje się w dolinach odcisku palca.

Nieważne jaka jest metoda porównywania, rezultaty powinny być podobne niezależnie od przesunięcia odcisku, obrotu, wywartego nacisku czy sprężystości skóry. 
#### Poziomy obserwacji odcisku
1. **Podstawowe** - grzbiety i doliny
2. **Globalne** - rdzeń i osobliwości (*arch, arch plain, ulnar loop*)
   >Punkty osobliwe to globalny parametr ludzkich palców. Prawdopodobieństwo ich wystąpienia to: 30% wir, 64% delta, 6% łuk.
   >**Rdzeniem jest najbardziej wysunięty na północ punkt osobliwy, służy do "wyrównania" odcisku i stworzenia punktu odniesienia.**

   >![[Pasted image 20260128145418.png]]
1. **Lokalne** - **minucje**, detale Galtona, zakończenia i rozwidlenia linii papilarnych oraz ich ułożenie, a także charakterystyczne ich formacje
   >![[Pasted image 20260128145425.png]]
2. **Szczegółowe** - pory, brodawki, zmarszczki, blizny, pozwala na uwzględnienie fragmentów palca
   >![[Pasted image 20260128145433.png]]

#### Generyczny schemat:
1. **Odcisk surowy**
2. **Filtr/normalizacja**
   >Zależy nam na tym, żeby mieć odcisk w notacji o pozycji ustalonej N-S. Może nam zależeć na uwypukleniu grzbietów i dolin (selektywność kierunkowa i częstotliwościowa, transformaty Fouriera, przekształcenie falkowe) a także wyrównanie jasności i ostrości obrazu (histogram, filtr Laplace'a). Wyrównanie histogramu może polegać na "rozciągnięciu" nasycenia na całe spektrum przestrzeni tonalnej.
   >
   >![[Pasted image 20260128152350.png]]
3. **Wzmocniony obraz odcisku**
4. Binaryzacja wg. **LOKALNEGO** progu - próg adaptywny lokalny, patrzy się fragment po fragmencie i ustala próg na podstawie średniego nasycenia.
5. **Monochrom**
6. **Ścinanie krawędzi**
7. **Obraz odcisku pocieniony**

#### Liczenie obrazku kierunkowego
Jest to pole gradientu dyskretnego (zmiany kierunków w pionie i poziomie) w "blokach" 8x8 pikseli na spreparowanym obrazie odcisku palca. Najpierw liczy się gradienty, potem je uśrednia.

$\nabla(x_i,y_i)=[\nabla x(x_i,y_i),\nabla y(x_i,y_i)]$

Po policzeniu dla każdego bloku takiego gradientu to zobaczymy +- jak te linie przebiegają. Wtedy nie trzeba patrzeć na każdy piksel osobno tylko porównywać blok do bloku. "Na linie papilarne naniesione są pola 8x8, ukierunkowane".

![[Pasted image 20260128151309.png]]

Do szukaniu **indexów Poincare** wykonywane jest 8 obliczen, które pozwala zidentyfikować obszar. Bloki dookoła obranego bloku są sprawdzane pod względem ukierunkowania, na podstawie wykonanego "obrotu" definiowany jest kształt - osobliwości. 

Np. obrót 360 oznacza wir, a obrót 180 oznacza pętlę.

![[Pasted image 20260128151322.png]]

#### Wykrywanie minucji
Jak już mamy binarny obraz to wystarczy przeszukać pixele. Czarny - na linii, biały - nie na linii. Jeśli ma dwóch sąsiadów, jest w środku linii. Jeśli ma tylko jednego sąsiada, to jest to grzbiet. Jeśli ma więcej niż dwóch sąsiadów, mamy rozwidlenie.
Da się też estymować z obrazu w skali szarości, ale jest to o wiele trudniejsze.

![[Pasted image 20260128152203.png]]

Przed analizą należy jednak zespolić obraz, ponieważ filtracja i ścinanie tworzy artefakty. Jednym z zalecanych działań jest wycięcie wszystkiego, co jest na krawędzi obrazu, bo tam będzie dużo dużo błędów.

Należy też brać od uwagę, że przecięta osoba ma 10-100 minucji (realistycznie 30-40). Odcisk z 100+ minucjami nie ma znamion autentycznego odcisku. Trzeba testować żywotność i autentyczność danych.

Nie bawimy się obrazami, które są ciężkie, tylko weksportowanymi cechami w szablonie - na przykład typ minucji 3bit, współrzędne (x,y) (9bit,9bit), kąt 8bit. Taki szablon będzie miał około 40bit dla każdej minucji.

Po wyekstraktowaniu minucji, oryginalny obraz nie jest już do niczego potrzebny. Do porównywaniu wzorca z próbką biometryczną będą służyły jedynie minucje, a konkretnie dystansy między nimi.

#### Jak oceniać podobność odcisków do siebie
Staramy się dopasowywać wzorce punktowe. Im więcej się uda dopasować między wzorcem a szablonem tym lepiej, na podstawie progu (np. 20 pasujących minucji) jest podejmowana decyzja. 

Popularna metoda to Transformata Hough'a, która polega na szukaniu *maksimum tablicy akumulatorowej*. Należy sprawdzić, czy dwa kąty znajdują się w pewnym dopuszczalnym "okręgu", czy odległość między punktami wzorca i porównawcza jest w dopuszczalnym range.

Czy pierwszą minucję da się porównać z drugą minucją? Czy mają podobny kąt i podobne współrzędne?
Każda próbka $m_i$ z wzorca $W$ ma współrzędne i kąt $m_i=\{x_i,y_i,\phi_i\}$.
Podobnie z próbkami $m'_i$ z wzorca porównawczego $P$.

$s(m'_j,m_i)=\sqrt{(x'_j-x_i)^2-(y'_j-y_i)^2} \leq r_0$
$d(m'_j,m_i) = \text{min}(|\phi_j'-\phi_i|, 360^o - |\phi_j'-\phi_i|) \leq \phi_0$

**Czyli ustalamy progi:**
- jaki dystans $r_0$ dopuszczamy między minucjami
- jaki obrót $\phi_0$ dopuszczamy między minucjami
- ile minucji wymagamy $D_n = \text{THRESHOLD}$

![[Pasted image 20260128152611.png]]

Zależy nam na dopasowaniu minucji w sposób taki, żeby wynik był jak najlepszy - maksymalne, najlepsze dopasowanie. Funkcja zwraca ilość pasujących minucji w najlepszym wypadku. Może działać poprzez sprawdzenie "każdy z każdym" i czasem nawet się tak robi.

Deformacje liniowe są dla nas "spoko" bo nie zmieniają odległości między punktami, ale deformacje nieliniowe są problemem. Przez nie wzorzec może zostać zdeformowany jeśli nie przewidujemy takiej sytuacji. Sposobem jest np. ustalenie jakiegoś tolerance box dookoła minucji.