Protokół uwierzytelniania stosowany do komunikacji z AAA. Spełnia podobną rolę, co [[TACACS+]], lecz są między nimi znaczące różnice:

1. Autentykacja jest połączona z autoryzacją, ale accounting jest osobno. Jeśli ktoś jest zautentykowany, to jest od razu autoryzowany.
2. Standard otwarty.
3. Komunikacja po UDP.
4. Mechanizm uwierzytelnienia opiera się na jednostronnym challenge-response - od servera RADIUS do klienta.
5. Szyfrowane jest samo hasło.
6. Skupia się bardziej ja uwierzytelnianiu i dostępie do usług, a nie do pojedynczych komend. Mniej granularny.
7. Mocno rozwinięty accounting

**Najważniejsze atrybuty:**
- **Autentykacja i autoryzacja są wykonywane w "jednym kroku" (!!!)**
- Szyfruje SAMO hasło
- Wykorzystuje UDP
- Wspiera technologie dostępu zdalnego, takie jak SIP

#### Konfiguracja autentykacji RADIUS
1. **Włącz AAA globalnie** - bez tego żadna operacja na AAA się nie powiedzie
   >`R1(config)#` **`aaa new-model`**
2. **Określ jaki serwer będzie używany do AAA** - RADIUS
   >`R1(config)#` **`radius server`** *`server-name`*
   >
   >Ta komenda tworzy ten serwer "lokalnie", ale żeby ta nazwa coś znaczyła, należy też wybrać adres IP. Nazwa to w sumie alias. Można też określić port do autentykacji i accountingu przy przy pomocy tej komendy, gdzie jest to silnie zalecane ponieważ Ciscowe routery używają innych portów do autentykacji niż RADIUS
   >
   >`R1(config-radius-server)#` **`address ipv4`** *`ip-address`* **`auth-port`** *`auth-port-num`* **`acct-port`** *`acct-port-num`*
1. **Skonfiguruj klucz szyfrowania**, służący do utajnienia ruchu między routerem a serwerem
   >`R1(config-radius-server)#` **`key`** *`server-password`*
   >
   >Klucz musi być dokładnie taki sam na serwerze i na urządzeniu.
2. **W konfiguracji AAA do listy serwerów** dodaj swoje serwery TACACS+
   >Odwołaj się do [[Metody autentykacji AAA|metod autentykacji]]
   >
   >`R1(config)# aaa authentication login default group radius local-case`
   >
   >Do autentykacji będą służyły wszystkie serwery RADIUS wcześniej zdefiniowane.