Ważne jest pamiętanie o kolejności konfiguracji [[ZPF]] - jeśli każdemu routerowi np. używać listy, której jeszcze nie ma to wyskoczy error.

![[Pasted image 20251126003526.png]]
#### Określ zone(s) - `zone`
Należy przemyśleć jakim użytkownikom będzie do czego potrzebny dostęp, a także jak ruch będzie płynął w sieci - w którą stronę i jaki.

**Zone definiuje się komendą:**
> `Router(config)#` **`zone security`** *`zone-name`*

Na przykład, żeby stworzyć sobie zone o nazwach `PRIVATE` i `PUBLIC` należy wpisać:
```
R1(config)# zone security PRIVATE
R1(config-sec-zone)# exit
R1(config)# zone security PUBLIC
R1(config-sec-zone)# exit
R1(config)#
```

#### Określ pożądany ruch - `class-map`
Zasady filtrowania ruchu są przypisywane do tzw. class-map, które jest swego rodzaju [[Zasady ruchu ZPF|policy]], gdzie na podstawie "match conditions" dane są przechwytywane, a co robi się z nimi dalej (odrzuca, przyjmuje lub inspektuje) definiuje się potem.

**Policy definiuje się komendą:**
>`Router(config)#` **`class-map type inspect`** **`[match-any | match-all]`** *`class-map-name`*
>- `match-any` oznacza, że jeśli przynajmniej jeden match criteria się zgadza to ruch przechodzi.
>- `match-all` wymaga, by wszystkie zasady się zgadzały

**Wpisy do policy można dodawać następująco:**

| Parametr                                                         | Opis                                                                                                             |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `Router(config-cmap)# match access-group {acl-# `\|` acl-name }` | Do policy dodaj kryteria na podstawie tego ACL                                                                   |
| `Router(config-cmap)# match protocol protocol-name`              | Do polucy dodaj kryterium dotyczące protokołu                                                                    |
| `Router(config-cmap)# match class-map class-map-name`            | Do policy dodaj inne class-map, pewnie chodzi o to by moc korzystac z "ogolnego" policy i potem je doszlifowywac |
```
R1(config)# class-map type inspect match-any HTTP-TRAFFIC
R1(config-cmap)# match protocol http
R1(config-cmap)# match protocol https
R1(config-cmap)# match protocol dns
```

W przykładzie powyżej powstała class-map, który oznacza, że urządzenia w zone z tym przypisanym policy mogą generować ruch http, https i dns.

#### Zdefiniuj zachowania - `policy-map`
Gdy już posiadamy class-map "łapiący" ruch, to teraz można użyć policy-map, żeby zdecydować co zrobić z takim ruchem

```
R1(config)# policy-map type inspect policy-map-name
R1(config-pmap)# class type inspect class-map-name
R1(config-pmap-c)# {inspect | drop | pass}
```

Jest to tak rozdzielone, by móc na podstawie tego samego class-map zrobić wiele policy-map, gdzie zachowania mogą być inne.

```
R1(config)# policy-map type inspect PRIV-TO-PUB-POLICY
R1(config-pmap)# class type inspect HTTP-TRAFFIC
R1(config-pmap-c)# inspect
```

#### Zidentyfikuj [[Zone Pair]] i przypisz do policy - `zone-pair`, `service-policy`

```
R1(config)# zone-pair security PRIV-PUB source PRIVATE destination PUBLIC
R1(config-sec-zone-pair)# service-policy type inspect PRIV-TO-PUB-POLICY
```

Przy tej konfiguracji ruch pochodzący "z zewnątrz" nie będzie mógł wejść, ale będzie mógł wrócić jako odpowiedź dzięki `inspect`.

#### Przypisz pożądane interface na routerze do zone - `zone-member`

```
R1(config)# interface GigabitEthernet 0/0
R1(config-if)# zone-member security PRIVATE
R1(config-if)# interface Serial 0/0/0
R1(config-if)# zone-member security PUBLIC
```