Są to zestawy ustawień takich jak adresy IP. serwisy, nazwy itd. Obiektów można używać wielokrotnie. Pozwala na pewien stopień ograniczenia manualnego wprowadzania zmian. Jeśli zmodyfikowany zostanie obiekt (network object), to wszystkie serwisy itp. odwołujące się do niego automatycznie to zauważą bez potrzeby dodatkowej konfiguracji. 

Obiekty można agregować w [[Object Groups]], co pozwala połączyć kilka Network Objects. Jeden obiekt może należeć do kilku grup. 

### Network Object
Może zawierać hosta, adres IP, range adresów IP, nazwę domeny. Konfigurowany przy pomocy:
>`NetSec-ASA(config)#`**`object network`** *`name`*

Wpisanie tej komendy powoduje wejście w tryb konfiguracji obiektu sieciowego `(config-network-object)#`, gdzie można wydawać kolejne komendy:

| **Komenda**                                                            | **Opis**                                                                                                 | Przykład                          |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | --------------------------------- |
| **`attribute`** *`attribute-agent`* *`attribute-type attribute-value`* | Definiuje atrybuty obiektu; pozwala np. filtrować lub klasyfikować ruch związany z maszynami wirtualnymi | `attribute vm host 10.1.1.5`      |
| **`description`**                                                      | Dodaje opis obiektu (do 200 znaków), ułatwiający identyfikację w konfiguracji                            | `description Serwer aplikacji`    |
| **`fdqn`** *`name`*                                                    | Fully-qualified domain name – umożliwia powiązanie obiektu z nazwą FQDN, np. `www.example.com`           | `fdqn www.example.com`            |
| **`host`** *`ip-address`*                                              | Określa pojedynczy adres IP dla obiektu                                                                  | `host 192.168.10.5`               |
| **`range`** *`start_addr end_addr`*                                    | Definiuje ciągły zakres adresów IP (bez masek ani prefixów)                                              | `range 192.168.1.10 192.168.1.50` |
| **`subnet`** *`ip_addr netmask`*                                       | Przypisuje podsieć do obiektu, używając adresu i maski                                                   | `subnet 10.0.0.0 255.255.255.0`   |
**UWAGA:** w jednym obiekcie może być albo `fdqn`, albo `host`, albo `range` albo `subnet` - komendy nawzajem się wykluczają.
### Service Object
Określa protokół, ewentualnie port źródłowy i docelowy. Konfigurowany przy pomocy:
>`NetSec-ASA(config)#`**`object service`** *`name`*

Wpisanie tej komendy powoduje wejście w tryb konfiguracji obiektu serwisowego `(config-service-object)#`, gdzie można wydawać kolejne komendy:

| **Komenda**                                                                                                                | **Opis**                                                                                                                                                                                          | **Przykład**                     |
| -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| **`service`** _`protocol`_                                                                                                 | Definiuje protokół IP po nazwie lub numerze (np. `tcp`, `udp`, `icmp`, `ip`, `47`, `esp`)                                                                                                         | `service tcp`                    |
| **`service tcp/udp`** `[`**`source`** _`operator port`_`]` **`service tcp/udp`** `[`**`destination`** _`operator port`_`]` | Określa protokół TCP/UDP oraz opcjonalne warunki dotyczące portu źródłowego i/lub docelowego. `operator` działa jak w [[Numerowane rozszerzone listy ACL\|rozszerzonych ACL]] (`eq`, `gt`, itp.). | `service tcp destination eq 443` |
| **`service icmp/icmp6`** _`[icmp-type [icmp-code]]`_                                                                       | Definiuje ICMP lub ICMPv6. Można podać typ ICMP (np. `echo`, `echo-reply`, `time-exceeded`, `unreachable`) oraz opcjonalnie kod (np. `3` dla port unreachable)                                    | `service icmp echo`              |
UWAGA: w jednym obiekcie może być jeden protokół.