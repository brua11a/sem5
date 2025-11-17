**Security Groups** to wirtualne firewalle działające na poziomie **instancji EC2** w twoim [[VPC]], które kontrolują **ruch przychodzący i wychodzący** z tych instancji. W przeciwieństwie do [[Network ACL]], które działają na poziomie podsieci, Security Groups są przypisywane indywidualnie do instancji - oznacza to, że różne instancje w tej samej podsieci mogą mieć zupełnie inne reguły bezpieczeństwa.

![[Pasted image 20251112214215.png]]

Domyślnie, cały ruch wchodzący (**inbound**) jest blokowany, a cały ruch wychodzący (**outbound**) jest dopuszczany. **Uwaga, w Security Groups nie ma możliwości "deny", zatem odrzuceniem jest brak pozwolenia**.

Security Groups są stanowe (**stateful**), czyli stan jest utrzymywany i zapisywany po wykonaniu zapytania. W praktyce oznacza to, że odpowiedź na ruch wysłany z instancji będzie mógł "wrócić" nawet jeśli inbound zasady teoretycznie na to nie zezwalają.

Zanim jakikolwiek ruch zostanie zezwolony lub odrzucony, sprawdzane są WSZYSTKIE zdefiniowane zasady, które mają pokrycie z tym ruchem. 