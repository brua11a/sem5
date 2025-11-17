**Amazon Key Management Service** służy do przechowywania i centralnego zarządzania kluczami używanymi w szyfrowaniu informacji. Działa zarówno dla szyfrowania client-side jak i server-side. 

Pozwala na tworzenie aliasów dla kluczy, automatyczną ich rotację, a także wyłączanie lub usuwanie tych niepotrzebnych. Wykorzystuje **HSMs** (Hardware Security Modules) do ochrony kluczy.

KMS działa dobrze z [[CloudTrail]] - pozwala to na logowanie kto i kiedy użył klucza.

---

Gdy jest wykorzystywane szyfrowanie po stronie klienta (**CSE**), aplikacje szyfrują dane zanim zostaną one wysłane do AWS i są one też przechowywane w tym zaszyfrowanym stanie. Klucze są znane tylko klientowi.

![[Pasted image 20251113104118.png]]

Szyfrowanie po stronie serwera (**SSE**) jest wykonywane przez AWS i transparentne dla klienta. Wysyłane są dane, a AWS zajmuje się resztą.

![[Pasted image 20251113104130.png]]

#### Warianty SSE
1. **SEE-C (Customer Provided Keys)**
   >Klient zarządza kluczami i przechowuje je, a sam Amazon ich nie ma - jedynie wykorzystuje je przy szyfrowaniu i rozszyfrowywaniu.
2. **SSE-S3 (Amazon S3 Managed Keys)**
   >Każdy obiekt jest szyfrowany unikalnym kluczem. Dodatkowo, same klucze też są szyfrowane przy pomocy rotującego klucza.
3. **SSE-KMS (AWS KMS Keys)**
   > Podobne do SSE-S3, ale dodatkowo zapewnia osobne permisje wykorzystywania kluczy KMS. Wspiera także audyt, który odnotowuje kto i kiedy użył kluczy. Wykorzystywane jest tzw. *envelope encryption* - plaintext jest szyfrowany kluczem danych, a klucz danych jest szyfrowany kluczem roota. 
   
## SSE-KMS
![[Pasted image 20251114003518.png]]
![[Pasted image 20251114003527.png]]