Jest to sposób na agregowanie [[Object|obiektów sieciowych]]. Grupowanie obiektów serwisowych jest możliwe, ale niezalecane. 

#### **Zasady:**
1. Wszystkie obiekty i object-groups są w tym samym _namespace_ (ASA nie rozróżnia ich po typach – tylko po nazwie).
2. Nazwy muszą być **unikatowe** - nie można mieć obiektu i object-group o tej samej nazwie.
3. Object-group nie może zostać usunięte, jeśli jest gdzieś wykorzystywane (np. w ACL, NAT, policy-map).
4. Nie są wspierane zagnieżdżone IPv6 object groups.
5. Object-group może zawierać:
    - wpisy _inline_ (np. `network-object 10.1.1.0 255.255.255.0`)
    - inne object-groups (tylko IPv4, `network-object object OBJECTNAME`)
6. Zmiany w object-group są dziedziczone automatycznie wszędzie tam, gdzie grupa jest użyta. Nie można usunąć grupy jeśli jest gdzieś wykorzystywana.
#### **Typy:**

1. **Network**
   > Hosty, podsieci, zakresy adresów, FQDN (jako osobne obiekty), inne network object-groups (IPv4)
2. **User**
   >Lokalne grupy użytkowników lub zaimportowane z Active Directory - wykorzystywane w tożsamościowym firewallingu (Identity Firewall).
3. **Service**
   >Grupuje protokoły TCP, UDP, ICMP, IP oraz zdefiniowane reguły portów.  
4. **ICMP-Type**
   >ICMP (v4/v6) definiuje **typy wiadomości kontrolnych**, np. `echo`, `echo-reply`, `time-exceeded`, `unreachable`.
5. **Security**
   >Cisco TrustSec (SGT), rozszerzone ACL, zasady dostępu oparte o tagi bezpieczeństwa.

### Konfiguracja (Network Object Group)
Zaczyna się od komendy:
>`NETSEC-ASA(config)#` **`object-group network`** *`name`*

Gdzie można wpisywać kolejne komendy, podobne do tych z normalnych grup. Konfiguracja może być inline - wpisywanie nowych obiektów:
> `network-object host+adres/podsieć`

Można też do grupy dodać istniejące już obiekty:
>`network-object object OBJECTNAME`



