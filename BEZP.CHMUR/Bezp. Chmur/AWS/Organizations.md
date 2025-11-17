**AWS Organizations** to usługa zarządzania **kontami AWS** (NIE [[Użytkownik|UŻYTKOWNIKAMI]]), która umożliwia tworzenie organizacji w celu **konsolidacji wielu kont** i ich **centralnego zarządzania**. Pozwala ona na scentralizowane tworzenie i administrowanie kontami oraz korzystanie ze **wspólnego rozliczania (consolidated billing)**, co ułatwia kontrolę kosztów, zgodności i bezpieczeństwa w całej organizacji.

AWS Organizations umożliwia **hierarchiczne grupowanie kont** w jednostki organizacyjne (**Organizational Units – OUs**) i przypisywanie do nich różnych polityk dostępu. Dzięki temu można tworzyć precyzyjne, dostosowane do potrzeb polityki i stosować je do pojedynczych lub wielu jednostek organizacyjnych. Struktura OUs może być zagnieżdżana do pięciu poziomów, co pozwala elastycznie odwzorować hierarchię organizacyjną firmy.

Jedną z kluczowych funkcji Organizations jest możliwość stosowania **Service Control Policies (SCPs)**, które definiują **maksymalny zakres uprawnień** dla kont członkowskich w organizacji. SCP nie przyznają uprawnień - służą jedynie do ich ograniczania. Oznacza to, że jeśli dane działanie jest zablokowane przez SCP, nie może być wykonane, nawet jeśli polityka IAM na poziomie konta na to pozwala.

![[Pasted image 20251112160636.png]]

AWS Organizations rozszerza możliwości zarządzania IAM, wprowadzając dodatkową warstwę kontroli na poziomie konta lub grupy kont. Dzięki temu zapewnia, że użytkownicy i role mogą wykonywać tylko te działania, które są dozwolone zarówno przez polityki IAM, jak i przez SCP - jeśli którakolwiek z tych polityk blokuje operację, użytkownik nie uzyska do niej dostępu.

**AWS Organizations działa ponad IAM - na poziomie całej organizacji złożonej z wielu kont AWS**