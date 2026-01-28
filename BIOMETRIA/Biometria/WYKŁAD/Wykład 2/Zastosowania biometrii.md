### Mamy być podejrzliwi - uważać, czy producenci nie za bardzo polegają na biometrycznym hype i wpychają ją bez sensu.

##### Case 1: Touch ID - dostęp do urządzeń mobilnych
Czytnik nie zczyta całego palca, jedynie wycinek. Podczas pierwszego odczytu uzupełniamy profil o kształty swojego palca. System nie próbuje bazować na np. 90% palca tylko na małej jego części - możemy dać palec bokiem a i tak odblokuje. 

Jest to system *blackboxowy* - nie są znane parametry tego systemu. Znamy jedynie rozwiązanie, które dostaliśmy bez jego specyfikacji. W każdym telefonie logowanie dotykiem będzie zupełnie inaczej to działać. 

Aplikacja deleguje sprawdzanie biometrii do systemu operacyjnego - nie bank, nie centrala żadna. Jedyne co zwraca system to "git/nie-git". Bezpieczeństwo tego systemu biometrycznego nie polega na samym systemie, tylko od jakości samego sprzętu - poważny błąd, zabezpieczenie jest *hardware-dependant*. 

##### Case 2: Ciągła weryfikacja w bankowości
Część banków implementuje systemy ciągłej weryfikacji biometrycznej. System monitoruje wzorce behawioralne użytkownika podczas korzystania z aplikacji - sposób trzymania telefonu, tempo pisania, charakterystyczne gesty, naciski na ekran, nawet kąt nachylenia urządzenia.

Rozwiązanie działa cicho w tle przez cały czas sesji i może wykryć podejrzane zachowania nawet po poprawnym zalogowaniu. Jeśli system stwierdzi, że użytkownik zachowuje się nietypowo (np. ktoś inny trzyma telefon), może zablokować dostęp do wrażliwych operacji lub wymusić ponowne uwierzytelnienie.

##### Case 3: Karta płatnicza
Niektóre karty płatnicze posiadają wbudowany czytnik linii papilarnych, który pozwala na weryfikację użytkownika poprzez dotyk zamiast PIN-u. Karta ma wbudowany mikroprocesor i czytnik (zwykle pojemnościowy), który weryfikuje odcisk lokalnie - dane nie wychodzą z karty. Rejestracja odcisku odbywa się przez specjalną aplikację lub w oddziale banku. W Polsce rozwiązanie jest mało powszechne.

##### Case 4: Tokeny hardware'owe
Tokeny hardware'owe (np. Yubikey Bio, Feitian BioPass) czytają odciski palca do weryfikacji tożsamości użytkownika. Czytnik może być **optyczny** (skanuje obraz palca przy użyciu światła LED i kamery) lub **pojemnościowy** (mierzy różnice w przewodności elektrycznej między grzbietami a dolinkami linii papilarnych - bardziej precyzyjny i trudniejszy do oszukania).

Trzeba dotknąć odpowiednim, wcześniej zarejestrowanym palcem, by zweryfikować tożsamość i umożliwić działanie tokena - można zarejestrować kilka palców jako backup.