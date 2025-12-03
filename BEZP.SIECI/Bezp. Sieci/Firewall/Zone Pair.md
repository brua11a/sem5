Zone pair służy w [[ZPF]] definiowanie zachowania przy przejściu z *Zone A* do *Zone B*. Bez niego, ruch między zone jest domyślnie zablokowany. 

Opcjonalnie, po stworzeniu pary można jeszcze dopisać policy-map, który został wcześniej zdefiniowany. Wtedy ruch zostanie odpowiednio przefiltrowany.

**Definiowanie zone pair:**
> `Router(config)#` **`zone-pair security`** *`zone-pair-name`* **`source`** *`{source-zone-name | self}`* **`destination`** *`{destination-zone-name | self}`*

Czyli ruch z pierwszego zone do drugiego zone będzie dozwolony dzięki zone pair o jakiejś nazwie, ale dodatkowo...

**Przypisywanie policy-map do zone pair:**
> `Router(config-sec-zone-pair)#` **`service-policy type inspect`** *`policy-map-name`*

Teraz ruch będzie poddawany inspekcji przed podaniem dalej i będzie zapisywany stan.

Słowem kluczowym `self` zamiast nazwy src lub dest zone można sprawić, żeby ruch był określony "[[Self Zone|do siebie]]".

```
R1(config)# zone-pair security PRIV-PUB source PRIVATE destination PUBLIC
R1(config-sec-zone-pair)# service-policy type inspect PRIV-TO-PUB-POLICY
```