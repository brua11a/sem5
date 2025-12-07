Modular Policy Framework służy do konfigurowania zestawu zasad dotyczących [[ASA Firewall|firewalla]]. Umożliwia granularną klasyfikację ruchu, dzięki czemu różne typy ruchu mogą mieć przypisane różne, zaawansowane polityki.

Workflow MPF jest podobny do tego [[ZPF]] - klasyfikacja -> przypisanie polityki -> wykonanie akcji. Zobacz: [[konfiguracja ZPF]]

Wykorzystywane są trzy typy obiektów:
1. **Class Maps**
   >`ASA(config)#` **`class map`** *`class-name`*
   >Służą do klasyfikacji ruchu. Zdarzenia spełniające zdefiniowane kryteria będą wywoływały wybraną akcję w polityce. Class Maps mogą zawierać wiele warunków dotyczących warstw 3 i 4.
2. **Policy Maps**
   >`ASA(config)#` **`policy map`** *`policy-name`*
   >Służą do definiowania **akcji oraz polityk** dla ruchu w warstwach 3-7. To tutaj określa się, co zrobić z ruchem, który trafił do danej klasy (np. `inspect`, `drop`, `police`).
3. **Service Policy**
   >`ASA(config)#` **`service-policy`** *`serv-name`* `[`**`global | interface`** *`if-name`* `]`
   >Służy do **aktywacji Policy Map** na odpowiednim poziomie - globalnie lub na konkretnym interface.

### Konfiguracja
1. *(Opcjonalnie)* Skonfiguruj extended [[ASA ACL]] do granularnego rozpoznawania ruchu.
   >```
   >NETSEC-ASA(config)# access-list UDP permit udp any any  
NETSEC-ASA(config)# access-list TCP permit tcp any any  
NETSEC-ASA(config)# access-list SERVER permit ip any host 10.1.1.1  
   >```
2. Skonfiguruj class map do rozpoznawania ruchu
   >```
   >NETSEC-ASA(config)# class-map ALL-TCP  
NETSEC-ASA(config-cmap)# description This class-map matches all TCP traffic  
NETSEC-ASA(config-cmap)# match access-list TCP  
NETSEC-ASA(config-cmap)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# class-map ALL-UDP  
NETSEC-ASA(config-cmap)# description This class-map matches all UDP traffic  
NETSEC-ASA(config-cmap)# match access-list UDP  
NETSEC-ASA(config-cmap)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# class-map ALL-HTTP  
NETSEC-ASA(config-cmap)# description This class-map matches all HTTP traffic  
NETSEC-ASA(config-cmap)# match port TCP eq http  
NETSEC-ASA(config-cmap)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# class-map TO-SERVER  
NETSEC-ASA(config-cmap)# description Class map matches traffic  10.1.1.1  
NETSEC-ASA(config-cmap)# match access-list SERVER  
NETSEC-ASA(config-cmap)# exit  
   >```
   >
   >Jak widać, do dopasowania (`match`) ruchu do `class-map` zastosowano `match access-list` *`acl-name`*, instnieje jeszcze `match any` oraz inline `match port TCP eq http`. Zazwyczaj jeden match statement odpowiada jednej mapie. 
1. Skonfiguruj policy map żeby przypisać akcje to tamtego ruchu (z class map)
   >```
   >NETSEC-ASA(config)# access-list TFTP-TRAFFIC permit udp any any eq 69  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# class-map CLASS-TFTP  
NETSEC-ASA(config-cmap)# match access-list TFTP-TRAFFIC  
NETSEC-ASA(config-cmap)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# policy-map POLICY-TFTP  
NETSEC-ASA(config-pmap)# class CLASS-TFTP  
NETSEC-ASA(config-pmap-c)# inspect tftp  
NETSEC-ASA(config-pmap-c)# exit  
NETSEC-ASA(config-pmap)# exit  
   >```
   >Do przypisania akcji do konkretnej class-map w obrębie polityki wykorzystywane jest `class` *`class-map-name`*. Będąc w trybie konfiguracji policy map można wykonać m.in.:
   >- `set connection` - modyfikacja parametrów połączeń dla ruchu tej klasy (timeouty, limity resetów itd.)
   >- `inspect` - application layer inspection dla danego protokołu, analiza protokołu, sanity-checking
   >- `police` - ogranicz (rate limit) ruch z tej klasy, zmniejsz przepustowość, ruch przekraczający limit -> coś z nim zrób
   >Akcje działają obustronnie
2. Skonfiguruj service policy aby "podpiąć" policy map to interface (lub globalnie)
   >```
   >NETSEC-ASA(config)# **service-policy POLICY-TFTP global**
   >```
   >Tutaj globalnie

