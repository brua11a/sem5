![[Pasted image 20260128134357.png]]

#### Kryteria:
1. **Koszt**
2. **Stopy błędów**
3. **Szybkość obliczeń**
4. **Łatwość pobierania**
5. **Prywatność**
6. **Łatwość użycia**
7. **Dojrzałość**
   >Jeśli technologia jest już rozwinięta to ryzyko jest mniejsze, lepsze jest tez zrozumienie jakiś odchyleń próbek biometrycznych
8. **Typ (kontaktowe lub bezdotykowe), rozmiar ("kieszonkowe" lub dedykowana stacja), koszt czujników** powiązanych z tą biometrią
9. **Wielość szablonu**
   >Ile i jak będzie zajmował miejsce wzorzec biometryczny? Ma to szczególne znaczenie na kartach inteligentnych, np. kartach ID czy debetowych. Często da się przyciąć szablon w sposób taki, żeby znajdowały się tam jedynie te dane, które są nam potrzebne
10. **Skalowalność**
    >Liczność populacji, na której możemy zastosować dane rozwiązanie biometryczne przy zachowaniu pożądanych stóp błędów. Skalowalna biometryka to taka, która będzie unikalna dla zdecydowanej większości populacji.

![[Pasted image 20260128134839.png]]
###### Wyróżnia się trzy poziomy/obszary, na których można oceniać systemy:
- technologia (robi się w laboratorium, na symulacjach, testach, badaniach); są to jednak warunki niepodobne do rzeczywistych, są obciążone wyidealizowanymi warunkami
- scenariusz
- eksploatacja

Szybki przykład: biometria palca, wynik technologiczny może być dobry 10^(-6), ale w scenariuszu access control w piekarni czujniki będą pokryte mąką i czytniki nie będą działały. Dobra technologia, ale nie dostosowana do scenariusza i warunków eksploatacyjnych. 

#### Proces oceny: technologia
Udostępnia się bazę danych uczących oraz pewien czas na ustawienie parametrów systemu. Potem dostarcza się bazę danych testowych $Q$. Dane mają być reprezentatywne - pochodzą z rozkładu danych rzeczywistych. Należy rozważyć wiele cech, takich jak przy np. twarzy: ich morfologia, rasa, przystosowanie biologiczne. 

Zbiór danych należy podzielić na: zbiór uczący, walidujący (opcjonalnie) i testowy. Zbiór testowy sprawdza, czy system działa prawidłowo. Można np. po prostu pokroić oryginalny zbiór.

![[Pasted image 20260128142305.png]]

Dostęp do informacji jest ogólnie trudny - zwłaszcza jeśli chcemy dobrą reprezentację i jakość. Pierwszym krokiem jest kupienie lub uzyskanie danych, bo publiczne zbiory są słabe. Druga rzecz to etykietowanie danych. Może być problem jeśli technologia przeuczy się, dokonane zostaje nadanie niepotrzebnej wagi, będącej ostatecznie jedynie wycinkiem rzeczywistości. 

#### Podział systemów
1. **Systemy fizycznej kontroli dostępu i uwierzytelnienia dla małych grup użytkowników**
   >Kontrola dostępu i handel akcjami - możliwe duże straty finansowe, względnie mało użytkowników
2. **Systemy fizycznej kontroli dostępu dla dużych grup użytkowników**
   >Przesiewanie na lotnisku - dużo użytkowników i zagrożenie życia. 
3. **Systemy autoryzacji operacji dla dużych grup użytkowników**
   >Operacje kartowe - bardzo dużo użytkowników, ograniczony koszt strat do limitu transakcynego.

#### Diagramy Zephyr
Wizualizacja porównawcza biometryk, gdzie cztery czynniki są porozkładane po osiach - np. wysiłek, inwazyjność, dokładność i koszt. Zazwyczaj wybiera się bardziej konkretne kryteria.

![[Pasted image 20260128142816.png]]