Poza przydzieleniem dostępu do zasobów jedynie konkretnym użytkownikom i zaszyfrowaniu danych w spoczynku, należy rozważyć dodatkowe mechanizmy modyfikowania publicznego dostępu. Ponownie, domyślnie publiczny dostęp jest całkowicie zablokowany. Właściciel zasobu może jednak wygenerować tzw. Presigned URL, który pozwala na dostęp do konkretnego obiektu.

#### Na S3, koncie AWS czy AP można ustawić:
1. **BlockPublicAcls**
   >Blokuje wszelkie próby nadania publicznego dostępu poprzez listy ACL. Zapobiega przypadkowemu uczynieniu zasobu publicznym przez błędne ustawienie uprawnień na poziomie obiektu lub bucketu.
2. **IgnorePublicAcls**
   >Ignoruje istniejące reguły ACL, które próbują nadać publiczny dostęp. Nawet jeśli ACL zezwala na dostęp publiczny, nie zostanie on faktycznie zastosowany.
3. **BlockPublicPolicy**
   >Blokuje możliwość dodania lub modyfikacji polityki (bucket policy), która przyznałaby publiczny dostęp do zasobu.
4. **RestrictPublicBucket**
   >Ogranicza publiczny dostęp do zasobów S3 wyłącznie dla usług AWS i autoryzowanych użytkowników w ramach konta — uniemożliwia pełen publiczny dostęp z Internetu.

#### Wersjonowanie
Pozwala na trzymanie wielu wersji tego samego obiektu w tym samym S3. Pozwala na odzyskiwanie danych po przypadkowym usunięciu lub nadpisaniu. Wspierane jest też *MFA delete*, czyli autentykacja wieloetapowa przy próbie usunięcia czegokolwiek.

![[Pasted image 20251113102009.png]]
#### Object lock
Działa jedynie na bucketach z włączonym wersjonowaniem. Dzięki temu rozwiązaniu, obiekty są przechowywane w sposób ***write-once-read-many*** (**WORM**). Zapewnia, że dane nie zostaną zmodyfikowane. 

![[Pasted image 20251113102159.png]]

Blokada obiektów może być wykonywana na dwa sposoby:
- **retention periods**
  >Po prostu odcinek czasu, w którym obiekt jest zablokowany.
- **legal holds**
  >Ograniczenie bez konkretnej daty zakończenia. Obiekty staną się modyfikowalne dopiero gdy jawnie zostanie zdjęta ta blokada.
  
Object Lock działa w dwóch trybach:
- **governance mode**
  >Obiekt nie jest modyfikowalny dla nikogo poza osobami ze specjalnymi uprawnieniami i rootem.
- **compliance mode**
  >Obiekt nie jest modyfikowalny dla nikogo.
  
#### Logging
Jest wbudowanym feature w S3, ale trzeba go włączyć. 