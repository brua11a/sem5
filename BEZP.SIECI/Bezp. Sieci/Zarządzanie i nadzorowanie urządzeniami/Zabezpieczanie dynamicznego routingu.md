Protokoły routingu dynamicznego, takie jak OSPF, są wygodne w użyciu i powszechnie stosowane. Sąsiednie urządzenia wymieniają się informacjami o urządzeniach, do których znają trasę i "podają dalej" te informacje, aż sieć stanie się zbieżna.

Problem jest w tym, że domyślnie każdy może "dołączyć" do tej wymiany i podać fałszywe informacje, tym samym przekierowując ruch w niepożądany sposób. Stąd pojawiła się potrzeba powstania mechanizmu autentykacji informacji o routingu.

W przypadku OSPF istnieje wbudowany protokół uwierzytelniania z użyciem MD5, który może zostać włączony globalnie albo tylko na konkretnych interfejsach. Jest on jednak przestarzały, zatem zaleca się przynajmniej SHA.

### Zabezpieczenie OSPF poprzez MD5
##### Globalnie
Wymusza konfigurację autentykacji OSPF na wszystkich włączonych interfejsach. Jeśli interfejs nie ma ustawionego klucza, nie będzie w stanie ustalać sąsiedztwa.
1. `R1(config-if)#` **`ip ospf message-digest-key`** *`key`* **`md5`** *`password`*
2.  `R1(config)#` **`area`** *`area-id`* **`authentication message-digest`**
##### Na interface
Nadpisuje globalny setting. Hasła nie muszą być te same w całym *area*, ale muszą być TE SAME MIĘDZY SĄSIADAMI próbującymi przylegać do siebie.
1. `R1(config-if)#` **`ip ospf message-digest-key`** *`key`* **`md5`** *`password`*
2. `R1(config-if)#` **`ip ospf authentication message-digest`**

### Zabezpieczanie OSPF poprzez SHA
##### Keychain
1. `Router(config)#` **`key chain`** *`name`* - tworzy keychain o tej nazwie i wchodzi w jego konfigurację
2. `Router(config-keychain)#` **`key`** *`key-id`* - nadaje numer keychainowi, konieczny krok
3. `Router(config-keychain-key)#` **`key-string`** *`password`* - zahasłowuje keychain
4. `Router(config-keychain-key)#` **`cryptographic-algorithm`** *`{hmac-sha-1 | hmac-sha-256 | hmac-sha-384 | hmac-sha-512 | md5}`* - pozwala wybrać oczekiwany algorytm hashowania
5. *Opcjonalne*: `Router(config-keychain-key)#` **`send-lifetime start-time`** *`{infinite | end-time | duration seconds}`* - ustawia czas życia klucza
##### Przypisz keychain do interfejsu
`Router(config-if)#` **`ip ospf authentication key-chain`** *`name`*
Wcześniej stworzony, nazwany keychain zostaje przypisany do interfejsu. Żeby uwierzytelnianie działało, obydwa routery muszą mieć ten sam keychain na sąsiednich interfejsach.