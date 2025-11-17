Do autentykacji jest wykorzystywana lokalna baza użytkowników. Trzeba ich manualnie [[Tworzenie użytkowników|stworzyć]]. Jest to OK dla malutkich sieci z małą ilością przewidywanych użytkowników. 

Lokalny AAA jest bardzo podobny do dostępu przy pomocy `login local`, ale dodatkowo pozwala na ustawienie zapasowej metody autentykacji bez hard resetu.

#### Konfiguracja lokalnego AAA
1. **Stwórz użytkowników**
   >`R1(config)#` **`username algorithm-type`** *`algorytm`* **`secret`** *`hasło`*
2. **Włącz AAA globalnie** - bez tego żadna operacja na AAA się nie powiedzie
   >`R1(config)#` **`aaa new-model`**
   >
   >Uwaga - domyślnie wtedy na wszystkich liniach vty odpalane jest logowanie lokalną bazą danych! A więc najpierw użytkownicy potem AAA.
1. **Skonfiguruj parametry AAA**
   >`Router(config)#` **`aaa authentication login`** **`{default | list-name}`** *`method1… [method4]`*
   
   
| Fragment komendy               | Wyjaśnienie                                                                                                                                                                                                                                                                                       |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`aaa authentication login`** | Określ w jaki sposób użytkownicy autentykują się podczas logowania do urządzenia                                                                                                                                                                                                                  |
| **`default`**                  | [[Metody autentykacji AAA]] wylistowane później są traktowane jako domyślna lista metod wykorzystywanych do autentykacji, gdy użytkownik się loguje                                                                                                                                               |
| *`list-name`*                  | Pozwala stworzyć nazwaną listę metod uwierzytelniania. Żeby zaaplikować tą listę do linii, należy być explicit i użyć `login authentication`*`list-name`*                                                                                                                                         |
| *`method1… [method4]`*         | Lista 1-4 [[Metody autentykacji AAA\|metod]] stosowanych przez AAA podczas uwierzytelniania w tej kolejności. Jeśli pierwsza metoda jest niedostępna, próbowana jest druga, potem trzecia itd. Jeśli jednak ktoś nie uwierzytelni się poprawnie w pierwszej metodzie to nie są próbowane kolejne. |

**W kontekście Local AAA obchodzą nas metody:**
- `enable`
- `local`
  > Jako jedyny ma dedykowaną metodę do ustawiania maksymalnej ilości nieudanych prób autentykacji: `Router(config)# aaa local authentication attempts max-fail [number]`, gdzie zablokowany użytkownik będzie musiał być manualnie odblokowany (`R1# show aaa local user lockout`, `clear aaa local user lockout`), a nie po prostu [[Dodatkowe ustawienia haseł i dostępu|zablokowany na jakiś czas]].
- `local-case`

#### Przykład

```
R1(config)# username JR-ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# username ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# aaa new-model
R1(config)# aaa authentication login default local-case enable
R1(config)# aaa authentication login SSH-LOGIN local-case
R1(config)# line vty 0 4
R1(config-line)# login authentication SSH-LOGIN
```

Stworzeni zostali użytkownicy JR-ADMIN i ADMIN, na wszystkich liniach domyślnie logowanie wykonywane jest poprzez `local-case` z fallbackiem na `enable`, ale na liniach `vty 0 4` jasno jest określone, że listą metod będzie SSH-LOGIN, w którym jest tylko `local-case` - logowanie przez lokalną bazę danych albo zakaz wstępu, bez fallbacku.