Polityka [[IAM]] to dokument w formacie JSON, który w sposób jawny definiuje uprawnienia dotyczące dostępu do zasobów AWS. Określa ona, jakie działania są dozwolone lub zabronione oraz na jakich zasobach i w jakich warunkach mogą być wykonywane.

Polityki nie nadają uprawnień same z siebie - muszą zostać dołączone do tożsamości, czyli [[Użytkownik|użytkownika]], [[Grupa|grupy]] lub [[Rola|roli]], aby mogły zacząć obowiązywać.

Dla długoterminowego dostępu, zalecane jest przypisywanie polityk do grup, a potem przypisywanie użytkowników do tych grup, a potem ewentualnie przypisywanie użytkownikom indywidualnych polityk jeśli jest to wymagane.

![[Pasted image 20251112001516.png]]

Domyślnie, bez polityki dającej jawnego zezwolenia, podmiot nie ma dostępu do niczego. Pozwolenia właśnie tworzy się poprzez polityki. Polityki przypisują uprawnienia *tożsamościom* lub *zasobom*. 

Polityka IAM definiuje **akcje**, które są dozwolone lub zabronione (**effect**), określa **zasoby**, których dotyczą te uprawnienia, oraz **warunki**, pod którymi podmiot może wykonywać operacje na interfejsach API usług AWS.

### AWS obsługuje obecnie sześć typów polityk:
- **Polityki tożsamościowe (Identity-based policies)** – Dołączane do tożsamości IAM, takich jak użytkownicy, role i grupy. Nadają uprawnienia podmiotowi, do którego są przypięte.
  > ![[Pasted image 20251112003606.png]]
  > 
  > Użytkownikowi wolno zrobić wszystko związane ze swoim hasłem (dzięki akcji `iam:*LoginProfile`), wszystko związane ze swoim kluczem dostępu (dzięki akcji `iam:*AccessKey*`) oraz na wszystko związane ze swoim kluczem SSH (dzięki akcji `iam:*SSHPublicKey*`). Jest on ograniczony do jedynie swoich zasobów przez wymienienie `"Resource": ".../${aws:username}"`
- **Polityki oparte na zasobach (Resource-based policies)** – Przypisywane do zasobów AWS (np. S3, Lambda). Nadają uprawnienia podmiotom wskazanym w polityce, również tym z innych kont.
  > ![[Pasted image 20251112003753.png]]
  > 
  > Do zasobów udostępnionych przez konto A (`"Resource": [...]`) zostało przyznane podmiotowi B (koncie AWS o numerze `{"AWS": "11..33"}`) pozwolenie na wykonywanie akcji `"s3:*"`, czyli wszystkiego na tych dwóch S3 Bucketach.
  > 
  > ![[Pasted image 20251112002531.png]]
- **Granice uprawnień (Permissions boundaries)** – Definiują _maksymalny_ zakres uprawnień, jakie polityki tożsamościowe mogą nadać podmiotowi. Same w sobie nie nadają uprawnień. Żeby użytkownik mógł otrzymać uprawnienia, muszą one znajdować się zarówno w granicy uprawnień jak i w przyznanej innej polityce.
  >![[Pasted image 20251112004608.png]]
- **SCP – Service Control Policies (AWS Organizations)** – Definiują _maksymalne_ możliwe uprawnienia dla kont członkowskich w organizacji AWS lub jednostkach organizacyjnych (OU). Mogą ograniczać polityki tożsamościowe i zasobowe, ale nie mogą nadawać uprawnień.
- **Listy kontroli dostępu (ACLs)** – Określają, które podmioty z _innych kont_ mogą uzyskać dostęp do zasobu, do którego ACL jest przypięta. Nie nadają uprawnień podmiotom z tego samego konta. Jako jedyny typ polityk **nie używają formatu JSON**.
- **Polityki sesji (Session policies)** – Używane przy tworzeniu sesji tymczasowych (np. dla roli lub federowanego użytkownika). Mogą tylko **ograniczać** uprawnienia nadawane przez polityki tożsamościowe, nie mogą natomiast nadawać nowych.

### Polityki mogą być *managed* lub *inline*

##### Managed polityki:
Są to samodzielne polityki oparte na tożsamości, które mogą być przypisywane do wielu użytkowników, grup i ról w AWS. Występują w dwóch wariantach: polityki zarządzane przez AWS oraz polityki zarządzane przez użytkownika. Ich głównym celem jest możliwość ponownego wykorzystania, centralnego zarządzania i łatwego udostępniania w różnych częściach środowiska. Managed polityki mogą również współpracować z mechanizmem _granicy uprawnień_, który pozwala określić maksymalny zakres uprawnień, jaki polityki tożsamościowe mogą nadać danej tożsamości IAM.
##### Inline polityki:
Są to polityki bezpośrednio powiązane z konkretnym podmiotem IAM – użytkownikiem, grupą lub rolą. W przeciwieństwie do polityk zarządzanych, każda inline polityka jest **częścią danego podmiotu** i nie istnieje jako samodzielny, wielokrotnie używalny obiekt. Choć można utworzyć identyczne polityki dla różnych podmiotów, każda z nich będzie tak na prawdę osobną polityką ale robiącą to samo.