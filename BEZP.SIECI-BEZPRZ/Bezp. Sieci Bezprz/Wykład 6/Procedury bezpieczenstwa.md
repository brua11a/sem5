"Wykład skomplikowany"
Pokaże, gdzie szukać problemów.

Procedury bezpieczeństwa w Bluetooth mamy 3-4, mogą być na poziomie łącza (gdy nie ma jeszcze fizycznego połączenia) lub na poziomie usługi (jeszcze przed usługami ale po fizycznym połączeniu), wcześniej albo później.

Od 2.1 dopiero jest prawdziwe zabezpieczenie, trzy trybu w 2.0 są słabe.

##### Tryb 1
Archaiczny, nie używać. Brak uwierzytelnienia i szyfrowania. Łączy się z każdym co tego chce. Na poziomie łącza

##### Tryb 2
Autoryzacja, ale mechanizmy podczas parowania, w których można przechwycić klucze. Autoryzacja może być wykonywana już po usługach - jest to złe. Na poziomie usługi.

##### Tryb 3
Wszystko jest szyfrowane i uwierzytelniane, jeśli kontroler się zgodzi to można ewentualnie wykryć usługi bez uwierzytelniania. Na poziomie łącza.

##### Tryb 4
Tego chcemy używać. Na poziomie usługi. Wykorzystuje mechanizm SSP - wykorzystuje krzywe eliptyczne do generowania kluczy. Połączenie będzie autoryzowane i bezpieczne. Dla usługi mogą być wybrane konkretne zabezpieczenia na podstawie poziomu - jeśli się da to jak najwyższy (4).
Od BLE 4.1 możemy czuć się bezpieczni.

Jeśli tylko się da, używaj 4, w innym wypadku 3. Nigdy 1 i 2.

### Parowanie i generowanie kluczy
Uwierzytelnianie i szyfrowanie odbywa się przy użyciu klucza symetrycznego - Link Key lub Long Term Key (zależy od wersji, nazwa inna ale dziala podobnie).

W trybie legacy do parowania wykorzystywany jest PIN. Dwa urządzenia jednocześnie dostarczają klucze Link Key po wpisują PIN, jeśli PIN jest za krótki to trzeba go uzupełnić poprzez BD_ADDR. Na podstawie tego powstają klucze inicjalizacyjne. Po wygenerowaniu kluczy, obydwie strony liczą randomową liczbę i wymieniają się nimi

Nowe: SSP, wprowadza cztery rodzaje parowania.
1. Parowanie numeryczne - porównanie dwóch liczb, nie jest ona brana pod uwagę podczas generacji klucza, użytkownik tylko potwierdza czy chce sparować urządzenia.
2. Wprowadzenie klucza - używane gdy jedno urządzenie ma wyświetlacz ale nie ma klawiatury, a drugie ma. Podobne.
3. Just Works - często uznawane za niebezpieczne, nie potwierdzamy niczego po prostu połączenie jest akceptowane. Przykład - słuchawki bezprzewodowe
4. Out of Band - najfajniejsze, inną technologią (np. NFC) potwierdza się to, że parowanie ma być wykonane.

Klucz SSP publiczny i praywatny jest generowany w środku na podstawie parametrów urządzenia. Podczas parowania urządzenia wybierają jeden z tych 4 trybów. Obliczane są E1 i E2, wysyłane nawzajem, druga strona weryfikuje. Sam klucz nigdy nie jest wysyłany. Uwierzytelnianie jest wykonywane na podstawie challenge-response. Są dwa tryby:
1. **Legacy** - urządzenie zaczyna procedurę w postaci przesłania liczby do weryfikowanego urządzenia, liczy się oczekiwaną odpowiedź, otrzymuje się rzeczywistą odpowiedź i są porównywane. Nie jest odsyłana całość - tylko 32b, reszta służy do generowania klucza szyfrujacego. Trzeba to zrobić 2x zeby zweryfikować obydwie strony
2. **Secure (od wersji 2.0)** - Master i Slave wysylaja sobie losowa liczbe, liczona jest odpowiedz uwierzytleniajaca, 32b się odsyla w druga strone 96b uzywa sie do generowania klucza szyfrowania symetrycznego. "W dwie strony jednocześnie"

==**To, co trzeba wiedzieć, to że do szyfrowania wykorzystuje się te 96 bitów z klucza wyliczonego wcześniej podczas uwierzytelniania.**== - *Kowal, brzmi jak cos co ma być na kolosie*

### Zaufanie
Zaufane urządzenie ma stałe powiązanie z innym i pełny dostęp do usług.
Niezaufane urządzenie nie ma powiązania i ma ściśle ograniczony dostęp.
Dla trybu 1 i 3 nie ma zdefiniowanych poziomów bezpieczenstwa.
Dla trybu 2 wymagane jest uwierzytelnianie, szyfrowanie i autoryzacja.