**IKE** umożliwia automatyczną [[Negocjacja IKE IPsec|negocjację parametrów]] i bezpieczną komunikację w ramach **IPsec**.  
Bez IKE konfiguracja IPsec byłaby ręczna i czasochłonna, ponieważ każda strona musiałaby ręcznie dopasować algorytmy szyfrowania, hashowania i polityki bezpieczeństwa.

W Phase 1 urządzenia próbują ustalić wspólne parametry (algorytmy szyfrowania, hashe itd.) i polityki bezpieczeństwa, a także autentykują się nawzajem (PSK, certyfikaty RSA).

![[Pasted image 20251203180317.png]]

Poza ustalaniem parametrów, IKE generuje też klucz współdzielony na podstawie serii wymiany pakietów danych przez dwie strony. Dzięki temu osoba trzecia nie może zdobyć klucza, bo nie jest on de facto nigdzie wysyłany.

Powstaje na koniec bezpieczny tunel. W tym bezpiecznym tunelu wykorzystywanym w Phase 2 dostosowywane są konkretne polityki IPsec (które pakiety będą chronione i jakie algorytmy szyfrowania i uwierzytelniania będą stosowane w ESP).

![[Pasted image 20251203180949.png]]
