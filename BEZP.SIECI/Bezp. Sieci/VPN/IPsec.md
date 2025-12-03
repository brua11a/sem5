Może służyć do połączeń site-to-site [[VPN]]. Chroni ruch w warstwach od 4 do 7 poprzez szyfrowanie i bezpieczną wymianę kluczy, a także weryfikację pochodzenia. Elementy IPsec można sobie dobierać wedle uznania i potrzeb:
### 1. **[[Protokoły IPsec VPN|Protokół]]**
   >AH (*Authentication Header* - uwierzytelnianie pakietu), ESP (*Encapsulation Security protocol* - szyfrowanie pakietu) lub to i to (AH powoduje problem z NAT)
### 2. **Poufność**
   >Poprzez algorytm szyfrowania symetrycznego. DES, 3DES, AES, brak...
### 3. **Integralność**
   >MD5, SHA...
### 4. **Uwierzytelnianie**
   >W tym weryfikacja źródła - [[IKE]] (*Internet Key Exchange*). PSK, RSA...
### 5. **Diffie-Hellman**
   >DH1, DH2... zalecane DH14+
   
![[Pasted image 20251203172424.png]]
