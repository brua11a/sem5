Jedną z dróg propagacji i sprzęgania się zaburzeń są wszelkie linie zasilające, sygnałowe i interfejsowe umożliwiające przenoszenie się energii zaburzeń do urządzenia bądź systemu wraz z sygnałami użytecznymi.

![[Pasted image 20251229140414.png]]

#### Elementy układu
- **EUT** (Equipment Under Test) - urządzenie testowane
- **Kabel sieciowy** - przewody fazowe L, neutralny N oraz ochronny PE
- **Ziemia odniesienia** - płaszczyzna referencyjna dla pomiarów
- **Rezystor 50Ω** - element pomiarowy/dopasowujący (LISN - Line Impedance Stabilization Network)
#### Napięcia różnicowe/symetryczne (DM - Differential Mode)
**Charakterystyka:**
- Napięcia między przewodami fazowymi: $U_{DM}$
- Prądy różnicowe: $I_{DM}$ (przepływające w przeciwnych kierunkach między przewodami)
- Występują między przewodami roboczymi (L-N, L-L)
**Właściwości:**
- Zaburzenia symetryczne wnikają bardzo słabo, jeśli przewody leżą blisko siebie
- Gdy przewody są dobrze zrównoważone i odsunięte od przewodów zakłócających, zaburzenia wnikające symetryczne można zignorować
- **Bezpośrednio zakłócają sygnał użyteczny** - nie kasują się w odbiorniku różnicowym

![[Pasted image 20251229141251.png]]

#### Napięcia wspólne/asymetryczne (CM - Common Mode)
**Charakterystyka:**
- Napięcia względem ziemi: $U_{CM}$
- Prądy wspólne: $I_{CM}$ (przepływające w tym samym kierunku)
- Występują między wszystkimi przewodami a ziemią odniesienia
**Właściwości:**
- Przepływają przez pojemności pasożytnicze do ziemi
- W idealnym układzie różnicowym kasują się w odbiorniku
- Tworzą ścieżkę powrotu przez uziemienie ($-2I_{CM}$)

#### Konwersja zakłóceń CM → DM

![[Pasted image 20251229142439.png]]

Sygnał zewnętrzny (zakłócenie wspólne/asymetryczne) **nie jest problemem dopóty, dopóki nie zmieni się w zaburzenie symetryczne (różnicowe)**.

Zakłócenia asymetryczne zamieniają się na symetryczne przez **niezrównoważone połączenie**, w którym pojawia się:
- **Asymetria w liniach przesyłających sygnał** (różne impedancje przewodów)
- **Niesymetria obciążenia na końcu linii** (różne impedancje wejściowe)
- **Niezrównoważenie połączenia** (różne pojemności do ziemi)

#### Mechanizm konwersji
Na obrazku widzimy, że **prądy wspólne $I_{CM}$** przepływające przez impedancje pasożytnicze (pojemności EUT do ziemi) mogą powodować różne spadki napięć na przewodach. 

Gdy impedancje tych ścieżek są różne, zakłócenie wspólne **konwertuje się na zakłócenie różnicowe**, które już bezpośrednio zakłóca sygnał użyteczny.

**Przykład konwersji:**
- Zakłócenie CM: oba przewody +0,1V względem ziemi → kasuje się w odbiorniku ✓
- Niesymetria układu: przewód 1 widzi +0,15V, przewód 2 widzi +0,05V
- Powstaje składowa DM: 0,15V - 0,05V = **0,1V zakłócenia różnicowego** ✗

#### Znaczenie w kontekście EMC
1. **Zaburzenia DM** - bezpośrednio szkodliwe, łatwiejsze do tłumienia (filtry szeregowe, dławiki różnicowe)
2. **Zaburzenia CM** - potencjalnie szkodliwe (konwertują się na DM), trudniejsze do eliminacji, wymagają filtrów z kondensatorami Y i dławików wspólnych
3. **Symetria układu** - kluczowa dla minimalizacji konwersji CM→DM
4. **LISN (50Ω)** - standaryzacja impedancji sieci zasilającej dla pomiarów EMI