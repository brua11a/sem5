Największa z nich to to, że agenci [[SNMP]] mogą poprzez [[Żądania SNMP|żądania]] wysyłać i odbierać wszystko tak długo, jak manager sobie tego życzy. W SNMPv1 i SNMPv2 te requesty nie są szyfrowane ani uwierzytelniane, zatem każdy może zająć pozycję managera SNMP i np. zażądać reset urządzenia.

W SNMPv3 ten problem został rozwiązany poprzez mechanizmy szyfrowania, hashowanie, kontrolę dostępu.

**Przykładowo, można skonfigurować SNMPv3 poprzez:**
- `Router(config)#` **`ip access-list`** *`acl-name`*
  >Utwórz nazwaną listę [[ACL]]
- `Router(config-std-nacl)#` **`permit`** *`source_net`*
  > Dodaj do niej sieć, której hosty mają być dozwolone
- `Router(config)#` **`snmp-server view`** *`view-name oid-tree`*
  > Stwarza [[Role-Based CLI|widok]] SNMP o jakiejś nazwie wraz z drzewem OID (zobacz: [[MIB]]), do którego manager ma mieć dostęp
- `Router(config)#` **`snmp-server group`** *`group-name`* **`v3 priv read`** *`view-name`* **`access`** *`[acl-number | acl-name]`*
  >Skonfiguruj `group` na snmp serverze o konkretnej `group-name`, ustaw wersję na `v3`, wymagaj autentykacji i szyfrowania poprzez `priv`, przypisz grupę do `view` i nadaj dostęp jedynie do `read`, wybierz ACL o konkretnej `acl-number`/`acl-name`. 
- `Router(config)#` **`snmp-server user`** *`username group-name`* **`v3 auth {md5 | sha}`** *`auth-password`* **`priv {des | 3des | aes {128 | 192 | 256}`** *`priv-password`*
  >Skonfiguruj `user` na snmp serverze o konkretnym `username`, przypisz go do `group-name`, ustaw wersję na `v3`, wymagaj `auth` poprzez `auth-password` wygenerowany przy pomocy `md5` lub `sha`, a dodatkowo szyfruj ruch przy pomocy `des/3des/aes` z hasłem `priv-password`
  
##### Przykład
```
R1(config)# ip access-list standard PERMIT-ADMIN
R1(config-std-nacl)# permit 192.168.1.0 0.0.0.255  
R1(config-std-nacl)# exit
R1(config)# snmp-server view SNMP-RO iso included
R1(config)# snmp-server group ADMIN v3 priv read SNMP-RO access PERMIT-ADMIN  
R1(config)# snmp-server user BOB ADMIN v3 auth sha cisco12345 priv aes 128 cisco54321  
R1(config)# end
R1#
```

