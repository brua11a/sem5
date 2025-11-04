**SNMP** (*Simple Network Management Protocol*), jak nazwa wskazuje, służy do wygodnego i prostego zarządzania siecią - węzłami, serwerami, stacjami roboczymi, routerami, przełącznikami, zabezpieczenia... Pozwala też na monitorowanie wydajności sieci, szukanie i rozwiązywanie problemów, łatwiejszy rozwój.

##### System SNMP składa się z:
1. **Menedżera SNMP**
   >Na nim uruchamia się oprogramowanie do zarządzania SNMP. Pobiera informacje od agentów za pomocą akcji "**get**" i zmienia jego konfigurację poprzez "**set**". [[Żądania SNMP|Żądania]] opisane są dokładniej tutaj.
2. **Agentów SNMP**
   >Ich zadaniem jest zbieranie i przechowywanie informacji o urządzeniach w bazie MIB. Mogą przekazywać informacje do menedżera za pomocą "pułapek" ([[Pułapki agentów SNMP|traps]]). Znajdują się na urządzeniach klienckich - to, co chcemy zarządzać SNMP musi mieć specjalne oprogramowanie.
3. **Bazy danych zarządzania** ([[MIB]] - *Management Information Base*)
   >Przechowuje dane o urządzeniu i statystyki operacyjne. Dostępne dla uwierzytelnionych użytkowników zdalnych.  MIB musi znajdować się na każdym urządzeniu klienckim.

![[Pasted image 20250518113828.png]]

##### SNMP ma 3 główne wersje:
1. **SNMPv1** - prosta, pierwsza implementacja. Korzysta z [[Zabezpieczenia społecznościowe|zabezpieczeń społecznościowych]].
2. **SNMPv2c** - zawiera mechanizmy grupowego pobierania i szczegółowego raportowania komunikatów błędów, a także rozszerzoną obsługę błędów. Korzysta z [[Zabezpieczenia społecznościowe|zabezpieczeń społecznościowych]].
3. **SNMPv3** - wspiera autoryzację, szyfrowanie, integralność wewnętrzną, modele bezpieczeństwa. Do uwierzytelniania może służyć nazwa użytkownika (`NoAuthnopriv`) lub hash (`AuthNopriv`), a do szyfrowania DES, AES etc. (`authPriv`).