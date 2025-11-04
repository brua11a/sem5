To skrypt na nowszych wersjach urządzeń Cisco, który automatycznie ustawia wszystkie podstawowe zalecenia odnośnie bezpieczeństwa - banner, bezpieczne logowanie, SSH, odpowiednio skonfigurowane serwisy.

Można go traktować jako baseline konfiguracji, który potem można dostosowywać do swoich potrzeb.

```
R1# auto secure  
  --- AutoSecure Configuration ---
 
*** AutoSecure configuration enhances the security
of the router but it will not make router
absolutely secure from all security attacks ***
 
All the configuration done as part of AutoSecure
will be shown here. For more details of why and
how this configuration is useful, and any possible
side effects, please refer to Cisco documentation of
AutoSecure.
 
At any prompt you may enter '?' for help.
Use ctrl-c to abort this session at any prompt.
 
Gathering information about the router for
AutoSecure
 
Is this router connected to internet? [no]:yes
```

AutoSecure ma wiele sposobów działania
> `Router#` **`auto secure`** *`{no-interact | full} [forwarding | management] [ntp | login | ssh | firewall | top-intercept]`*


| Fragment komendy                              | Za co odpowiada                                                                                                                                                                    |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`auto secure`**                             | Początek komendy - samo w sobie też zadziała, ale wymusi wybór `full` lub `no-interact`                                                                                            |
| *`no-interact`*                               | Nieinteraktywna sesja, po prostu ustawią się domyślne ustawienia.                                                                                                                  |
| ***`full`***                                  | Domyślny setting, pozwala na konfigurację auto secure w sposób interaktywny, gdzie skrypt będzie po kolei pytał nas co i jak zrobić                                                |
| *`forwarding`*                                | Tylko *forwarding plane* zostanie zabezpieczony (zabezpieczenie przepływu danych). Jeśli nie zostanie określone, to obydwa plane'y się skonfigurują, ale tylko po części.          |
| *`management`*                                | Tylko *management plane* zostanie zabezpieczony (zabezpieczenie dostępu administracyjnego). Jeśli nie zostanie określone, to obydwa plane'y się skonfigurują, ale tylko po części. |
| *`ntp`*                                       | Pozwala określić konfigurację NTP                                                                                                                                                  |
| *`login`, `ssh`, `firewall`, `tcp-intercept`* | Podobnie jak wyżej, można jednocześnie kilka na raz, żeby od razu skonfigurować kilka elementów w rozszerzony sposób.                                                              |
