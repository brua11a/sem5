Alternatywny sposób przydzielania dostępu. Jest bardziej flexible od zabawy z [[privilege level]]. Polega on na **widokach (views)**.

### Trzy podstawowe widoki
1. **Root View**
   >Administrator, odpowiedzialny za konfigurację WSZYSTKICH innych widoków - dodawanie ich, usuwanie i przyznawanie komend itd. Ma te same uprawnienia, co osoba z privilege level 15, ale nie jest to dokładnie to samo. 
2. **CLI View**
   >Zestaw niezależnych, przyznanych komend. **Nie ma tutaj dziedziczenia**, każdy CLI View jest osobny, dzięki czemu unikane są problemy z tym, że osoby "wyżej" zawsze mają wszystkie komendy osób "niżej". CLI Views może być max 15.
3. **[[Superview]]**
   >Zlepek jednego lub więcej CLI View, używane przez administratorów do grupowania powiązanych ze sobą zestawów uprawnień w CLI View bez przyznawania każdego z nich osobno manualnie.
   >>*A single CLI view can be shared within multiple superviews.
   >>Commands cannot be configured for a superview. An administrator must add commands to the CLI view and add that CLI view to the superview.
   >>Users who are logged into a superview can access all the commands that are configured for any of the CLI views that are part of the superview.
   >>Each superview has a password that is used to switch between superviews or from a CLI view to a superview.
   >>Deleting a superview does not delete the associated CLI views. The CLI views remain available to be assigned to another superview.*
   
![[Pasted image 20251027233726.png]]

### Tworzenie widoków
##### 1. Włącz AAA
> `R#` **`aaa new-model`**

Konieczne do tworzenia jakichkolwiek widoków, bez tego reszta komend nie zadziała.
##### 2. Wejdź w Root View
> `R#` **`enable view`**

`enable view` wchodzi w Root View, `enable view` *`name`* wchodzi w nazwany CLI View, nie Root View - przydatne w [[Debugowanie CLI Views|debugowaniu]]

##### 3. Stwórz nowy CLI View
> `R(config)#` **`parser view`** *`name`*

Stworzony zostaje "pusty" CLI View o nadanej nazwie. Jednocześnie wchodzimy wtedy w konfigurację tego widoku.

##### 4. Zahasłuj widok
> `Router(config-view)#` **`secret`** *`password`*

Hasło dotyczy dostępu do tego jednego widoku. Hasło trzeba ustawić OD RAZU, inaczej error.

##### 5 : (N-1). Przypisz komendy do widoku
> `Router(config-view)#` **`commands`** *`parser-mode`* **`{include | include-exclusive | exclude}`** **`[all]`** `[`**`interface`** *`interface-name`* `|` *`command`*`]`


| Fragment komendy                      | Opis                                                                                                                                  |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **`commands`**                        | Początek komendy, konieczny ofc                                                                                                       |
| *`parser-mode`*                       | Tryb, w którym później opisana komenda istnieje - np. EXEC, configure, interface                                                      |
| a) **`include`**                      | Dodaje później opisaną komendę (lub interfejs) do widoku w sposób nieblokujący                                                        |
| b) **`include-exclusive`**            | Później opisana komenda (lub interfejs) zostaje dodana do widoku ale ŻADEN INNY WIDOK nie może mieć tej komendy!!                     |
| c) **`exclude`**                      | Ten widok nie ma tej komendy (lub interfejsu) - nadpisuje przypisanie przyznawane przez inny widok.                                   |
| 1. `all`                              | Jeśli ten wildcard zostanie użyty, to WSZYSTKIE komendy (lub interfejs) w wybranym wcześniej trybie zostają przypisane do tego widoku |
| 2. **`interface`** *`interface-name`* | W końcu - interface zostaje dodany do widoku                                                                                          |
| 3. *`command`*                        | W końcu - komenda z trybu, która zostaje dodana do widoku                                                                             |
**Przykłady:**
- `R1(config-view)# commands exec include ping`, 
- `R1(config-view)# commands configure include interface GigabitEthernet0/0`

##### N. Wyjdź z konfiguracji widoku
`end`

