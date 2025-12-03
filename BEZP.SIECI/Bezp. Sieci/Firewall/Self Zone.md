
| Czy src. int. jest w *Zone*? | Czy dst. int. jest w *Zone*? | *zone-pair*? | *class-map*? | Rezultat |
| ---------------------------- | ---------------------------- | ------------ | ------------ | -------- |
| Tak, Self Zone               | Tak, jakimkolwiek            | Nie          | N/A          | PASS     |
| Tak, Self Zone               | Tak, jakimkolwiek            | Tak          | Nie          | PASS     |
| Tak, Self Zone               | Tak, jakimkolwiek            | Tak          | Tak          | INSPECT  |
| Tak, jakimkolwiek            | Tak, Self Zone               | Nie          | N/A          | PASS     |
| Tak, jakimkolwiek            | Tak, Self Zone               | Tak          | Nie          | PASS     |
| Tak, jakimkolwiek            | Tak, Self Zone               | Tak          | Tak          | INSPECT  |

**Self Zone** to specjalna strefa w [[ZPF]], która reprezentuje sam router - czyli wszystkie interfejsy logiczne i adresy IP przypisane bezpośrednio do urządzenia. Obejmuje to m.in.:
- adresy interfejsów fizycznych i VLAN,
- adresy loopback,
- wirtualne interfejsy (np. tunnel).

Największa różnica jest taka, że dla self zone dozwolony jest ruch nawet jak nie ma [[zone pair]].

Zazwyczaj ruch skierowany do self zone to management taki jak SSH lub routing - management i forwarding plane.

