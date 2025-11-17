**Elastic Load Balancer (ELB)**, jak sama nazwa wskazuje, jest load balancerem w AWS. Umożliwia **automatyczną dystrybucję ruchu sieciowego lub aplikacyjnego (lub *klasycznego*)** pomiędzy wiele celów (ang. _targets_), takich jak EC2, kontenery, adresy IP.

![[Pasted image 20251112220443.png]]

Konfiguracja load balancera polega na definiowaniu tzw. **listenerów** (_listeners_). Listener to proces nasłuchujący prób połączenia od klientów - na określonym porcie i protokole (np. `TCP:80` lub `HTTPS:443`) - i decydujący, do którego target group (grupy celów) skierować dany ruch. Listener może też wykonywać dodatkowe akcje, takie jak przekierowania, uwierzytelnienia czy terminacje SSL.

Zalecana jest również konfiguracja tzw. *health checks*, dzięki którym cele (*targety*) otrzymują ruch tylko jeśli są *zdrowe*. Można też zintegrować ELB z Auto Scaling, CloudFormation czy Elastic Container Service.

Load balancer ustawiony w podsieci publicznej w naszym VPC może być jedynym publicznym sposobem kontaktu z klientem, co zwiększa bezpieczeństwo i dostępność. Wspierane jest również [[Szyfrowanie danych w spoczynku|szyfrowanie przechowywanych]] logów ELB, a także terminacja TLS na granicy sieci, co ułatwia pracę *targetom* - nie muszą same rozszyfrowywać ruchu HTTPS.

![[Pasted image 20251112221444.png]]
##### ELB działa w postaci trzech typów load balancerów:
- **Application Load Balancer**
  >Działa na poziomie requesta i routuje ruch do *targetów* na podstawie treści żądania. Jest dobry do równoważenia ruchu HTTP i HTTPS i inteligentnej dystrybucji.
- **Network Load Balancer**
  >Działa na poziomie połączenia i routuje ruch do *targetów* w VPC na podstawie danych w nagłówku IP. Działa dobrze zarówno dla TCP jak i UDP. Giga szybki i stabilny.
- **Classic Load Balancer**
  >Zapewnia podstawowe równoważenie obciążenia między wieloma instancjami EC2 i działa zarówno na poziomie żądania (request level), jak i poziomie połączenia (connection level).

![[Pasted image 20251112221557.png]]