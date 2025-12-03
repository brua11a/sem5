Pierwszy sposób zabezpieczenia portu: wyłącz go, jeśli nie jest używany. Ogranicza to nieautoryzowany dostęp. 

```
S1(config)# interface range fa0/8 - 24
S1(config-if-range)# shutdown
%LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down
(output omitted)
%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down
S1(config-if-range)#
```

Dodatkowo, można wyłączone porty przekierować do nieużywanego VLANa.

Powinno się też ustawić banner ostrzegający potencjalnych intruzów.

Nie należy zapomnieć też o [[Kontrola dostępu|kontroli dostępu]].  

Na łączach trunk należy jednoznacznie zdefiniować dozwolone VLANy.

Dodatkowo, fizyczny dostęp do switcha powinien być ograniczony - za kłódką.

Na portach przełącznika należy włączyć [[BPDU Guard]] by nie wykrzaczyć sieci. 

Pozostałe sposoby zabezpieczania portu zaczynają się od polecenia `switchport port-security`. Mają one na celu [[Ataki na tablicę adresów MAC|ataków na tablicę adresów MAC]].
