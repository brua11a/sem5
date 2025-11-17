Kontroluje dostęp do zasobów w AWS - kto jest zautoryzowany do dostepu do nich ([[Użytkownik|użytkownicy i aplikacje]], [[Grupa|grupy]], [[Rola|role]]). Działa on z większością serwisów oferowanych przez AWS, a także wspiera MFA.

Są właściwie dwie filozofie przy weryfikowaniu podmiotu przy pomocy IAM:
- *authentykacyjna* - kto może wykorzystywać moje zasoby
- *autoryzacyjna* - jakie zasoby może ktoś wykorzystać i w jaki sposób

IAM polega na [[Policy|politykach]] przypisywanych do [[Grupa|grup]] i podmiotów.

![[Pasted image 20251111233426.png]]

Z założenia, uprawnienia IAM działają tak, że wymagana jest explicit zgoda, żeby uzyskać do czegokolwiek dostęp. Nawet jeśli ona istnieje, to explicit odmowa ją nadpisuje.

Nic -> deny
**Pozwolenie -> allow**
Odmowa -> deny
Pozwolenie + odmowa -> deny

