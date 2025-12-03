Pierwsze co trzeba zrobić to wymagać uwierzytelniania na vty, konsoli i aux. Jest to część wstępnej konfiguracji switcha, już dobrze znana. `login` wymusza logowanie.

```
R1(config)# line vty 0 5
R1(config-line)# password ci5c0
R1(config-line)# login
```

Trzeba też skonfigurować SSH do zdalnego dostępu. SSH wymusza nazwę użytkownika i hasło do logowania, uwierzytelnia za pomocą lokalnej bazy danych i zapisuje aktywność. Było to już wcześniej poruszane dla przełącznika, dla routera to wygląda analogicznie.

Na każdym urządzeniu trzeba skonfigurować użytkownika lokalnie, co się słabo skaluje i jest czasochłonne. Nie oferuje też alternatywnej metody logowania. Lepiej, gdy w dużych sieciach nie używamy `local` bazy użytkowników i haseł tylko mamy osobny centralny serwer. Wtedy, użytkownik zamiast weryfikować się na routerze wysyła zapytanie do routera a ten uwierzytelnia go za pomocą serwera AAA. 

Można jeszcze wspomnieć o **802.1X**. Jest to standard oparty na portach. Ogranicza nieautoryzowanym urządzeniom łączenie się z siecią poprzez publiczne porty. Najpierw uwierzytelnia urządzenie, potem dopiero oferuje usługi. Urządzenia w takiej sieci mają role:
1. **Klient (suplikant)**
   >Urządzenie zgodne z 802.1X, które jest dostępne.
2. **Przełącznik (wystawca uwierzytelnienia)**
   >Żąda informacji od klienta, by ten się zidentyfikował, a potem weryfikuje je z serwerem.
3. **Serwer uwierzytelniania**
   >Sprawdza tożsamość klienta i na podstawie tego mówi wystawcy czy klient ma mieć dostęp czy nie

## **A (*Authentication*) -> Uwierzytelnianie**
## **A (*Authorization*)  -> Autoryzacja**
## **A (*Accounting*) -> Ewidencjonowanie**