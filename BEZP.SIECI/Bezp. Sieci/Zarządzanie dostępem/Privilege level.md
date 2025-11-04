Domyślnie jest tylko 1 (user mode) i 15 (privileged EXEC mode). Gdy wpisuję w konsolę po prostu `enable`, domyślnie loguje mnie na poziom 15.

#### Ogólnie poziomów jest 16
1. **Level 0**
   > Rzadko używany, tylko komendy `disable, enable, exit, help, logout`
2. **Level 1**
   >Domyślny user mode, ląduje się w nim po normalnym odpaleniu routera bez żadnych dodatkowych komend. Z tego poziomu nie można czytać ani modyfikować konfiguracji. Znak zachęty to `>`
3. **Level 2-14 (CUSTOM)**
   >Customowe, można tu przypisać te komendy, które się chce.
4. **Level 15**
   >Ponownie, domyślny privileged EXEC. Pozwala na czytanie i edytowanie konfiguracji. Znak zachęty to `#`
   
##### Żeby przypisać komendy do customowego poziomu, należy użyć komendy:
> `Router(config)#` **`privilege`** *`mode`* `{` **`level`** *`level`*`|`**`reset`**`}` *`command`*

| Fragment komendy        | Opis                                                                                           |
| ----------------------- | ---------------------------------------------------------------------------------------------- |
| *`mode`*                | Tryb konfiguracji, jest tego dużo zatem po napisaniu **`privilege ?`** wyświetli się wszystko. |
| **`level`** + *`level`* | Komenda będzie dotyczyła privilege level określonego w tym miejscu                             |
| **`reset`**             | Resetuje privilege level komendy                                                               |
| *`command`*             | Komenda, której dotyczą zmiany                                                                 |
`R1(config)# privilege exec level 5 ping`
Wszystkie komendy z level 1 + ping

`R1(config)# privilege exec level 10 reload`
Wszystkie komendy z level 5 + reload

Można zalogować się do użytkownika o konkretny privilege level albo po prostu "bezpośrednio" do privilege level.
##### Ustawianie uprawnień
1. **Do użykownika**
   >`R1(config)#` **`username`** *`name`* **`privilege`** *`level`* **`algorithm-type scrypt secret`** *`haslo`*
2. **Do "poziomu"**
   > `R1(config)#` **`enable algorithm-type scrypt secret level`** *`level password`*
   
##### Logowanie
1. **Do użytkownika**
   > Zwykłe logowanie przy uruchomieniu urządzenia
2. **Do "poziomu"**
   >`R1>` **`enable`** *`level`* zamiast po prostu `enable` (które de facto jest aliasem dla `enable 15`)
   
**Poziom swoich uprawnień po zalogowaniu można sprawdzić poleceniem:**
> `R1#` **`show privilege`**

Chociaż ustawianie privilege level może być użyteczne, to ma poważne ograniczenia - chociażby to, że użytkownik wyższego levela dziedziczy wszystkie uprawnienia użytkowników "niżej". Z tego powodu używa się raczej [[Role-Based CLI|role]].

