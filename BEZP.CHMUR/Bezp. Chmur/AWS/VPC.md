Amazon **Virtual Private Cloud (VPC)** to usługa umożliwiająca tworzenie **wirtualnej, prywatnej sieci** w ramach infrastruktury AWS. Daje ona możliwość uruchamiania zasobów w logicznie odizolowanym fragmencie chmury, który użytkownik w pełni kontroluje pod względem konfiguracji sieciowej.

W ramach VPC można samodzielnie określić **zakres adresów IP**, tworzyć **podsieci**, definiować **tabele routingu** oraz konfigurować **bramy sieciowe** i inne elementy infrastruktury sieciowej. VPC obsługuje zarówno sieci **publiczne** (z dostępem do Internetu), jak i **prywatne**, które są odizolowane od ruchu zewnętrznego.

Dodatkowo VPC zapewnia wbudowane mechanizmy bezpieczeństwa, takie jak **[[Security Groups]]** (kontrola ruchu na poziomie instancji) oraz **Network Access Control Lists (ACLs)** (kontrola ruchu na poziomie podsieci), które umożliwiają precyzyjne zarządzanie przepływem ruchu sieciowego w obrębie wirtualnej chmury.

![[Pasted image 20251112162843.png]]

VPC musi całe znajdować się w jednym regionie, ale może rozciągać się na wiele stref dostępności. Możliwe jest też podzielenie swojego VPC na wiele podsieci składających się z jakiegoś zakresu adresów IP. Podsieć należy do jednej strefy dostępności, ale można stworzyć wiele podsieci w różnych strefach dostępności, co zwiększa dostępność (!!!!!!!!!!!).

![[Pasted image 20251112212612.png]]

Informacje na temat ruchu sieciowego (inbound i outbound) dziejącego się w VPC (na poziomie VPC, podsieci lub interfejsu) mogą być zapisywane dzięki **VPC Flow Logs**, gdzie są one wysyłane do [[CloudWatch]] lub S3. Flow Logs są zbierane inną "ścieżką", niż reszta ruchu sieciowego, zatem funkcja nie wpływa na performance. 

### Kompletny przykład

![[Pasted image 20251112221619.png]]