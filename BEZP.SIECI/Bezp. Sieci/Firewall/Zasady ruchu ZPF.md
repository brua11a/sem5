
| Czy src. int. jest w *Zone*? | Czy dst. int. jest w *Zone*? | *zone-pair*? | *class-map*? | Rezultat |
| ---------------------------- | ---------------------------- | ------------ | ------------ | -------- |
| Nie                          | Nie                          | N/A          | N/A          | PASS     |
| Tak                          | Nie                          | N/A          | N/A          | DROP     |
| Nie                          | Tak                          | N/A          | N/A          | DROP     |
| Tak, *Zone A*                | Tak, *Zone A*                | N/A          | N/A          | PASS     |
| Tak, *Zone A*                | Tak, *Zone B*                | Nie          | N/A          | DROP     |
| Tak, *Zone A*                | Tak, *Zone B*                | Tak          | Nie          | PASS     |
| Tak, *Zone A*                | Tak, *Zone B*                | Tak          | Tak          | INSPECT  |
Działanie [[ZPF]] zależy od tego, w jakich zone są źródłowe i docelowe urządzenia (jeśli w jakimś w ogóle są).

Jeśli żaden interfejs nie jest w żadnym zone, to ruch przechodzi.
Jeśli obydwa są w tym samym zone to też przechodzi.
Jeśli jeden jest w jakimkolwiek zone a drugi w żadnym to blokuje. Podobnie jeśli jeden jest w jednym zone a drugi w drugim, ale nie określono zasad ruchu pomiędzy nimi ([[zone pair]]).
Jeśli te zasady są określone, to można przepuścić albo dodatkowo zinspectować wg. policy.
