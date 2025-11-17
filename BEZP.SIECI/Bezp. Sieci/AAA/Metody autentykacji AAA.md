
| Metoda                     | Opis                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------ |
| **`none`**                 | Brak autentykacji                                                                    |
| **`enable`**               | Do autentykacji używane jest hasło na `enable`                                       |
| **`local`**                | Wykorzystywana jest lokalna baza użytkowników                                        |
| **`local-case`**           | To samo ale case-sensitive                                                           |
| **`group radius`**         | Używana jest lista wszystkich serwerów [[RADIUS]]                                    |
| **`group tacacs+`**        | Używana jest lista wszystkich serwerów [[TACACS+]]                                   |
| **`group`** *`group-name`* | Jedynie część serwerów (znajdująca się w grupie) jest wykorzystywana do autentykacji |
