Bezpieczna, szyfrowana alternatywa dla protokołu Telnet. Służy do zdalnego dostępu do urządzeń. Dla urządzeń takich jak routery czy switche są wymagane kroki:
1. **Ustaw unikatowy hostname.**
   >Pozwala to zidentyfikować urządzenie w domenie, a także jest dołączany do niej przy generowaniu klucza.
   >`Router(config)# hostname R1`
2. **Ustaw IP domain-name.**
   >Nazwa domeny jest wykorzystywana w generowaniu klucza.
   >`R1(config)# ip domain name span.com`
3. **Wygeneruj klucz SSH.**
   >Pozwala on na asymetryczne szyfrowanie ruchu pomiędzy urządzeniem źródłowym a docelowym.
   >`R1(config)# crypto key generate rsa general-keys modulus 1024`
4. **[[Tworzenie użytkowników|Stwórz użytkowników w lokalnej bazie danych.]]**
   >Na tych użytkowników będą logowali się użytkownicy próbujący uzyskać dostęp do urządzenia.
   >`R1(config)# username Bob secret cisco`
5. **Spraw, by linie VTY wykorzystywały lokalną bazę danych.**
   >Bez tego logowanie nie będzie wykorzystywało użytkownika z poprzedniego kroku.
   >`R1(config)# line vty 0 4`
   >`R1(config-line)# login local`
6. **Pozwól na ruch SSH na liniach VTY.**
   >Domyślnie, nie jest on dozwolony, ale można to zmienić.
   >`R1(config-line)# transport input ssh`

Dodatkowo można ustawić timeout w sekundach oraz ilość dozwolonych prób logowania, a także podejrzeć informacje o konfiguracji ssh.

```
R1(config)# ip ssh time-out 60
R1(config)# ip ssh authentication-retries 2
R1# show ip ssh
SSH Enabled - version 2.0
Authentication methods:publickey,keyboard-interactive,password
Authentication timeout: 60 secs; Authentication retries: 2
```

---


Jeśli klucz RSA już istnieje (sprawdź `show crypto key mypubkey rsa`) to należy go "wyzerować" za pomocą:
> `R1(config)# crypto key zeroize rsa`

Przykładowy wygenerowany klucz:

![[Pasted image 20251026004823.png]]