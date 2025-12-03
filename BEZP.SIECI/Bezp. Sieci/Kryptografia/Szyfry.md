W klasycznej kryptografii wyróżniamy kilka kategorii szyfrów.

#### Transposition Ciphers
Litery nie są zastępywane, zamiast tego są "przesuwane", zamieniane miejscami. Przykładem jest zapisanie plaintextu od tyłu:
- plaintext: CHUJ
- szyf: czytaj od tyłu
- ciphertext: JUHC
Same w sobie te algorytmy są słabe, ale jako element potężniejszego rozwiązania są przydatne - np. w AES dalej się korzysta z przestawień.

#### Substitution Ciphers
Litery nie są "przesuwane", zamiast tego są zamieniane na inne. Przykładem szyfru przesunięciowego monoalfabetycznego jest szyfr Cezara, który każdą literę przesuwał o $K$ znaków dalej w alfabecie - polegało to na stałym kluczu. Przykład:
- plaintext: CHUJ
- szyf: Cezar, $K$=1
- ciphertext: DIWK

Monoalfabetyczne szyfry są słabe, dlatego wymyślono wieloalfabetyczne takie jak Vigenere'a. W tej metodzie brana była tabelka dwóch alfabetów, gdzie oś X to litera z ciphertextu a os Y to litera z klucza $K$, będącego ciągiem znaków. Przykład:
- plaintext: CHUJ
- szyfr: Vigenere, $K$="SZ" -> $K_\text{padding}$ = "SZ**SZ**"
  >![[Pasted image 20251129231146.png]]
- ciphertext: UGMI

#### Stream Cipher / One-Time Pad Cipher
Każdy klucz jest wykorzystywany jednorazowo i jest (teoretycznie) losowym ciągiem znaków łączonym w jakiś sposób z oryginalnym tekstem. Odszyfrowanie jest procesem odwrotnym, gdzie ten ciąg jest "odejmowany" od oryginalnego tekstu.

W praktyce jest to ciężkie.