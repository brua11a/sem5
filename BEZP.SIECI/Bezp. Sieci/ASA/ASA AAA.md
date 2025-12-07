ASA może służyć zarówno do [[Local AAA|lokalnego AAA]] jak i [[Server-Based AAA]]. Te pierwsze używa lokalnej bazy użytkowników.

#### Lokalne
1. `username name password passowrd [privilege priv_level]`

#### Server-Based
1. `ASA(config)#` **`aaa-server`** *`server-tag`* **`protocol tacacs+/radius`**
   >Tworzy server group do autentykacji TACACS+ lub RADIUS
2. `ASA(config-aaa-server-group)#` **`aaa-server`** *`server-tag`* *`[(if_name)]`* **`host`** *`{server-ip | name }`* *`[ key ]`*
   >Konfiguruje wcześniej utworzoną server group - konkretnie konfiguruje serwer jako część grupy, ewentualnie modyfikuje parametry połączenia
3. `ASA(config)# aaa authentication { serial | enable | telnet | ssh | http } console { LOCAL | server-group [ LOCAL ]}`
   >Ustaw globalnie [[metody autentykacji AAA]]. Różnią się one tym, że można albo używać bazy lokalnej (`LOCAL`) albo `server-group` z falloverwem `LOCAL`