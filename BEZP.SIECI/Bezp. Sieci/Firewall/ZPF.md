**Zone-based Policy Firewall (ZPF)** to sposób konfiguracji, w którym inferface są przypisywane do *security zones*, a same polityki firewall dotyczą ruchu pomiędzy *security zones* a nie stricte adresów, portów, aplikacji itd.

Nie polega na [[Lista ACL|ACL]], ale również zachowuje zasadę, że jeśli nie ma explicit pozwolenia to jest zakaz, a także da się określić osobne policy dla różnych "kierunków" ruchu.

Od ACL rozróżnia też go to, że może wykonywać inne akcje na pakietach:
1. Inspect - wykonuje stanową inspekcję pakietu, zachowuje sesję i pozwala na ruch powrotny
2. Drop (odpowiednik `deny`)
3. Pass (odpowiednik `permit`) - bezstanowy