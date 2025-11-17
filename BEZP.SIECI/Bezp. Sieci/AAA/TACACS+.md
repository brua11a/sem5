Protokół uwierzytelniania stosowany do komunikacji z AAA. Spełnia podobną rolę, co [[RADIUS]], lecz są między nimi znaczące różnice:

1. Zgodnie z założeniami, TACACS+ każdy z serwisów zapewnia osobny serwis AAA, co pozwala np. używać go do tylko autentykacji i autoryzacji ale accounting robić czymś innym. Czyni go to bardziej modularnym.
2. Standard głównie używany przez Cisco.
3. Komunikacja po TCP.
4. Mechanizm uwierzytelnienia TACACS+ opiera się na obustronnym challenge-response, podobnie jak w CHAP.
5. Szyfrowany jest CAŁY pakiet.
6. Granularne uprawnienia - można autoryzować pojedyncze polecenia dla grup i użytkowników.
7. Ograniczony accounting.

**Najważniejsze atrybuty:**
- Rozdziela autentykację od autoryzacji
- Szyfruje CAŁĄ komunikację
- Wykorzystuje TCP, port 49

#### Konfiguracja autentykacji TACACS+
1. **Włącz AAA globalnie** - bez tego żadna operacja na AAA się nie powiedzie
   >`R1(config)#` **`aaa new-model`**
2. **Określ jaki serwer będzie używany do AAA** - TACACS+
   >`R1(config)#` **`tacacs server`** *`server-name`*
   >
   >Ten serwer tworzy ten serwer "lokalnie", ale żeby ta nazwa coś znaczyła, należy też wybrać adres IP. Nazwa to w sumie alias. Można też określić niedomyślny port do autentykacji i accountingu przy przy pomocy tej komendy.
   >
   >`R1(config-server-tacacs)#` **`address ipv4`** *`ip-address`*
   >
   >Dodatkowa komenda poprawia działanie TCP poprzez utrzymywanie pojedynczej sesji.
   >
   >`R1(config-server-tacacs)# single-connection`
3. **Skonfiguruj klucz szyfrowania**, służący do utajnienia ruchu między routerem a serwerem
   >`R1(config-server-tacacs)#` **`key`** *`server-password`*
   >
   >Klucz musi być dokładnie taki sam na serwerze i na urządzeniu.
4. **W konfiguracji AAA do listy serwerów** dodaj swoje serwery TACACS+
   >Odwołaj się do [[Metody autentykacji AAA|metod autentykacji]]
   >
   >`R1(config)# aaa authentication login default group tacacs+ local-case`
   >
   >Do autentykacji będą służyły wszystkie serwery TACACS+ wcześniej zdefiniowane.