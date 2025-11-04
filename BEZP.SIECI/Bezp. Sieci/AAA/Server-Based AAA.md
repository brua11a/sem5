Podczas uwierzytelniania, router odwołuje się do centralnego serwera AAA zamiast porównywać credentiali z lokalną bazą danych. Do komunikacji z serwerem wykorzystywane są protokoły **RADIUS** (*Remote Authentication Dial-In User Service*) oraz **TACACS+** (*Terminal Access Controller Access Control System*). 

Jest to zdecydowanie lepsze rozwiązanie w większych sieciach.

**Authentication:** Użytkownik prosi o dostęp do urządzenia, urządzenie pyta o credentiale, użytkownik je wysyła, urządzenie przekazuje credentiale do serwera AAA, na podstawie odpowiedzi serwera AAA urządzenie przyznaje dostęp lub go odmawia.

**Authorization:** Po nawiązaniu sesji, serwer AAA jest ponownie odpytywany gdy użytkownik próbuje uzyskać dostęp do konkretnego serwisu. Serwer AAA zwraca przyzwolenie lub odmowę.

**Accounting:** Informacje o wykorzystanych zasobach są zbierane przez serwer AAA. Mogą one potem zostać eksportowane do raportów. W logach jest zapisane wszystko, co użytkownik zrobił, wraz z odpowiednimi timestampami etc.