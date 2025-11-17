Serwis służący do audytu i zbierania logów - **akcje** wykonywane przez użytkowników, role czy serwisy są zapisywane w tej usłudze. Działa to z [[IAM]], gdzie chociażby zapisywane będą requesty o zasoby wykonywane przez podmioty. CloudTrail współpracuje też chociażby z konsolą, CLI, SDK i wywołaniami API.  

![[Pasted image 20251115140335.png]]

![[Pasted image 20251115133508.png]]

**Uwaga: czas jest zapisywany w UTC, NIE lokalnym timezone.**

#### Przykładowy log
![[Pasted image 20251115133628.png]]
![[Pasted image 20251115134540.png]]
**[[Użytkownik]] IAM `"Jane"` "jest zasobem" (`"arn"`) o nazwie `"arn:aws:iam:11...33:user/Jane"`:**
- serwis [[IAM]]
- ID konta AWS 11...33
- tożsamość user
- użytkownik Jane
 
**Czyli ten ARN określa: API call został wykonany przez użytkownika IAM o nazwie "Jane" o numerze konta AWS 11...33.**

![[Pasted image 20251115134209.png]]
![[Pasted image 20251115134549.png]]
**Wcześniej zidentyfikowany caller wykonał API call:**
- na EC2 (`"eventSource": "ec2.amazonaws.com"`)
- event to zatrzymanie instancji EC2 (`"eventName": "StopInstances"`)
- wykonana została ta akcja przy pomocy EC2 API Tools (`"userAgent": "ec2-api-tools 1.6.12.2"`)
- stało się to `"2021-07-06 21:01:59"` (UTC)

![[Pasted image 20251115134606.png]]
![[Pasted image 20251115134615.png]]
**Szczegóły wywołania to:**
- zostało ono wywołane na instancji o ID `"i-ebeaf9e2"`
- odpowiedź potwierdza, że maszyna przeszła ze stanu ``"running"`` na `"stopping"`