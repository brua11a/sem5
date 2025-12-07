Konfiguracja [[ASA Firewall|ASA]] jest podobna do konfiguracji normalnego urządzenia Cisco - routera lub switcha. Jest normalnie `enable`, `conf t`, `int g0/1` itd. Czasem są różnice, niektóre z nich:

![[Pasted image 20251206001700.png]]

Dodatkowa róznica jest taka, że parametr `do` jest niepotrzebny bo z "wyższego" poziomu można wydawać komendy "niższego" poziomu bez problemu. Komenda `help` wyświetla coś jak manual dotyczący innej komendy.

Podstawowa konfiguracja jest podobna (`hostname`, `domain-name`, `banned motd`) z różnicą przy ustawianiu hasła do trybu EXEC (`enable password`*`password`*). Szyfrowanie też jest bardziej skomplikowane:
- **`key config-key password-encryption`** *`password`* - ustawia device-wide master key potrzebny do dalszego szyfrowania
- **`password encryption aes`** - szyfruje wszystkie hasła przy pomocy AES z wykorzystaniem master key