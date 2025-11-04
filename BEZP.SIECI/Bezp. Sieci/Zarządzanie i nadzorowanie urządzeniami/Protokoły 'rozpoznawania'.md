Chodzi tu o **CDP** (*Cisco Discovery Protocol*) oraz **LLDP** (*Link Layer Discovery Protocol*) - pozwalają one zobaczyć sąsiednie urządzenia, które również korzystają z tych protokołów. Konfiguruje się je bardzo podobnie, tylko CDP jest włączony domyślnie a LLDP nie.

LLDP można włączyć poprzez:
> `R1(config)#` **`lldp run`**

A gdy protokół już działa to można zobaczyć informacje o sąsiadach poprzez:
> `R1#` **`show`** *`cdp/lldp`* **`neighbors detail`**

LLDP może zwrócić na przykład takie informacje:
```
Local Intf: Gi0/1
Chassis id: 0022.9121.0380
Port id: Fa0/5
Port Description: FastEthernet0/5
System Name: S1
 
System Description:  
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE7,
RELEASE SOFTWARE (fc1)
<output omitted>
```

Teoretycznie te protokoły są zagrożeniem, ponieważ pomagają atakującym na rekonesans sieci, zatem powinno się je wyłączyć. W praktyce jednak atakujący nie potrzebują CDP i LLDP, żeby zdobyć te informacje.

Wiele innych protokołów jest jedynie domyślnie włączonych z powodów historycznych, zatem należy je wyłączyć jeśli nie są wykorzystywane, czasem też należy wyłączyć serwis tylko na konkretnych interfejsach, np. tych przylegających do niezaufanych sieci.