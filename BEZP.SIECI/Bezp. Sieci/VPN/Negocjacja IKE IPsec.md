Jest wykonywana przed jakimkolwiek stworzeniem bezpiecznego tunelu [[IPSec]] [[VPN]] poprzez [[IKE]]. Jak sama nazwa wskazuje, negocjacja pozwala wynegocjować parametry pomiędzy dwoma stronami.  

Wymiana zaczyna się, gdy host A wyśle do hosta B ruch uznany za "interesujący" (czyli spełniający określone kryteria, pasujący do odpowiedniej [[Lista ACL|ACL]]) – wtedy tworzy się tunel **ISAKMP (nazywany też tunelem IKE)**.  

W tunelu tym, w **Phase 1**, są uzgadniane **polityki IKE**:
- algorytm szyfrowania (np. AES, 3DES)  
- algorytm hashowania / integralności (np. SHA-1, SHA-2)  
- sposób uwierzytelniania (PSK lub certyfikaty)  
- grupa Diffie-Hellmana (DH)  
- czas życia (lifetime) SA  

![[Pasted image 20251203183923.png]]

Na podstawie wynegocjowanych parametrów w **Phase 2** tworzony jest bezpieczny tunel **IPSec**, w którym definiowane są **polityki IPSec**:
- algorytm szyfrowania (AES, 3DES, ChaCha20)  
- algorytm integralności (HMAC-SHA1, HMAC-SHA2)  
- tryb działania (Transport lub [[Protokoły IPsec VPN|Tunnel]])  
- selektory ruchu (który ruch ma być szyfrowany)  
- czas życia (lifetime) SA  

![[Pasted image 20251203183930.png]]
##### **IKE / Phase 1** – negocjuje, jak strony będą się bezpiecznie komunikować (klucze, autentykacja)
##### **IPSec / Phase 2** – zabezpiecza faktyczny ruch sieciowy w tunelu, zgodnie z wynegocjowanymi politykami.  
