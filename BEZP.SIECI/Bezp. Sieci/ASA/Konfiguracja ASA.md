### `ciscoasa(config)# interface`*`interface`*
##### Adres IP

| **Komenda**                          | **Opis**                                                  |
| ------------------------------------ | --------------------------------------------------------- |
| **`ip address`** *`ip-addr netmask`* | Manualne ustawienie adresu IP na interface                |
| **`ip address dhcp`**                | Interface będzie requestował serwer DHCP o adres          |
| **`ip address dhcp setroute`**       | Od serwera DHCP będzie brany adres i brama domyślna       |
| **`ip address pppoe`**               | Interface będzie brał adres IP od urządzenia wysyłającego |
| **`ip address pppoe setroute`**      | Poza adresem IP będzie też brana ścieżka do urządzenia    |
##### [[ASA security level]] - OBOWIĄZKOWY
| **Komenda**                   | **Opis**                                                                                                                         |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **`nameif`** *`if-name`*      | Nazywa interface, nie jest case-sensitive. <br>Uwaga - żeby nadpisać, wydaj komendę ponownie<br>z nową nazwą zamiast używać `no` |
| **`security-level`*`value`*** | Ustawia security level od 0 (najnizszy) do 100 (maksymalny)                                                                      |
| **`no shutdown`**             | Włącz                                                                                                                            |
##### Domyślna trasa statyczna
| **Komenda**                                                                | **Opis**                                                                                                                                             |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`route`** *`interface-name`*<br>**`0.0.0.0 0.0.0.0`**<br>*`next-hop-ip`* | Tworzy trasę statyczną globalnie na całym ASA.<br>Należy określić interface, z którego ruch będzie wychodził,<br>a także adres następnego przeskoku. |
##### Dostęp zdalny
| **Komenda**                                            | **Opis**                                                                                                                            |
| ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **`password`** *`password`*                            | Ustawia hasło loginu zdalnego, uwierzytelnienie na liniach vty                                                                      |
| **`telnet`** *`ip_addr mask name`*                     | Określa jakie hosty lub sieci mogą łączyć się Telnetem do ASA                                                                       |
| **`clear configure telnet`**                           | Usuń telnet                                                                                                                         |
| **`username`** *`name`*<br>**`password`** *`password`* | Tworzy lokalnego użytkownika                                                                                                        |
| **`aaa authentication`<br>`ssh console LOCAL`**        | SSH będzie się odwoływał do lokalnej bazy danych w celu autentykacji                                                                |
| **`crypto key generate`<br>`rsa modulus`** *`size`*    | Tworzy klucz RSA używany w szyfrowaniu SSH, powinien miec dlugość min. 2048                                                         |
| **`ssh`** *`ip_addr mask`*<br>*`name`*                 | Określa jakie hosty mogą próbować łączyć się SSH do ASA. `if_name` jest opcjonalny, bez niego komenda zadziała na wszystkich iface. |
##### Integracja z [[NTP]]
| **Komenda**                                              | **Opis**                                                                                |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **`ntp authenticate`**                                   | Włącza autentykację wobec serwera NTP                                                   |
| **`ntp trusted-key`** *`key_id`*                         | Klucz o wybranym ID będzie kluczem zaufanym,<br>używanym do autentykacji                |
| **`ntp authentication-key`**<br>*`key_id hash_algo key`* | "Tworzy" klucz używany do autentykacji NTP wykorzystujący<br>wybrany algorytm hashujący |
| **`ntp server`** *`ip_addr`*                             | Wybiera serwer NTP, do którego odwołuje się ASA                                         |
##### ASA jako serwer DHCP
| **Komenda**                                         | **Opis**                                                                  |
| --------------------------------------------------- | ------------------------------------------------------------------------- |
| **`dhcpd address`** *`ip_addr1 - ip_addr2 if_name`* | Tworzy pulę adresów DHCP w tej samej podsieci do interface ASA            |
| **`dhcpd enable`** *`interface_name`*               | Włącza DHCP na interface - podłączone urządzenia mogą korzuystać z usługi |
| **`dhcpd dns`** *`dns`*                             | Opcjonalnie wskazuje jaki jest serwer DNS                                 |
| **`dhcpd lease`** `time`                            | Opcjonalnie zmienia lease time z 3600s do nawet 1048575 sekund            |
| **`dhcpd domain`** *`domain_name`*                  | Opcjonalnie określa domenę                                                |
