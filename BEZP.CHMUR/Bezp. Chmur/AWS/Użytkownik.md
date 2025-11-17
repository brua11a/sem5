Użytkownik [[IAM]] to trwała tożsamość tworzona w ramach konta AWS. Reprezentująca konkretną osobę lub aplikację, która potrzebuje stałego dostępu do usług i zasobów w chmurze. Każdy użytkownik posiada swoje unikalne credentiale, takie jak hasło umożliwiające logowanie do AWS Management Console lub klucze dostępowe wykorzystywane do połączeń programowych przez API, CLI czy SDK.

Po utworzeniu użytkownik nie ma domyślnie żadnych uprawnień i dopiero przypisanie mu odpowiednich [[Policy|polityk IAM]], przynależność do [[Grupa|grup]] albo czasowe przejęcie [[Rola|roli]] pozwala na wykonywanie określonych działań.

Pierwszym użytkownikiem w systemie jest użytkownik AWS account *root user*, posiadający pełny, nielimitowany dostęp do wszystkich zasobów.

**Konto AWS i użytkownik IAM to NIE TO SAMO**

Konto AWS to **cały** twój AWS, który może zawierać wiele zasobów i wielu użytkowników, natomiast użytkownik IAM to **konkretna tożsamość** utworzona wewnątrz tego konta, służąca do uzyskiwania dostępu do usług i zasobów.

Oznacza to, że dwa różne konta AWS to dwa różne środowiska.

**Podmiotem** jest osoba lub aplikacja wykorzystująca konto użytkownika IAM, AWS root lub przyjętą rolę żeby wykonywać requesty do AWS. Taki request będzie się składał z *kontekstu*, a konkretnie:
- akcji, która ma być wykonana
- zasobu, na którym akcja zostanie wykonana
- podmiotu wysyłajacego request
- danych dodatkowych, takich jak adres IP, user agent, SSL, timestamp
- danych dotyczące zasobu

Na podstawie tych elementów AWS przyznaje albo odmawia zapytaniu.