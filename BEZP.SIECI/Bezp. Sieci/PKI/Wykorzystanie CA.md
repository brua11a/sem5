## Wykorzystanie CA (Certification Authority)

Pierwszym krokiem w autentykacji przy użyciu CA jest zdobycie klucza publicznego CA – *self-signed certificate*.  
- Służy do weryfikacji i **certyfikacji** wszystkich kolejnych elementów wymiany informacji.  
- Jest punktem odniesienia zaufania w całym systemie PKI.  

### Automatyczne rozprowadzanie certyfikatów
Często rozdzielanie certyfikatów CA odbywa się automatycznie, np. w przeglądarkach internetowych:  
- Przeglądarka internetowa jest preinstalowana z zestawem publicznych certyfikatów Root CA.  
- Organizacje i ich domeny WWW przesyłają swoim odwiedzającym certyfikaty publiczne.  
- CAs i rejestratorzy domen tworzą i dystrybuują certyfikaty prywatne i publiczne dla klientów, którzy je zakupili.  

### Proces rejestracji certyfikatu (Certificate Enrollment)
Proces rejestracji certyfikatu pozwala systemowi-hostowi zarejestrować się w PKI:  
1. Certyfikaty CA są pobierane **w sieci** (in-band).  
2. Autentykacja odbywa się **poza siecią** (out-of-band), np. przez telefon.  

Po zarejestrowaniu:  
- Autentykacja między dwoma stronami **nie zależy już od obecności serwera CA**.  
- Użytkownicy wymieniają się certyfikatami zawierającymi klucze publiczne, umożliwiając wzajemne uwierzytelnienie.  

### Zastosowanie PKI
- SSL/TLS certificate-based peer authentication
- Secure network traffic using IPsec VPNs
- HTTPS Web traffic
- Control access to the network using 802.1x authentication
- Secure email using the S/MIME protocol
- Secure instant messaging
- Approve and authorize applications with Code Signing
- Protect user data with the Encryption File System (EFS)
- Implement two-factor authentication with smart cards
- Securing USB storage devices