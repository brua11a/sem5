W [[VPC]] **brama internetowa (internet gateway)** to komponent, który umożliwia komunikację między zasobami uruchomionymi w sieci **publicznej** AWS a Internetem. Pełni rolę „celu” routingu dla instancji, które muszą wysyłać lub odbierać dane z sieci publicznej. Brama internetowa wykonuje również **NAT (Network Address Translation)** dla instancji posiadających publiczne adresy IPv4, dzięki czemu mogą one komunikować się z Internetem, zachowując jednocześnie bezpieczeństwo i kontrolę nad ruchem.

NAT jest potrzebny bo instancje w VPC mają i adres publiczny i prywatny, zatem NAT służy do mapowania pomiędzy nimi.

Aby brama internetowa działała poprawnie, należy:
- utworzyć ją i **podłączyć do swojego VPC**,
- dodać odpowiednią **trasę w tablicy routingu** dla podsieci, aby ruch kierowany do Internetu był przesyłany do bramy,
- upewnić się, że instancje w tej podsieci posiadają **globalnie unikalne adresy IP** (np. publiczne adresy IPv4 lub przypisane Elastic IP),
- sprawdzić, czy konfiguracje **Network ACL** oraz **[[Security Groups]]** pozwalają na ruch w obu kierunkach - zarówno wychodzący, jak i przychodzący, zgodnie z oczekiwaniami aplikacji.

![[Pasted image 20251112211512.png]]
(na obrazku zły practice, w publicznej podsieci powinien być [[ELB|Load Balancer]], który przekazywałby ruch do instancji EC2 w sieciach prywatnych)

---

Amazon **NAT Gateway** (Network Address Translation Gateway) to zarządzana usługa AWS, która umożliwia **instancjom w prywatnych podsieciach** łączenie się z Internetem lub innymi usługami AWS - **bez umożliwienia połączeń przychodzących z Internetu**.

Żeby NAT Gateway działał poprawnie, należy:
- określić podsieć publiczną, w której ma się znajdować
- nadać jej publiczny adres IP
- zaktualizować tabele routingu w prywatnych sieciach podpiętych do bramy tak, by ruch wychodzący do internetu był kierowany do NAT Gateway

![[Pasted image 20251112211406.png]]