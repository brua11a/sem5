Służy do tego komenda:
> **`username`** *`name`* **`{  password | secret  }`** *`password`* w najprostszej postaci

Samo `secret` używa co najwyżej szyfrowania 5 (hash MD5), czyli słabego. Podobnie, jak w wypadku [[Szyfrowanie haseł|dostępu do trybu EXEC]], można wybrać silniejszą metodę dzięki dopisaniu **`algorithm-type`** *`{  md5 | scrypt | sha256  }`*

#### `username name secret hasło` -> `username` **`algorithm-type` *`algorytm`*** `secret hasło`

`username` *`name`* ~~`password` *`password`*~~ nie powinno nigdy być używane.