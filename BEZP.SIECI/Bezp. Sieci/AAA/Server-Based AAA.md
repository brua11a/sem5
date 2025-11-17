Podczas uwierzytelniania, router odwołuje się do centralnego serwera (lub serwerów) AAA zamiast porównywać credentiali z lokalną bazą danych. Do komunikacji z serwerem wykorzystywane są protokoły **[[RADIUS]]** (*Remote Authentication Dial-In User Service*) oraz **[[TACACS+]]** (*Terminal Access Controller Access Control System*). 

Jest to zdecydowanie lepsze rozwiązanie w większych sieciach.

**Authentication:** Użytkownik prosi o dostęp do urządzenia, urządzenie pyta o credentiale, użytkownik je wysyła, urządzenie przekazuje credentiale do serwera AAA, na podstawie odpowiedzi serwera AAA urządzenie przyznaje dostęp lub go odmawia.

**Authorization:** Po nawiązaniu sesji, serwer AAA jest ponownie odpytywany gdy użytkownik próbuje uzyskać dostęp do konkretnego serwisu. Serwer AAA zwraca przyzwolenie lub odmowę.

**Accounting:** Informacje o wykorzystanych zasobach są zbierane przez serwer AAA. Mogą one potem zostać eksportowane do raportów. W logach jest zapisane wszystko, co użytkownik zrobił, wraz z odpowiednimi timestampami etc.

#### Autentykacja Server-Based AAA
1. **Włącz AAA globalnie** - bez tego żadna operacja na AAA się nie powiedzie
   >`R1(config)#` **`aaa new-model`**
2. **Określ jaki serwer będzie używany do AAA** - RADIUS i/lub TACACS+
   >`R1(config)#` **`tacacs/radius server`** *`server-name`*
   >
   >Przypisz także adres IP w jakiś sposób
3. **Skonfiguruj klucz szyfrowania**, służący do utajnienia ruchu między routerem a serwerem
   >`R1(config-server-tacacs)#` **`key`** *`server-password`*
4. **W konfiguracji AAA do listy serwerów** dodaj swoje serwery RADIUS i/lub TACACS+
   >Odwołaj się do [[Metody autentykacji AAA|metod autentykacji]]
   >
   >`R1(config)# aaa authentication login default group tacacs+ group radius local-case`
   >
   >Tutaj najpierw sprawdzane będą wszystkie TACACS+, potem wszystkie RADIUS i dopiero na końcu lokalna baza danych.
   
#### Autoryzacja Server-Based AAA
```
R1(config)# username JR-ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# username ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# aaa new-model
R1(config)# aaa authorization exec default group tacacs+
R1(config)# aaa authorization network default group tacacs+
```

Jako zautentykowanych użytkowników zostaną uznani wszyscy, którzy zostali zdefiniowani na serwerze TACACS+ - będą oni mieli dostęp do serwisów związanych z siecią i trybem exec, ale da się też przypisać komendy związane z konkretnym [[privilege level]].
#### Accounting Server-Based AAA
```
R1(config)# username JR-ADMIN algorithm-type scrypt secret Str0ng5rPa5w0rd
R1(config)# username ADMIN algorithm-type scrypt secret Str0ng5rPa55w0rd
R1(config)# aaa new-model
R1(config)# aaa authentication login default group tacacs+
R1(config)# aaa authorization exec default group tacacs+
R1(config)# aaa authorization network default group tacacs+
R1(config)# aaa accounting exec default start-stop group tacacs+
R1(config)# aaa accounting network default start-stop group tacacs+
```

Accounting będzie wykonywany dla sesji powłoki EXEC i dla wszystkich serwisów sieciowych takich jak PPP przez cały czas trwania procesu dla użytkowników zdefiniowanych na serwerze TACACS+. 