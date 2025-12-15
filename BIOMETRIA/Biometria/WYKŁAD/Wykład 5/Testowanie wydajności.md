**Kryteria:**
- koszt
- stopy błędów
- szybkość obliczeń
- łatwość pobierania
- prywatność łatwość użycia
- dojrzałość - jeśli technologia jest już rozwinięta to ryzyko jest mniejsze, lepsze jest tez zrozumienie jakiś odchyleń próbek biometrycznych
- typ, rozmiar, koszt
- wielość szablonu - ile i jak będzie zajmował miejsce wzorzec biometryczny? ma to szczególne znaczenie na kartach inteligentnych, np. kartach ID czy debetowych, często da się przyciąć szablon w sposób taki, żeby znajdowały się tam jedynie te dane, które są nam potrzebne
- skalowalność - liczność populacji, na której możemy zastosować dane rozwiązanie biometryczne przy zachowaniu pożądanych stóp błędów

###### Wyróżnia się trzy poziomy/obszary, na których można oceniać systemy:
- technologia (robi się w laboratorium, na symulacjach, testach, badaniach); są to jednak warunki niepodobne do rzeczywistych, są obciążone wyidealizowanymi warunkami
- scenariusz
- eksploatacja

Szybki przykład: biometria palca, wynik technologiczny może być dobry 10^(-6), ale w scenariuszu access control w piekarni czujniki będą pokryte mąką i czytniki nie będą działały. Dobra technologia, ale nie dostosowana do scenariusza i warunków eksploatacyjnych. 

#### Proces oceny: technologia
Udostępnia się bazę danych uczących oraz pewien czas na ustawienie parametrów. Dane mają być reprezentatywne - pochodzą z rozkładu danych rzeczywistych. Należy rozważyć wiele cech, takich jak przy np. twarzy: ich morfologia, rasa, przystosowanie biologiczne. 

Zbiór danych należy podzielić: zbiór uczący, walidujący (opcjonalnie) i testowy. Można np. po prostu pokroić oryginalny zbiór. Dostęp do informacji jest ogólnie trudny - zwłaszcza jeśli chcemy dobrą reprezentację i jakość. Pierwszym krokiem jest kupienie lub uzyskanie danych, bo publiczne zbiory są słabe. Druga rzecz to etykietowanie danych. Może być problem jeśli technologia przeuczy się, dokonane zostaje nadanie niepotrzebnej wagi, będącej ostatecznie jedynie wycinkiem rzeczywistości. 

#### Podział systemów
1. Systemy fizycznej kontroli dostępu i uwierzytelnienia dla małych grup użytkowników
2. Systemy fizycznej kontroli dostępu dla dużych grup użytkowników
3. Systemy autoryzacji operacji dla dużych grup użytkowników

#### Diagramy zephyr
Wizualizacja porównawcza, gdzie cztery czynniki są porozkładane po osiach - np. wysiłek, inwazyjność, dokładność i koszt. 