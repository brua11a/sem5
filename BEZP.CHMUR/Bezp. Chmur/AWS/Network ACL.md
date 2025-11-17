**Network ACL (Access Control List)** to dodatkowa, opcjonalna warstwa zabezpieczeń w [[VPC]], działająca na **poziomie podsieci**. Pełni rolę firewalla, który kontroluje **ruch przychodzący (inbound)** i **wychodzący (outbound)** dla całej podsieci, a więc wpływa na wszystkie instancje znajdujące się w jej obrębie.

![[Pasted image 20251112214228.png]]

Każda podsieć w [[VPC]] **musi być powiązana z dokładnie jednym Network ACL**, choć jeden ACL może być współdzielony przez wiele podsieci. AWS automatycznie tworzy **domyślny Network ACL**, który zezwala na cały ruch - można go jednak zmodyfikować lub zastąpić własnym.

W przeciwieństwie do [[Security Groups]], **Network ACL są stateless**, co oznacza, że ruch odpowiedzi nie jest automatycznie dozwolony - trzeba jawnie utworzyć odpowiednie reguły dla ruchu w obu kierunkach.

Domyślnie, każdy customowy network ACL blokuje cały ruch inbound i outbound. Dodatkowo, ACL akceptują lub odrzucają ruch na podstawie pierwszego pasującego wpisu z listy - reszta nie jest sprawdzana.