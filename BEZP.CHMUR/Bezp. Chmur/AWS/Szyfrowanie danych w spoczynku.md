Dzięki niemu informacje w naszych zasobach nie są widoczne dla atakującego nawet jeśli uzyska do nich dostęp w nieoczekiwany sposób. Często jest to wymóg stawiany przez firmy.

Dane w spoczynku należy też chronić (i/lub ograniczać do nich dostęp) w scenariuszach takich jak:
1. **Information disclosure (ujawnienie informacji)**
   >Ogranicz liczbę użytkowników, którzy mają dostęp do danych i użyj [[Policy|polityk]] żeby zarządzać dostępem do zasobów. Użyj szyfrowania, by chronić informacji poufnych
2. **Data integrity compromise (naruszenie integralności danych)**
   >Użyj uprawnień aby ograniczyć ilość użytkowników mogących modyfikować dane wraz z podpisami cyfrowymi i szyfrowaniem. Korzystaj z backupów i wersjonowania.
3. **Accidental or malicious deletion (przypadkowe lub złośliwe usunięcie)**
   >Principle of least privilege. Korzystaj z backupów i wersjonowania.
4. **System, hardware, and software availability (dostępność systemu, sprzętu i oprogramowania)**
   >W krytycznych sytuacjach odnów dane z replik.
   
Na przykład zasoby w instancjach [[Ochrona S3|S3]] są domyślnie prywatne i jedynie właściciel zasobów ma do nich dostęp. Dodatkowo można je zaszyfrować. Dostęp do zasobów określany jest przy pomocy [[IAM]]. Jeszcze możliwe, ale raczej niepotrzebne jest skonfigurowanie ACL.

