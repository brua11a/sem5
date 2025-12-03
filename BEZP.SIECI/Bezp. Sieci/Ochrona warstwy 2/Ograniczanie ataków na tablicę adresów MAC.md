---
tags:
  - Konfiguracja
---
[[Ataki na tablicę adresów MAC]] ograniczamy [[Zabezpieczanie portów|zabezpieczeniami portów]], konkretniej komendami z rodziny `switchport port-security`. Pozwalają one przełącznikowi na zapamiętanie i/lub nauczenie się ograniczonej ilości adresów, tym samym odrzucając te nieznajdujące się na liście bezpiecznych.

## Przede wszystkim żeby `port-security` działał to trzeba go włączyć. Kolejne komendy nie zadziałają jeśli się tego nie wpisze. 

```
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security
S1(config-if)# end
S1#
```

Po wpisaniu tej komendy możemy modyfikować szczegóły zabezpieczeń

```
S1(config-if)# switchport port-security ?
  aging        Port-security aging commands
  mac-address  Secure mac address
  maximum      Max secure addresses
  violation    Security violation mode 
```

___
#### `aging`:

Komendy z rodziny `switchport port-security aging` pozwalają określić czas (`time`) i typ (`type`) przedawniania się adresów. 

Domyślnie przedawniają się tylko adresy dynamicznie uczone, `switchport port-security aging static` sprawia, że adresy statycznie ustawione też mogą się zestarzeć.

Czas potrzebny na przedawnienie można ustawić poprzez `switchport port-security aging time`*`time`*, gdzie zakres to od 0 do 1440 minut; 0 oznacza, że w porcie nic się nie przedawnia. Jest to opcja domyślna.

Są dwa typy przedawnienia: `absolute` i `inactivity`. `switchport port-security aging absolute` sprawia, że adres MAC zostanie przedawniony po określonym czasie i zniknie z listy bezpiecznych adresów. `switchport port-security aging inactivity` sprawia, że adres MAC zostanie przedawniony po określonym czasie nieaktywności.

```
S1(config)# interface fa0/1
S1(config-if)# switchport port-security aging time 10
S1(config-if)# switchport port-security aging type inactivity
S1(config-if)# end
S1# show port-security interface fa0/1
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 10 mins
Aging Type                 : Inactivity
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 2
Total MAC Addresses        : 2
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 1
Last Source Address:Vlan   : a41f.7272.676a:1
Security Violation Count   : 0
```

___
#### `mac-address`:

Ciąg `switchport port-security mac-address`*`mac-address`* pozwala ręcznie dodać adres MAC do tabeli bezpiecznych.

Po samym wpisaniu `switchport port-security` urządzenie podłączone do portu jest automatycznie uznawane za bezpieczne do resetu przełącznika.

Żeby nauczyć się tego podłączonego urządzenia na "stałe" trzeba wydać polecenie `switchport port-security sticky`. Dynamicznie poznane urządzenie będzie na stałe zapisane w konfiguracji w pamięci NVRAM jako bezpieczne.

```
S1(config-if)# switchport port-security mac-address aaaa.bbbb.1234
S1(config-if)# switchport port-security mac-address sticky
S1(config-if)# end
S1# show port-security address
               Secure Mac Address Table
-----------------------------------------------------------------------------
Vlan    Mac Address       Type                          Ports   Remaining Age
                                                                   (mins)    
----    -----------       ----                          -----   -------------
1    a41f.7272.676a    SecureSticky                  Fa0/1        -
1    aaaa.bbbb.1234    SecureConfigured              Fa0/1        -
-----------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 1
Max  Addresses limit in System (excluding one mac per port) : 8192
```

___
#### `maximum`:

Komenda `switchport port-security maximum`*`value`* określa maksymalną ilość adresów MAC dozwolonych na porcie. Domyślnie 1, można do 8192. 

___
#### `violation`:

Polecenia zaczynające się od `switchport port-security violation` określają co ma się stać jeśli podepnie się adres MAC poza tym z listy bezpiecznych.  Mamy do wyboru:
1. **`shutdown`** (domyślny)
   >Port przechodzi w stan error-disabled, wyłącza kontrolkę LED portu, wysyła wiadomość [[syslog]], zwiększa licznik naruszeń. Wymaga ponownego wyłączenia i włączenia przez administratora.
2. **`restrict`**
   >Port odrzuca pakiety z nieznanego źródła aż zostanie uznane ono za bezpieczne. Rośnie licznik naruszeń, pojawia się wiadomość syslog.
3. **`protect`**
   >Tylko odrzuca nieznane pakiety, nie generuje wiadomości syslog.


___
Polecenie `show port-security interface`*`interface`* pokazuje stan zabezpieczeń interfejsu.
Samo `show port-security` pokaże ustawienia zabezpieczeń na wszystkich portach. 


### `S1(config)# mac address-table notification`
Instnieje dodatkowo możliwość wysyłania [[Pułapki agentów SNMP|SNMP Traps]] gdy adres MAC uznany za bezpieczny znika z przypisanego mu portu. Wiadomość może być też wysyłana za każdym razem gdy nowy MAC zostanie dodany lub stary usunięty z forwarding table. 