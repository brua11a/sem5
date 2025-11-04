Są to zestawy CLI views przypisane do konkretnej "roli". Pozwalają na wygodniejsze przypisywanie powiązanych ze sobą uprawnień.

### Tworzenie superwidoków

##### 1. Włącz AAA

> `R#` **`aaa new-model`**

Konieczne do tworzenia jakichkolwiek widoków, bez tego reszta komend nie zadziała.

##### 2. Wejdź w Root View

> `R#` **`enable view`**

`enable view` wchodzi w Root View, `enable view` _`name`_ wchodzi w nazwany CLI View, nie Root View - przydatne w debugowaniu
##### 3. Stwórz superview
Proces tworzenia superviews jest podobny do tworzenia zwykłych widoków:
>`Router(config)#` **`parser view`** *`superview-name`* **`superview`**

Czyli jak tworzenie widoku ale słowo kluczowe `superview` pozwala stworzyć i wejść w konfigurację SUPERwidoku. 
==Różnica w stosunku do tworzenia zwykłego widoku: słowo kluczowe `superview`==
##### 4. Zahasłuj
Ponownie, od razu po utworzeniu superwidoku (jak każdego widoku) należy NATYCHMIAST ustawić hasło, inaczej nie przejdziemy dalej.
>`Router(config-view)#` **`secret`** *`password`*

Dopiero wtedy zadziała reszta komend
##### 5 : (N-1). Przypisz view(s) do superview
Nie ma z tego poziomu możliwości tworzenia konkretnych uprawnień jak w zwykłych views. Zamiast tego można je przypisać do właśnie konfigurowanego superwidoku.
>`Router(config-view)#` **`view`** *`view-name`*

Zasady znajdujące się w CLI View o nazwie `view-name` będą obowiązywały również w superwidoku `superview-name`. 
==Różnica w stosunku do tworzenia zwykłego widoku: zamiast przypisywania komend, przypisywane są już gotowe widoki==

##### N. Wyjdź z konfiguracji widoku
`end`