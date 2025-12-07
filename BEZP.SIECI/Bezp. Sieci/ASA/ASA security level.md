Jest on stosowany aby rozróżnić sieci wewnętrzne od zewnętrznych. Im wyższy security level tym bardziej zaufany jest interface (0-100). Każdy interface musi też mieć nazwę zwyczajową. 

Ruch od sieci z niskim security level do sieci z wysokim security level jest traktowany jako inbound - ruch z zewnątrz, potencjalnie niebezpieczny. W drugą stronę - ruch z wysokiego do niskiego security to outbound, raczej bezpieczny.

![[Pasted image 20251204162023.png]]

Security level to liczba od 0 do 100, która określa poziom zaufania do danego interfejsu.
Typowo: inside = 100, dmz ≈ 50, outside = 0.
Wiele interfejsów może mieć ten sam security level, jeśli administrator tak ustawi (`same-security-traffic permit inter-interface`).

Ruch z wyższego security level do niższego jest automatycznie dozwolony.
Ruch z niższego do wyższego jest domyślnie blokowany, chyba że skonfigurujemy ACL lub reguły NAT.
Ruch pomiędzy interfejsami o tym samym poziomie jest domyślnie blokowany, ale można to zmienić (`same-security-traffic permit inter-interface`).

ASA śledzi połączenia wychodzące z wyższego do niższego poziomu (state table).
Dzięki temu ruch powrotny jest automatycznie przepuszczany bez dodatkowych reguł.

Inspekcja zaawansowana (np. FTP inspection, ESMTP inspection, HTTPS filtering) dotyczy połączeń outbound, czyli z wyższego security level do niższego.
Połączenia przychodzące (low → high) zawsze wymagają ACL, niezależnie od inspekcji.