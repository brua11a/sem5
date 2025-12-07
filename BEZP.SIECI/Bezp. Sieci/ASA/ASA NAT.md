Na ASA działa NAT. Są trzy metody:
1. **Inside NAT**
   >Najczęstszy, zazwyczaj ruch z sieci prywatnej (o wyższym [[ASA security level]]) jest tłumaczony - prywatne adresy IP są tłumaczone na publiczne. 
2. **Outside NAT**
   >Gdy ruch z zewnatrz (mniejsze bezpieczeństwo) jest tłumaczony, żeby mógł dotrzeć do wewnętrznego hosta. 
3. **Bidirectional NAT**
   >Inside i Outside NAT są używane jednocześnie
   
Wspierany jest **dynamiczny PAT** (wiele inside addresses -> mniej outside addresses:port), **statyczny NAT**, **policy NAT** (bazujacy na zestawei zasad, np. tylko konkretne adresy źródłowe mogą korzystać z NAT) oraz **identity NAT** (prawdziwy adres jest statycznie tłumaczony do samego siebie, przydatne do omijania NAT).

### Konfiguracja dynamicznego NAT
Potrzebne są trzy komponenty:
1. Network [[Object]] określający pulę adresów jako `range` lub `subnet`. Te adresy będą tymi "przetłumaczonymi"
2. Drugi Network Object, który określa pulę adresów "tłumaczonych" jako `range` lub `subnet`
3. Powiązanie dwóch obiektów "w drugim obiekcie" poprzez komendę:
   > **`nat`** *`(in_iface,out_iface)`* **`dynamic`** *`mapped_obj_out`*

![[Pasted image 20251206174723.png]]

```
NETSEC-ASA(config)# object network PUBLIC  
NETSEC-ASA(config-network-object)# range 209.165.200.240 209.165.200.248  
NETSEC-ASA(config-network-object)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# object network DYNAMIC-NAT  
NETSEC-ASA(config-network-object)# subnet 192.168.1.0 255.255.255.224  
NETSEC-ASA(config-network-object)# nat (INSIDE,OUTSIDE) dynamic PUBLIC  
NETSEC-ASA(config-network-object)# end  
NETSEC-ASA#
```

Żeby pingi wracały, należy dodatkowo:
```
NETSEC-ASA(config)# policy-map global_policy  
NETSEC-ASA(config-pmap)# class inspection_default  
NETSEC-ASA(config-pmap-c)# access-list ICMPACL extended permit icmp any any  
NETSEC-ASA(config)# access-group ICMPACL in interface OUTSIDE  
NETSEC-ASA(config)#
```

### Konfiguracja PAT
Potrzebne są dwa komponenty:
1. Określ Network Object definiujący listę adresów do przetłumaczenia
2. **`nat`** *`(in_iface,out_iface)`* **`dynamic interface`**

Nie ma tutaj obiektu sieciowego definiującego dynamiczne zewnętrzne adresy, zamiast tego używany jest adres zewnętrzny interface ASA z overloadowanymi portami.

### Konfiguracja statycznego NAT
Dwa kroki:
1. Zdefiniuj Network Object określający hosta
2. **`nat`** *`(in_iface,out_iface)`* **`static`** *`translated_ip_addr`*

```
NETSEC-ASA(config)# object network DMZ-SERVER  
NETSEC-ASA(config-network-object)# host 192.168.2.3  
NETSEC-ASA(config-network-object)# nat (DMZ,OUTSIDE) static 209.165.200.227  
NETSEC-ASA(config-network-object)# exit  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# access-list OUTSIDE-DMZ extended permit ip any host 192.168.2.3  
NETSEC-ASA(config)# access-group OUTSIDE-DMZ in interface OUTSIDE  
NETSEC-ASA(config)#    
NETSEC-ASA(config)# policy-map global_policy  
NETSEC-ASA(config-pmap)# class inspection_default  
NETSEC-ASA(config-pmap-c)# access-list ICMPACL extended permit icmp any any  
NETSEC-ASA(config)# access-group ICMPACL in interface DMZ  
NETSEC-ASA(config)#
```
### Weryfikacja
```
NETSEC-ASA(config)# show xlate  
1 in use, 1 most used    
Flags: D - DNS, e - extended, I - identity, I - dynamic, r - portmap,    
       s - static, T - twice, N - net-to-net    
    
NAT from INSIDE:192.168.1.3 to OUTSIDE:209.165.200.242 flags I idle 0:00:02 timeout 3:00:00    
NETSEC-ASA(config)#   
 
NETSEC-ASA(config)# show nat  
  
Auto NAT Policies (Section 2)    
1 (INSIDE) to (OUTSIDE) source dynamic DYNAMIC-NAT PUBLIC      
    translate_hits = 1, ntranslated_hits = 1    
NETSEC-ASA(config)#    

NETSEC-ASA(config)# show nat detail  
  
Auto NAT Policies (Section 2)    
1 (INSIDE) to (OUTSIDE) source dynamic DYNAMIC-NAT PUBLIC      
    translate_hits = 1, ntranslated_hits = 1    
    Source - Origin: 192.168.1.0/27, Translated: 209.165.200.240-209.165.200.248    
NETSEC-ASA(config)#
```