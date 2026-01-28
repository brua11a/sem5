Keystroking nie dotyczy tylko klawiatury - chodzi o interakcję podczas korzystania z urządzenia. Zalicza się touchpad, mysz, klawiaturę itd. Każde z tych urządzeń ma jakieś "mierzalne" elementy, na podstawie których można stworzyć profil użytkownika wraz z jego zachowaniami. **Mowa tu o biometrii behawioralnej - działanie człowieka w różnych kontekstach.**

Biometria behawioralna pozwala na ciągłą weryfikację, transparentne pobieranie danych od użytkownika (dzieje się to "przy okazji" na sprzęcie, którego użytkownik już używa), łatwo się ja uczy i poprawia, a także na podstawie tych samych danych można zbudować wiele modeli.

Keystroking jest dobrym **drugorzędnym systemem uwierzytelniania, ale nie jako samodzielny mechanizm** - duże FAR/FRR. Wynika to ze zmiennych czynników, takich jak typ interfejsu wejściowego, znajomosci tego interface (i wpisywanego tekstu) oraz stan psycho-fizyczny. 
Uczenie się nowego środowiska będzie szybkie, ale na początku "ekspertyza" będzie niska. Wzorzec zatem powinien powstawać wtedy, kiedy użytkownik już dużo się nie polepsza.

W bankach różne biometrie są testowane - keystroking może służyć do wykrywania pewnych anomalii w zachowaniu użytkownika.

### Co mierzyć na klawiaturze
Najłatwiej mierzyć zdarzenie **KEY-DOWN** i **KEY-UP**, na tego podstawie (i znaczników czasu)
można policzyć znaczniki **Dwell Time** (ile trzyma się jeden przycisk) i **Flight Time** (ile trwa przejście od przycisku do przycisku). Są one liczone "pomiędzy" konkretnymi przyciskami. Można też liczyć WPM. 

Dwa następujące po sobie klawisze to digrafy. W alfabecie angielskim 26 znaków, 2 symbole da wariację z powtórzeniami - $W^2_{26}$, czyli ZA to nie to samo co AZ. Rozkład jest "rzadki" - części digrafów używa się cały czas, części wcale. Zależy to też od języka. Udział pewnych digrafów będzie mniejszy niż innych - różna te z większym udziałem, częstsze, będą "ważniejsze". Nie jest to jednak takie czarno białe - jeśli *rzadki* digraf ma małą wariancję, ale zawsze jest pisany tak samo przez tego użytkownika, to ten digraf może identyfikować osobę lepiej, niż ten częściej się pojawiający.

**Trigrafy** dadzą wariancję (NIE wariancja - jest to odchylenie od średniej)  $W^3_{26}=26^3$ czyli 17576 możliwości -> zza, aaz, aza. 

Wielu autorów rozkład digramów próbowało modelować rozkładem normalnym, lecz bez jednoznacznego kontekstu nie jest to uzasadnione. Np. w języku polskim digraf dla "ie" będzie wyglądał jak wielbłąd dla wszystkich zastosowań. Żeby rozkład normalny miał sens, trzeba się ograniczyć do np. "zastosowanie digrafu ie tylko jako końcówki słowa". 

![[Pasted image 20260128153517.png]]

Rozkład digrafów można "przyciąć" poprzez usunięcie skrajnych odchyleń - pozwoli to stworzyć dokładniejszy rozkład, lepiej opisujący typowe zachowanie użytkownika.

### Mysz
**Podczas badania myszy można badać:**
- szybkość ruchów
- pokonywane wektory przemieszczeń
- liczbę kliknięć w jednostkach czasu
- intensywność ruchów
- pole odwiedzonych powierzchni

Każdy interfejs "sterujący kursorem" będzie miał swoje cechy, zatem ustandaryzowanie tego wymaga ustalenia co potrafią wszystkie takie urządzenia - ruszać kursorem i klikać. 

W przypadku ruchu myszą mogą pojawić się "ruchy niemerytoryczne" - kręcenie kursorem z nudów. Może to też służyć do identyfikacji. 

![[Pasted image 20260128152959.png]]

Touch screen dodatkowo poza informacjami o samym ruchu możemy traktować ekran jako prosty czytnik pojemnościowy - element fizyczny (np. grubość palca), połączenie behawioru z fizycznością. Oceniane są *slide'y, tap'y* oraz *drag-and-drop'y*. 
### Ochrona danych
Musimy coś pisać, robić, cokolwiek, żeby tworzyć wzorzec. Jednocześnie chcemy te dane chronić przed innymi. Obosieczne podejście. Dane (w tym wypadku np. digrafy) należy przechowywać, ale anonimizować. Będzie do tego służyć **funkcja perturbacji - nieodwracalna, z sekretnym kluczem**.

Dane przed trafieniem do jakiejś bazy danych są zaszumiane funkcją perturbacji, która je przekształca. Jeśli ktoś to wykradnie i będzie próbował się podszywać pod tożsamość z bazy, nie dopasuje się, ponieważ próbując się zidentyfikować znowu dokonana zostanie perturbacja - _perturbacja perturbacji_.

To, jak ma się perturbować, określa klucz zewnętrzny (auxiliary). Może to być jakaś "sól" w systemie, może być podawany z zewnątrz przy każdej próbie weryfikacji. Wszystko to ma związek z **anulowalnymi biometrykami** - stary wzorzec nie jest powiązany z nowym, jeśli zmieni się klucz.

Podsumowując, nasza rzeczywista tożsamość nie jest przechowywana. Zamiast tego w bazie jest nasza tożsamość przekształcona przez funkcję perturbacji i KLUCZ. Inny klucz daje de facto inną tożsamość, nawet z tą samą "rzeczywistą" tożsamością i tą samą funkcją. Pozwala to anulować starą tożsamość i nadpisać ją nową.

![[Pasted image 20260128153015.png]]![[Pasted image 20260128153026.png]]
### Claude wysryw na podstawie artykulu od Wodo (https://www.researchgate.net/publication/301282681_Identity_security_in_biometric_systems_based_on_keystroking)
#### 1. Constant Delay Algorithm (Algorytm stałego opóźnienia)

Zbiera zdarzenia klawiatury w buforze i uwalnia je jedno po drugim po upływie stałego czasu `d`. Generuje uniformiczne sekwencje timingów dla danych poniżej progu, powyżej działa natychmiastowo. Zapewnia wysoki poziom bezpieczeństwa, ale jest łatwo wykrywalny przez atakującego ze względu na regularny wzorzec. Bezużyteczny dla osób niemogących utrzymać minimalnego rytmu pisania.

---

#### 2. Random Noise Algorithm (Algorytm losowego szumu)

Dla każdego zdarzenia klawiatury losowo decyduje (p=0.5), czy będzie opóźnione i generuje losowe rozszerzenia timingów (15-70 ms). Tworzy wrażenie pisania przez prawdziwego użytkownika, co czyni go trudniejszym do wykrycia niż Constant Delay. Zapewnia tylko niewielki wpływ na timings i nie może zapewnić długich opóźnień, więc jest odpowiedni tylko dla dobrze wytrenowanych typistów.

---

#### 3. PUF Method (Physical Unclonable Function)

Używa funkcji PUF i hasła użytkownika do transformacji timingów między zdarzeniami klawiatury, zmieniając je maksymalnie o 128 ms. Umożliwia stworzenie wielu tożsamości keystroke i przełączanie się między nimi poprzez zmianę hasła. Nawet jeśli atakujący ma dostęp do urządzenia, nie może go sklonować ani połączyć różnych tożsamości użytkownika bez znajomości haseł. To realizacja anulowalnych biometryki - zmiana hasła generuje nową, niepowiązaną tożsamość.

---

#### 4. Binary Representation Probability Algorithm (Algorytm prawdopodobieństwa reprezentacji binarnej)

Probabilistycznie zmienia poszczególne bity w reprezentacji binarnej timingu, gdzie i-ty bit jest odwracany z prawdopodobieństwem p^(i+1). Mniej znaczące bity są zmieniane częściej niż bardziej znaczące, co daje naturalniejszą perturbację niż stałe opóźnienie. Parametr p kontroluje intensywność transformacji, pozwalając na balans między naturalnością a poziomem ochrony.