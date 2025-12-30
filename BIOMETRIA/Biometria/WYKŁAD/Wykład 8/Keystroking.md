Keystroking nie dotyczy tylko klawiatury - chodzi o interakcję podczas korzystania z urządzenia. Zalicza się touchpad, mysz, klawiaturę itd. Każde z tych urządzeń ma jakieś "mierzalne" elementy, na podstawie których można stworzyć profil użytkownika wraz z jego zachowaniami. Mowa tu o biometrii behawioralnej - działanie człowieka w różnych kontekstach.

Biometria behawioralna pozwala na ciągłą weryfikację, transparentne pobieranie danych od użytkownika (dzieje się to "przy okazji" na sprzęcie, którego użytkownik już używa), łatwo się ja uczy i poprawia, a także na podstawie tych samych danych można zbudować wiele modeli.

Keystroking jest dobrym drugorzędnym systemem uwierzytelniania, ale nie jako samodzielny mechanizm - duże FAR/FRR. Wynika to ze zmiennych czynników, takich jak typ interfejsu wejściowego, znajomosci tego interface (i wpisywanego tekstu) oraz stan psycho-fizyczny. 
Uczenie się nowego środowiska będzie szybkie, ale na początku "ekspertyza" będzie niska. Wzorzec zatem powinien powstawać wtedy, kiedy użytkownik już dużo się nie polepsza.

W bankach różne biometrie są testowane - keystroking może służyć do wykrywania pewnych anomalii w zachowaniu użytkownika.

### Co mierzyć na klawiaturze
Najłatwiej mierzyć zdarzenie KEY-DOWN i KEY-UP, na tego podstawie (i znaczniki czasu)
można policzyć znaczniki Dwell Time (ile trzyma się jeden przycisk) i Flight Time (ile trwa przejście od przycisku do przycisku). Są one liczone "pomiędzy" konkretnymi przyciskami. Można też liczyć WPM. 

Dwa następujące po sobie klawisze to digrafy. W alfabecie angielskim 26 znaków, 2 symbole da wariację z powtórzeniami - $W^2_{26}$, czyli ZA to nie to samo co AZ. Rozkład jest "rzadki" - części digrafów używa się cały czas, części wcale. Zależy to też od języka. Udział pewnych digrafów będzie mniejszy niż innych - różna "ważność". To też zależy - jeśli rzadki digraf ma małą wariancję, zawsze jest pisany tak samo, to może identyfikować osobę lepiej, niż teoretycznie częstszy digraf.

Trigrafy dadzą wariancję (NIE wariancja - jest to odchylenie od średniej)  $W^3_{26}=26^3$ czyli 17576 możliwości -> zza, aaz, aza. 

Wielu autorów rozkład digramów próbowało modelować rozkładem normalnym, lecz bez jednoznacznego konktekstu nie jest to uzasadnione. Np. w języku polskim digraf dla "ie" będzie wyglądał jak wielbłąd dla wszystkich zastosowań. Żeby rozkład normalny miał sens, trzeba się ograniczyć do np. "zastosowanie digrafu ie tylko jako końcówki słowa". 

Rozkład digrafów można "przyciąć" poprzez usunięcie skrajnych odchyleń - pozwoli to stworzyć dokładniejszy rozkład, lepiej opisujący typowe zachowanie użytkownika.

### Mysz
Podczas badania myszy można badać szybkość ruchów, pokonywane wektoery przemieszczeń, liczby kliknięć w jednostkach czasum intensywność ruchów, pole odwiedzonych powierzchni itd. Każdy interfejs "sterujący kursorem" będzie miał swoje cechy, zatem ustandaryzowanie tego wymaga ustalenia co potrafią wszystkie takie urządzenia - ruszać kursorem i klikać. 

W przypadku ruchu myszą mogą pojawić się "ruchy niemerytoryczne" - kręcenie kursorem z nudów. Może to też służyć do identyfikacji. 

Touch screen dodatkowo poza informacjami o samym ruchu możemy traktować ekran jako prosty czytnik pojemnościowy - element fizyczny (np. grubość palca), połączenie behawioru z fizycznością. Oceniane są slide'y, tap'y oraz drag-and-drop'y. 

### Ochrona danych
Musimy coś pisać, robić, cokolwiek, żeby tworzyć wzorzec. Jednocześnie chcemy te dane chronić przed innymi. Obosieczne podejście. Dane (w tym wypadku np. digrafy) należy zachowywać, ale animizować. Będzie do tego służyć funkcja perturbacji - nieodwracalna, z sekretnym kluczem. Dane przed trafieniem do jakiejś bazy danych są zaszumiane funkcją perturbacji, która je przekształca. Jeśli ktoś to wykradnie i będzie próbował się podszywać pod tożsamość z bazy, nie dopasuje się ponieważ próbując się zidentyfikować znowu dokonana zostanie pertutbacja - perturbacja z perturbacji. To, jak ma się perturbować jest klucz zewnętrzny, auxilary. Może to być jakaś "sól" w systemie, może być z zewnątrz przy każdej próbie wykonania. Wszystko to ma związek z **anulowalnymi biometrykami** - stary pattern nie jest powiązany z nowym jeśli zmieni się klucz. Podsumowując, nasza rzeczywista tożsamość nie jest przechowywana, zamiast tego w bazie jest nasza tożsamość przekształcona przez funkcję perturbacji i KLUCZ. Inny klucz daje de facto inną tożsamość nawet z tą samą "rzeczywistą" tożsamością i tą samą funkcją. Pozwala to anulować starą tożsamość i nadpisać ją nową.

