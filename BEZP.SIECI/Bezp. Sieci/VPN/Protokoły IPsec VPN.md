### AH (Authentication Header)
Zapewnia integralność i autentykację. Nagłówek **AH** tworzy się poprzez policzenie hasha z nagłówka IP, payloadu danych oraz wspólnego klucza symetrycznego. Ten nagłówek jest "wciskany" pomiędzy dane a nagłówek IP.
Całość jest wysyłana, a po drugiej stronie odbiorca na podstawie nagłówka IP (który otrzymał), danych (które otrzymał) i klucza (który wcześniej ustalił) liczy ten hash i są one porównywane.

![[Pasted image 20251203173959.png]]
### ESP (Encapsulation Security Protocol)

**ESP** zapewnia integralność, autentyczność oraz dodatkowo poufność danych - szyfrowanie.
1. **Szyfrowanie payloadu**  
   >Zawsze wykonywane jako pierwsze
2. **Generowanie HMAC**
   > Cały payload zostaje zhashowany i dołączony do wiadomości 
3. **Anti-Replay Protection** 
   >ESP może opcjonalnie chronić przed _atakami powtórzeniowymi (replay attacks)_.  
   >Każdy pakiet ma:
   >- **sequence number** – rosnący licznik pakietów,
   >- **sliding window** – bufor sprawdzający, które numery są jeszcze akceptowalne.

##### ESP – tryby pracy
ESP może działać w dwóch trybach:
- **Transport mode**  
  >Szyfrowany jest _tylko payload_, a nagłówek IP pozostaje niezmieniony. Stosowane głównie przy host-to-host. Bezpieczeństwo jest zapewniane na warstwie transportowej wzwyż. Do rooutowania przez Internet jest używany oryginalny adres IP.
- **Tunnel mode**  
  >Cały oryginalny pakiet IP jest enkapsulowany i szyfrowany. Na zewnątrz dodawany jest nowy nagłówek IP - szyfrowanie **IP-in-IP**.  To jest najczęstsze rozwiązanie przy **VPN site-to-site**. Do routowania przez Internet wykorzystywany jest ten nowy nagłówek.
  
![[Pasted image 20251203175635.png]]
