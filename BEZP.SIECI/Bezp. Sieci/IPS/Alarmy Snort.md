[[Sygnatury]] w Snort są konfigurowane przy pomocy tzw. **zasad**. Dzięki nim można porównywać przychodzący ruch z ustalonym w nimi wzorcem. Traffic pasujący do zasady wygeneruje **akcję**.

Każda zasada to jednolinijkowy statement, który określa jakiś typ ruchu, trochę jak [[Lista ACL|ACL]].

#### Budowa zasad w Snort
#### `[action] [protocol] [sourceIP] [sourceport] -> [destIP] [destport]`

**Na przykład:**
`alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any`
Wygeneruj alert za każdym razem gdy połączenie TCP z portu 80 (HTTP) zostanie wywołane z zewnętrznej sieci do sieci wewnętrznej na dowolny port

![[Pasted image 20251127161657.png]]

#### Dodatkowe parametry
Poza samym określeniem podstawowych warunków, można dopisać dodatkowe informacje albo dodatkowo nimi filtrować, na przykład:
![[Pasted image 20251127161849.png]]