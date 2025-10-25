#### EXEC
Dostęp do trybu **EXEC** (enable) też można skonfigurować zwykłym nadaniem hasła.
```
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# enable secret cisco1234
Sw-Floor-1(config)# exit
Sw-Floor-1#
```
`enable password` *`password`* istnieje ale nie należy go używać.

#### CON
Standardowo dostęp do **konsoli** można skonfigurować poprzez nadanie hasła bezpośrednio na łączu.
```
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line console 0
Sw-Floor-1(config-line)# password cisco
Sw-Floor-1(config-line)# login
Sw-Floor-1(config-line)# end
Sw-Floor-1#
```

#### VTY
Linie **VTY** służące do zdalnego dostępu też można zabezpieczyć zwykłym hasłem nadanym tylko na interfejsach.
```
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line vty 0 15
Sw-Floor-1(config-line)# password cisco
Sw-Floor-1(config-line)# login
Sw-Floor-1(config-line)# end
Sw-Floor-1#
```

### Jednak w wypadku lini konsolowych i VTY zalecane jest logowanie przy pomocy lokalnej bazy danych!!!