**LEMP (*Lightning EMP*)** to impuls EM powstały podczas wyładowania piorunowego. 

#### Powstawanie LEMP
1. Gromadzą się ładunki w dolnej części chmury na skutek zderzeń kryształków lodu znajdujących się wewnątrz chmury.
   - napięcie zapłonu: 1MV
   - czas wytwarzania: 30min
   >
   >![[Pasted image 20260103164729.png]]
1. Lód i deszcz w chmurze burzowej zderzają się ze sobą i tworzą ładunki elektryczne. 
2. **Spadające cząstki zyskują ładunek ujemny, zaś te unoszące się - dodatni.**
3. Ładunki ujemne gromadzą się w dolnej części chmury, dodatnie w górnej. Nagromadzenie ładunków ujemnych w dolnej części chmury indukuje ładunki dodatnie na powierzchni ziemi. 
4. Gdy różnica potencjałów między chmurą a Ziemią osiąga napięcie przebicia (około 1 MV), następuje wyładowanie - z chmury do Ziemi a potem w drugą stronę.

## Zjawiska związane z LEMP / surge

#### Zjawisko 1 - piorunowe stany przejściowe
Są one związane m.in. z bezpośrednim uderzeniem pioruna o obwód zewnętrzny znajdujący się na wolnym powietrzu **(1)**. Wywołuje to duże prądy, które wytwarzają wysokie napięcia poprzez np. przepływ prądu przez rezystancję Ziemi.

Mogą one dotyczyć również pośrednich uderzeń pioruna **(2)**, wyładowania między chmurami **(3)**, do pobliskich obiektów. Tworzy to pole EM, które indukuje napięcia i prądy w przewodach.

![[Pasted image 20260103171021.png]]

![[Pasted image 20260103171126.png]]

##### Claude wysryw: Zagrożenia stwarzane przez wyładowania atmosferyczne

Rysunek przedstawia przykładowe drogi oddziaływania pioruna na systemy elektroniczne i infrastrukturę:

**Bezpośrednie uderzenie pioruna**

> Piorun może uderzyć bezpośrednio w budynek, antenę, linie energetyczne (15 kV) lub ziemię w pobliżu obiektu. Bezpośrednie trafienie przenosi ogromne energie i prądy (dziesiątki do setek kiloamperów), które mogą zniszczyć urządzenia, wywołać pożar lub uszkodzić konstrukcję.

**Sprzężenie elektroenergetyczne**

> Prądy piorunowe przepływające przez instalację odgromową, uziom lub sieć elektroenergetyczną indukują przepięcia w obwodach zasilających. Przepięcia te penetrują do wnętrza budynku poprzez instalację elektryczną i mogą uszkodzić podłączone urządzenia elektroniczne, mimo zastosowania klimatyzacji i połączeń wewnątrz systemu.

**Sprzężenie przez linie telekomunikacyjne i transmisji danych**

> Pole elektromagnetyczne wyładowania indukuje napięcia i prądy w długich przewodach (liniach telekomunikacyjnych, transmisji danych). Te przepięcia przedostają się do systemu elektronicznego, zagrażając czułym elementom elektroniki.

**Sprzężenie przez antenę**

> Impulsy elektromagnetyczne LEMP mogą być odbierane przez anteny systemów komunikacyjnych, wprowadzając destrukcyjne przepięcia bezpośrednio do odbiorników i nadajników.

**Uziom jako droga rozpływu prądu**

> Prąd piorunowy rozpraszany przez system uziemienia podnosi potencjał ziemi lokalnie, co może prowadzić do różnic potencjałów między różnymi punktami uziemienia i uszkodzenia urządzeń poprzez przepływ prądów wyrównawczych.


#### Zjawisko 2 - łączeniowe stany przejściowe
Udary powstają również podczas podłączenia zasilania, np. baterii konsensatorów. Podczas włączania lub wyłączania dużych obciążeń pojemnościowych powstają krótkotrwałe przepięcia i prądy udarowe. Niewielkie wyładowania pojawiają się również przy podłączaniu mniej znaczących elementów, a także przy zmianie obciążenia w sieci rozdzielczej. Dodatkowo: obwody rezonansowe, uziemienie instalacji.

Na kształt i amplitudę impulsów powstałych w wyniku wcześniej opisanych zjawisk wpływa przede wszystkim długość linii zasilających/sygnałowych/telekomunikacyjnych jak i od ich rodzaju i umieszczenia względem Ziemi. Przy wystarczająco długiej linii impuls mają charakter unipolarny.

**[[Parametry kształtu impulsu surge|Przyjęto dwa typy impulsów:]]**
1. **$1,2/50\;\mu s$ - $8/20\;\mu s$**
2. **$10/700\;\mu s$ - $5/320\;\mu s$**

![[Pasted image 20260103173301.png]]