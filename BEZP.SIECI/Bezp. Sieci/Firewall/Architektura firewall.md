#### Private and Public
Ruch z sieci lokalnej może wyjść do sieci publicznej. Ruch wracający jako odpowiedź od Internetu na zapytanie z sieci lokalnej powinien być dozwolony. Zablokowany jest ruch "z zewnątrz", który nie jest odpowiedzią.

#### Demilitarized Zone
Jest jeden interface podłączony do sieci publicznej, jeden do sieci prywatnej. Z sieci prywatnej ruch może wychodzić bez problemu, ale nie jest dozwolona komunikacja w drugą stronę. Jedyna dopuszczalna wymiana odbywa się pomiędzy DMZ a Internetem, lecz jedynie po inspekcji.

==**Te dwa poprzednie to klasyczne Firewalle**==
#### Zone-based Policy Firewalls - [[ZPF]]
Zone to grupa interface'ów o podobnej funkcjonalności, zatem potrzebujących podobnych pozwoleń i zasobów. Ruch pomiędzy urządzeniami w tym samym zone przechodzi bez problemu, ale zasady ruchu pomiędzy nimi należy zdefiniować - inaczej połączenie \[ zone1 <-> zone2 \] jest domyślnie zablokowane.