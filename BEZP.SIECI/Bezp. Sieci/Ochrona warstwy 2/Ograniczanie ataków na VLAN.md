---
tags:
  - Konfiguracja
---
1. Wyłącz negocjowanie DTP (Dynamic Trunking protocol)
2. Wyłącz nieużywane porty i umieść je w nieużywanym VLAN
3. Ustaw trunki na sztywno, bez negocjowania
4. Stwórz nowy VLAN natywny, nie domyślny VLAN 1, używaj go

```
S1(config)# interface range fa0/1 - 16
S1(config-if-range)# switchport mode access
S1(config-if-range)# exit
S1(config)#
S1(config)# interface range fa0/17 - 20
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 1000
S1(config-if-range)# shutdown
S1(config-if-range)# exit
S1(config)#
S1(config)# interface range fa0/21 - 24
S1(config-if-range)# switchport mode trunk
S1(config-if-range)# switchport nonegotiate
S1(config-if-range)# switchport trunk native vlan 999
S1(config-if-range)# end
S1#
```

