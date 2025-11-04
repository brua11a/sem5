Jest to baza danych informacji do [[SNMP]] przechowywana na agentach. Składa się ona z zestawu zmiennych, które można wysyłać i modyfikować w zależności od uprawnień i żądania. 

Zmienne są zorganizowane w sposób hierarchiczny, zazwyczaj w postaci drzewa. Są tam informacje wspólne dla wielu urządzeń sieciowych ale też odgałęzienia z wartościami zmiennych specyficznych dla konkretnego urządzenia. Zazwyczaj te struktury drzewa są ustandaryzowane.

![[Pasted image 20250518130003.png]]

Żeby uzyskać konkretny obiekt, należy wskazać jego OID jako ciąg liczb odseparowany kropkami, na przykład `.1.3.6.1.4.1.9.2.2` żeby dostać się do `interface group`

Takie szukanie liczbami jest niewygodne, dlatego zazwyczaj robi się to przez GUI.
