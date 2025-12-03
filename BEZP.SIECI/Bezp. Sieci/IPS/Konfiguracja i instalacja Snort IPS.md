Żeby mieć [[Snort IPS]] na swoim routerze:
1. Pobierz i zainstaluj plik OVA z wirtualnym serwisem
   >`R1# virtual-service install name MYIPS package dysk_lub_zdalna_lokacja:plik_ova.ova`
2. Skonfiguruj interfejsy VPG
   >Pierwszy VPG to management VPG - służy do m.in. pobierania update'ów sygnatur. Drugi służy do lokalnej wymiany ruchu z routerem.
   >```
   >R1# configure terminal
   >
   >Ri(config)# interface VirtualPortGroup0
   >R1(config-if)# description Management interface
   >R1(config-if)# ip address 209.165.201.1 255.255.255.252
   >Ri(config-if)# exit
   >
   >Ri(config)# interface VirtualPortGroup1
   >R1(config-if)# description Data interface
   >R1(config-if)# ip address 197.168.6.1 255.255.255.252
   >R1(config-if)# exit
   >```
1. Uruchom wirtualne serwisy
   >Definiowany jest wirtualny serwis, w którym stworzone są dwa wirtualne gateway, wirtualne karty sieciowe do wymiany ruchu, a także nadawany im jest adres. Ten sam serwis jest potem aktywowany.
   >```
   >R1(config)# virtual-service MYIPS
   >
   >R1(config-virt-serv)# vnic gateway VirtualPortGroup0
   >R1(config-virt-serv-vnic)# guest ip address 209.165.201.2
   >R1(config-virt-serv-vnic)# exit
   >
   >R1(config-virt-serv)# vnic gateway VirtualPortGroup1
   >R1(config-virt-serv-vnic)# guest ip address 192.168.0.2
   >R1(config-virt-serv-vnic)# exit
   >
   >R1(config-virt-serv)# activate
   >```
1. Skonfiguruj specyfikację Snort
   >Określ gdzie są wysyłane logi i w jaki sposób, czy ma działać jako IDS czy jako IPS, czy ma być bardziej "wygodny" czy "bezpieczny" czy zbalansowany, jak często mają być pobierane nowe sygnatury, dane logowania do serwera z update'ami, a także dla jakiego severity level [[syslog]] eventy mają być wysyłane.
   >```
   >R1(config)# utd engine standard
   >
   >R1(config-utd-eng-std)# logging host 10.16.10.254
   >R1(config-utd-eng-std)# logging syslog
   >
   >R1(config-utd-eng-std)# threat-inspection
   >R1(config-utd-engstd-insp)# threat protection
   >R1(config-utd-engstd-insp)# policy balanced
   >
   >R1(config-utd-engstd-insp)# signature update occur-at daily 6 @
   >R1(config-utd-engstd-insp)# signature update server cisco username Bob password class
   >R1(config-utd-engstd-insp)# logging level warning
   >```
1. Włącz [[IPS]] globalnie lub na pożądanych interfejsach
   >W przykładzie jest włączony globalnie - czyli wąchane będą wszystkie interfejsy sieciowe. Dodatkowo, zdefiniowane jest co ma zrobić Snort gdy się wywali - tutaj ma się po prostu zamknąć wraz z routerem, czyli jeśli Snort przestanie działać to nie zezwalamy na ruch w sieci.
   >```
   >R1(config)# utd
   >R1(config-utd)# all-interfaces
   >R1(config-utd)# engine standard
   >R1(config-engine-std)# fail close
   >```
   >Wspierana jest także whitelista - ignoruj sygnatury na podstawie ID.
   >```
   >R1(config)# utd threat-inspection whitelist
   >R1(config-utd-whitelist)# signature id 21555 comment traffic from Branch 1
   >```
2. Zweryfikuj - `show virtual service list/detail`