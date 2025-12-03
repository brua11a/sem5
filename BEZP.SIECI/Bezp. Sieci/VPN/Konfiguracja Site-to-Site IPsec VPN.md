Wymaga ona konfigurację obydwu [[Negocjacja IKE IPsec|faz negocjacji IPsec]] - musi powstać tunel IKE a potem w tym tunelu musi powstać tunel IPsec.

![[Pasted image 20251203221646.png]]

W tej topologii jest statyczny routing i odpowiednie adresy IP.

### 1. "Phase 0" - prerekwizyty
Żeby ruch IKE i IPsec w ogóle był możliwy, należy zezwolić na ruch UDP protokół ISAKMP (czyli w praktyce IKE), ruch ESP i AHP (dwa typy IPsec).

```
R1(config-ext-nacl)# permit udp host 172.30.2.2 host 172.30.2.1 eq isakmp
R1(config-ext-nacl)# permit esp host 172.30.2.2 host 172.30.2.1
R1(config-ext-nacl)# permit ahp host 172.30.2.2 host 172.30.2.1
```

Taką ACL należy zastosować na interface ustawionym w stronę drugiego routera próbującego ustanowić tunel - tutaj `R1 S0/0/0 inbound`. Dodatkowo, by zapewnić multicasty i broadcasty należy rozważyć dodanie GRE (Generic Routing Ecnapsulation).

> `R1(config)# access-list 101 permit ip 10.0.1.0 0.0.0.255 192.168.1.0 0.0.0.255`

Należy zacząć też zdefiniować "interesujący" ruch jako [[Lista ACL|listę ACL]]. Jeśli coś będzie pasowało do tej ACL to będzie powodowało stworzenie tunelu w Phase 1. Ta ACL definiuje ruch z Site 1 do Site 2.

### Phase 1 - tunel ISAKMP (IKE)
Kilka polityk jest domyślnie zdefiniowanych, można je podejrzeć dzięki `show crypto isakmp default policy`. Są one oznaczone numerami. Domyślnie, router będzie używać najbezpieczniejszej z nich (najniższy numer), a jeśli się nie uda to spróbuje tej o niższym bezpieczeństwie aż coś się uda. Na potrzeby nauki trzeba jednak zrobić własną policy.
#### `R1(config)# crypto isakmp policy` *`priority`*
Tą komendą można stworzyć nową politykę, gdzie niższy numer oznacza wyższy priorytet. Po wpisaniu tej komendy można ustanowić pięć podstawowych cech polityki:
1. **Hash** - algorytm hashowania, tutaj SHA
2. **Authentication** - sposób autentykacji, tutaj PSK
3. **Group** - grupa DH (czyli zestaw parametrów używanych w wymianie kluczy DH), tutaj #24
4. **Lifetime** - "czas życia", tutaj 3600s
5. **Encryption** - algorytm szyfrowania, tutaj AES 256

```
R1(config)# crypto isakmp policy 1
R1(config-isakmp)# hash sha
R1(config-isakmp)# authentication pre-share
R1(config-isakmp)# group 24
R1(config-isakmp)# lifetime 3600
R1(config-isakmp)# encryption aes 256
```

Żeby PSK działało trzeba go jeszcze ustawić na obydwu routerach. 
>`Router(config)# crypto isakmp key` *`keystring`* `address` *`peer-address`*

```
R1# conf t
R1(config-isakmp)# crypto isakmp key cisco12345 address 172.30.2.2

R2# conf t
R2(config-isakmp)# crypto isakmp key cisco12345 address 172.30.2.1
```

### Phase 2 - tunel IPsec
Pierwszy krok to zdefiniowanie zestawu algorytmów szyfrowania i hashowania użytych w Phase 2. Ten zestaw nazywa się `transform-set`. Należy wybrać jedną z dostępnych opcji po wymyśleniu jakiejś nazwy. Większość z tych wpisów to `AH/ESP-encryption/hashing-version`.

```
R1(config)# crypto ipsec transform-set ?
  WORD  Transform set tag
 
R1(config)# crypto ipsec transform-set R1-R2 ?
  ah-md5-hmac      AH-HMAC-MD5 transform
  ah-sha-hmac      AH-HMAC-SHA transform
  ah-sha256-hmac   AH-HMAC-SHA256 transform
  ah-sha384-hmac   AH-HMAC-SHA384 transform
  ah-sha512-hmac   AH-HMAC-SHA512 transform
  esp-3des         ESP transform using 3DES(EDE) cipher (168 bits)
  esp-aes          ESP transform using AES cipher
  esp-des          ESP transform using DES cipher (56 bits)
  esp-gcm          ESP transform using GCM cipher
  ...
```

Żeby tunel powstał, wybrane tu metody muszą być spójne po obydwu stronach.

```
R1(config)# crypto ipsec transform-set R1-R2 esp-aes esp-sha-hmac
R1(config)#

R2(config)# crypto ipsec transform-set R1-R2 esp-aes esp-sha-hmac
R2(config)#
```

Kolejnym krokiem jest wykorzystanie zdefiniowanego wcześniej "interesującego" ruchu oraz zasad IPsec i przypisanie ich do reszty polityki IPsec dzięki **crypto map**.

#### `Router(config)#` **`crypto map`** *`map-name seq-num`* **`ipsec-isakmp`**

| Fragment komendy   | Za co odpowiada                                                                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`crypto map`**   | Początek komendy                                                                                                                                                                        |
| *`map-name`*       | Nazwa zwyczajowa mapy                                                                                                                                                                   |
| *`seq-num`*        | Numer sekwencyjny przypisany tej mapie - ważny gdy definiowane jest wiele map, ale tutaj nie. `crypto map map-name seq-num` samo w sobie pozwala na modyfikowanie już istniejącej mapy. |
| **`ipsec-isakmp`** | Oznacza, że IKE będzie wykorzystywane do stworzenia połączenia IPsec VPN zgodnie z zasadami wpisanymi w tej mapie.                                                                      |
Po stworzeniu mapy tą komendą należy ją skonfigurować.
1. Przypisz ACL "interesującego" ruchu do mapy
2. Przypisz transform-set do mapy
3. Ustaw adres IP urządzenia pośredniczącego (tego, które będzie "przyjmowało" ruch VPN po drugiej stronie i go przetłumaczy dla reszty sieci)
4. Skonfiguruj grupę DH
5. Ustaw lifetime tunelu IPsec

```
R1(config)# crypto map R1-R2_MAP 10 ipsec-isakmp
% NOTE: This new crypto map will remain disabled until a peer
        and a valid access list have been configured.
R1(config-crypto-map)# match address 101
R1(config-crypto-map)# set transform-set R1-R2
R1(config-crypto-map)# set peer 172.30.2.2
R1(config-crypto-map)# set pfs group24
R1(config-crypto-map)# set security-association lifetime seconds 900
R1(config-crypto-map)# exit
R1(config)#
```

```
R2(config)# crypto map R1-R2_MAP 10 ipsec-isakmp
% NOTE: This new crypto map will remain disabled until a peer
        and a valid access list have been configured.
R2(config-crypto-map)# match address 102
R2(config-crypto-map)# set transform-set R1-R2
R2(config-crypto-map)# set peer 172.30.2.1
R2(config-crypto-map)# set pfs group24
R2(config-crypto-map)# set security-association lifetime seconds 900
R2(config-crypto-map)# exit
R2(config)#
```

#### `R1(config-if)# crypto map R1-R2_MAP`
Ostatni krok - ustaw mapę na interface