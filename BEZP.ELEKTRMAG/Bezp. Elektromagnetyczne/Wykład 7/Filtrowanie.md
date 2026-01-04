Jest to najczęściej stosowany sposób na tłumienie zaburzeń występujących w sieci elektrycznej. Poprawnie dobrany i zainstalowany filtr sygnałów wspólnych nie dopuszcza sygnałów z sieci do urządzenia, jak również chroni sieć przed tego typu sygnałami, gdy źródłem zaburzeń jest urządzenie. Filtry zwiększają także odporność na zakłócenia w obwodach zasilania, sygnałowych i danych. 

![[Pasted image 20260103230913.png]]

Zazwyczaj filtr składa się z [[Właściwości elementów L, C, R|kondensatorów, dławików i rezystorów]]. Jest to układ liniowy póki rdzenie dławików się nie nasycą. Filtry eliminują niepotrzebne zakresy sygnałów elektrycznych.

**Na podstawie charakterystyki częstotliwościowej filtry są klasyfikowane jako:**
- dolnoprzepustowe
- górnoprzepustowe
- pasmowoprzepustowe
- pasmowozaporowe

**Skuteczność filtrowania jest nazywana tłumiennością wtrąceniową.** Określa to jak mocno sygnał po drodze zostaje wytrącony. Jest to stosunek poziomu sygnału oryginalnego, bez filtra w stosunku do sygnału po przefiltrowaniu.

![[Pasted image 20260103175809.png]]

![[Pasted image 20260103180038.png]]

![[Pasted image 20260103180058.png]]

## Claude wysryw

# Szczegółowy opis układów filtrowania EMC

## 1. IMPEDANCJA LINII ZASILANIA - NISKA

### Układ 1: Kondensator szeregowy z rezystorem + kondensator równoległy

**Budowa:** Rezystor i kondensator połączone szeregowo w linii, dodatkowo kondensator równoległy do masy po stronie wejściowej.

**Dlaczego impedancja jest niska?**

- Linia zasilania ma małą rezystancję wewnętrzną (grube przewody, krótkie połączenia)
- Źródło może dostarczyć duże prądy bez znacznych spadków napięcia
- Niska impedancja = łatwa droga dla prądów zakłócających

**Jak działa filtr?**

- Kondensator równoległy (przy wejściu) odprowadza wysokoczęstotliwościowe zakłócenia bezpośrednio do masy
- Rezystor szeregowy tłumi przepływ zakłóceń
- Drugi kondensator dodatkowo oczyszcza sygnał

### Układ 2: Prosty kondensator równoległy

**Budowa:** Pojedynczy kondensator podłączony między linię a masę.

**Zastosowanie przy niskiej impedancji źródła:**

- Źródło o niskiej impedancji może "wytrzymać" obciążenie kondensatorem
- Kondensator tworzy ścieżkę niskiej impedancji dla wysokich częstotliwości
- Zakłócenia HF są zwierane do masy zamiast iść dalej w obwód

**Dlaczego to działa?**

- Impedancja kondensatora: Z = 1/(2πfC)
- Dla wysokich częstotliwości (zakłócenia) impedancja jest bardzo mała
- Zakłócenia "preferują" drogę przez kondensator zamiast dalej w obwód

### Układ 3: Rezystor z dwoma kondensatorami do masy

**Budowa:** Rezystor w linii, kondensatory po obu jego stronach do masy.

**Mechanizm działania:**

- Pierwszy kondensator odprowadza zakłócenia ze źródła
- Rezystor stanowi barierę dla przepływu zakłóceń
- Drugi kondensator "doczyszcza" sygnał po stronie wyjściowej
- Tworzy się filtr dolnoprzepustowy typu π (pi)

---

## 2. IMPEDANCJA LINII ZASILANIA - WYSOKA

### Układ 1: Kondensator równoległy

**Budowa:** Prosty kondensator do masy.

**Dlaczego impedancja jest wysoka?**

- Długie przewody zasilające
- Cienkie przewody
- Duża rezystancja wewnętrzna źródła
- Źródło nie może dostarczyć dużych prądów

**Problem z wysoką impedancją źródła:**

- Zakłócenia łatwiej "wchodzą" do układu
- Mniejsza zdolność do pochłaniania prądów zakłócających

**Rozwiązanie:**

- Kondensator tworzy lokalny rezerwuar energii
- Filtruje zakłócenia wysokoczęstotliwościowe
- Stabilizuje napięcie zasilania

### Układ 2: Kondensator z rezystorem (filtr RC)

**Budowa:** Rezystor szeregowo w linii, kondensator równolegle do masy.

**Działanie:**

- Rezystor ogranicza prądy zakłócające
- Wraz z kondensatorem tworzy filtr dolnoprzepustowy
- Częstotliwość graniczna: f = 1/(2πRC)
- Zakłócenia HF są tłumione, DC przechodzi swobodnie

---

## 3. IMPEDANCJA LINII ZASILANIA - WYSOKA (NIEZNANA)

### Rezystor z kondensatorami po obu stronach

**Budowa:** Rezystor w linii, kondensatory do masy przed i po rezystorze.

**Dlaczego "nieznana"?**

- Nie znamy dokładnej impedancji źródła
- Może się zmieniać w zależności od warunków pracy
- Chcemy zabezpieczyć się na różne scenariusze

**Zalety tego rozwiązania:**

- Uniwersalne - działa przy różnych impedancjach źródła
- Pierwszy kondensator stabilizuje napięcie wejściowe
- Rezystor izoluje źródło od obciążenia pod względem HF
- Drugi kondensator zapewnia dodatkowe filtrowanie

---

## 4. IMPEDANCJA URZĄDZENIA ZASILANEGO - NISKA

### Układ 1: Rezystor szeregowy + kondensator równoległy

**Budowa:** Rezystor w linii zasilającej, kondensator do masy po stronie obciążenia.

**Dlaczego impedancja odbiornika jest niska?**

- Urządzenie pobiera duże prądy
- Małe rezystancje wejściowe
- Np. silniki, przekształtniki mocy, urządzenia cyfrowe z dużą liczbą bramek

**Problem:**

- Urządzenia o niskiej impedancji generują dużo zakłóceń
- Szybkie zmiany prądu pobieranego (dI/dt)
- Zakłócenia mogą wracać do linii zasilania

**Jak filtr pomaga?**

- Rezystor tłumi zakłócenia wychodzące z urządzenia
- Kondensator lokalnie dostarcza prąd przy szybkich zmianach
- Zapobiega propagacji zakłóceń do linii zasilania

### Układ 2: Dwa rezystory + kondensator pośrodku

**Budowa:** Dwa rezystory szeregowo, kondensator między nimi do masy.

**Zaawansowane filtrowanie:**

- Pierwszy rezystor tłumi zakłócenia przychodzące
- Kondensator odprowadza je do masy
- Drugi rezystor dodatkowo izoluje urządzenie
- Lepsze tłumienie niż prosty układ RC

---

## 5. IMPEDANCJA URZĄDZENIA ZASILANEGO - WYSOKA

### Pojedynczy kondensator równoległy

**Budowa:** Kondensator między linią zasilania a masą.

**Dlaczego impedancja odbiornika jest wysoka?**

- Urządzenie pobiera małe prądy
- Duża rezystancja wejściowa
- Np. wzmacniacze operacyjne, układy analogowe, czujniki

**Charakterystyka:**

- Urządzenia wysokoimpedancyjne są wrażliwe na zakłócenia
- Małe prądy zakłócające mogą powodować duże zmiany napięcia (V = I × R)
- Potrzebują czystego, stabilnego zasilania

**Rola kondensatora:**

- Filtruje zakłócenia HF na wejściu urządzenia
- Stabilizuje napięcie zasilania lokalnie
- Zapewnia rezerwuar energii dla krótkotrwałych szczytów prądu
- Działa jak lokalna "bateria" dla wysokich częstotliwości

---

## 6. IMPEDANCJA URZĄDZENIA ZASILANEGO - WYSOKA (NIEZNANA)

### Dwa rezystory + kondensator

**Budowa:** Identyczna jak w przypadku niskiej impedancji - dwa rezystory szeregowo, kondensator między nimi.

**Dlaczego ta sama topologia?**

- Uniwersalność - nie znamy dokładnej impedancji wejściowej
- Impedancja może się zmieniać w różnych trybach pracy
- Zabezpieczenie na różne scenariusze

**Przewaga tego układu:**

- Pierwszy rezystor izoluje od linii zasilania
- Kondensator zapewnia lokalne filtrowanie
- Drugi rezystor chroni wrażliwe wejście urządzenia
- Działa skutecznie zarówno dla wysokich jak i niskich impedancji

---

## PODSUMOWANIE - ZASADY DOBORU

### Impedancja określa:

**NISKA IMPEDANCJA:**

- Duże prądy mogą płynąć swobodnie
- Potrzebne silniejsze tłumienie (więcej elementów)
- Większe kondensatory
- Rezystory do ograniczenia prądów

**WYSOKA IMPEDANCJA:**

- Małe prądy
- Prostsze filtry mogą wystarczyć
- Kluczowa stabilizacja napięcia
- Ochrona przed zakłóceniami napięciowymi

**NIEZNANA IMPEDANCJA:**

- Zastosowanie bardziej złożonych, uniwersalnych struktur
- Kombinacja elementów zabezpieczających różne przypadki
- Filtr π (pi) jako najbezpieczniejsze rozwiązanie
