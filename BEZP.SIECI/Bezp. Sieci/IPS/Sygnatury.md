Malicious ruch sieciowy ma pewne charakterystyczne cechy/zachowania, które nazywa się **sygnaturami**. Właśnie one są wykorzystywane przez [[Wykrywanie ataków|IDS]] i [[IPS]] do wykrywania ataków. Dla znanego już ataku (z zapisaną sygnaturą) może być zdefiniowane odpowiednie zachowanie prewencyjne.

Sygnatury mają trzy atrybuty:
#### Type

Może to być **Atomic Signature** - pojedynczy pakiet, aktywność lub zdarzenie świadczą o ataku. Nie jest wymagane zapamiętanie stanu i odpowiedź jest szybka.

Inny typ to **Composite Signature**, gdzie dopiero połączenie kilku fragmentów danych informuje o ataku. Stan jest utrzymywany na czas tzw. *event horizon*, którego długość zależy od implementacji.
#### Trigger - alarm

Coś, co dla IPS **może oznaczać próbę ataku**, na przykład dla Network IPS może to być jakiś ciąg znaków wysłany do konkretnego portu. Mechanizmy ataku, triggery, można przypisać do ataków atomic i composite.

##### Wyróżniamy triggery:
1. **Pattern-Based Detection**
   >Bazuje na samym wykrywaniu sygnatur. Szuka atomicznych lub złożonych patternów. IPS porównuje ruch sieciowy z bazą znanych ataków.
2. **Anomaly-Based Detection**
   >Nazywane też profile-based detection. Zaczyna się od określenia jaki ruch jest normalny dla hosta, ustalenia baseline. Wszystko co nie pasuje do tego baseline jest traktowane jako próba nadużycia.
3. **Policy-Based Detection**
   >Nazywane też nehavior-based detection. Zachowania są definiowane manualnie, w szczególności te podejrzane.
4. **Honey Pot-Based Detection**
   >Używany jest decoy server, który udaje prawdziwy by przyciągnąć atakujących. Ataki można wtedy przeanalizować.
#### Action - co zrobi IPS

![[Pasted image 20251127014256.png]]