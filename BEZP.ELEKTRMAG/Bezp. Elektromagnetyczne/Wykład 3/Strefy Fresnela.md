# Claude wysryw

## Podstawy propagacji

### Model fizyczny

Rozważamy sytuację, w której fala elektromagnetyczna rozprzestrzenia się między dwiema antenami nad płaską, przewodzącą powierzchnią ziemi. W rzeczywistości do punktu odbioru dociera:

- **Fala bezpośrednia** - propagująca się wprost od nadajnika
- **Fala odbita** - odbita od powierzchni ziemi

Interferencja (nakładanie się) tych dwóch fal determinuje wypadkowe natężenie pola w punkcie odbioru.

### Natężenie pola elektrycznego

Dla odległości **d** znacznie większej od wysokości anten ($h_t$ - nadawcza, $h_r$ - odbiorcza), natężenie pola wypadkowego wynosi:

$|E| = \frac{2\sqrt{60P_tG_t}}{d} \sin\left(\frac{2\pi h_t h_r}{\lambda d}\right) \quad [V/m]$

**Parametry:**

- $P_t$ - moc nadajnika [W]
- $G_t$ - zysk anteny nadawczej
- $d$ - odległość między antenami [m]
- $h_t, h_r$ - wysokości anten [m]
- $\lambda$ - długość fali [m]

**Kluczowa obserwacja:** Funkcja sinus we wzorze powoduje, że natężenie pola zmienia się wraz z wysokością anten - mogą wystąpić maksima i minima sygnału (zaniki interferencyjne).

### Minimalne wysokości zawieszenia anten

Aby uniknąć nadmiernych zaniku sygnału, anteny muszą być zawieszone na odpowiedniej wysokości. Minimalna wysokość zależy od:

- Częstotliwości (długości fali λ)
- Właściwości gruntu (przenikalność ε, przewodność σ)
- Polaryzacji fali

**Polaryzacja pionowa:** wymagana większa wysokość $h_{min} > \frac{5\lambda}{\pi} \sqrt{\frac{\varepsilon^2 + (60\lambda\sigma)^2}{(\varepsilon-1)^2 + (60\lambda\sigma)^2}}$

**Polaryzacja pozioma:** wymagana mniejsza wysokość $h_{min} > \frac{5\lambda}{\pi} \frac{1}{\sqrt[4]{(\varepsilon-1)^2 + (60\lambda\sigma)^2}}$

---

## Moc odbierana

Ponieważ moc jest proporcjonalna do kwadratu natężenia pola ($P \propto E^2$), moc odbierana przez antenę odbiorczą wynosi:

$P_r = 4P_t G_t G_r \left(\frac{\lambda}{4\pi d}\right)^2 \sin^2\left(\frac{2\pi h_t h_r}{\lambda d}\right) \quad [W]$

gdzie $G_r$ to zysk anteny odbiorczej.

**Wnioski praktyczne:**

- Moc odbierana maleje z kwadratem odległości
- Zależy od iloczynu wysokości obu anten
- Im wyższa częstotliwość (mniejsze λ), tym szybszy zanik z odległością

---

## Strefy Fresnela - koncepcja

### Problem podstawowy

Pytanie: **Jaki obszar przestrzeni między nadajnikiem a odbiornikiem ma rzeczywisty wpływ na propagację fali?**

Intuicyjnie moglibyśmy myśleć, że fala "leci" prostą linią między antenami. Jednak z zasady Huygensa-Fresnela wynika, że każdy punkt przestrzeni między źródłem a odbiornikiem działa jak wtórne źródło fali.

### Zasada Huygensa-Fresnela

**Pole w punkcie odbioru B** jest sumą pól pochodzących od wszystkich elementarnych źródeł rozmieszczonych na powierzchni poprzecznej między źródłem A a punktem B.

Matematycznie pole w punkcie B wyraża się całką:

$E(B) = -\frac{j}{\lambda} \int_{S_0} E_0 \frac{e^{-jk(\rho+r)}}{\rho r} (1_r, 1_s) dS$

gdzie:

- $\rho$ - odległość od źródła A do elementu powierzchni
- $r$ - odległość od elementu powierzchni do punktu B
- $k = 2\pi/\lambda$ - liczba falowa

**Kluczowa obserwacja:** Każdy element powierzchni wnosi wkład o określonej amplitudzie i **fazie**, która zależy od długości drogi $(\rho + r)$.

### Definicja stref Fresnela

Przestrzeń między antenami dzielimy na **pierścieniowe strefy koncentryczne** (strefy Fresnela) według kryterium różnicy faz.

**N-ta strefa Fresnela** to obszar, dla którego droga fali jest dłuższa o $n\lambda/2$ względem najkrótszej drogi:

$\rho_n + r_n = \rho_0 + r_0 + n\frac{\lambda}{2}$

**Interpretacja geometryczna:** Granice stref Fresnela to **elipsoidy obrotowe** z ogniskami w punktach A (nadajnik) i B (odbiornik).

---

## Działanie stref Fresnela

### Interferencja między strefami

Kluczowe odkrycie: pola pochodzące z **kolejnych stref są w przeciwfazie** (różnica 180°):

$E(B) = E_1 - E_2 + E_3 - E_4 + E_5 - ...$

**Dlaczego?** Każda kolejna strefa ma drogę dłuższą o λ/2, co daje różnicę fazy π (180°).

### Uproszczenie - przybliżenie

Można wykazać, że każda strefa ma amplitudę zbliżoną do średniej z sąsiednich stref. Po matematycznym przekształceniu szeregu otrzymujemy:

$E(B) \approx \frac{E_1}{2}$

**Praktyczny wniosek:** Pole w punkcie odbioru jest w przybliżeniu równe **połowie pola z pierwszej strefy Fresnela**. Dokładniej:

$\frac{E_1}{2} < E(B) < E_1$

### Znaczenie pierwszej strefy Fresnela

**Wniosek praktyczny dla planowania łączy radiowych:**

✅ **Pierwsza strefa Fresnela powinna być wolna od przeszkód** - zapewnia to optymalną propagację

⚠️ Przeszkody w pierwszej strefie (budynki, wzgórza, drzewa) powodują:

- Tłumienie sygnału
- Dodatkowe odbicia i dyfrakcję
- Pogorszenie jakości łącza

❌ Strefy wyższych rzędów (2, 3, 4...) mają znacznie mniejszy wpływ na sygnał

---

## Promień stref Fresnela

### Wzór na promień n-tej strefy

$R_n = \sqrt{\frac{n\lambda\rho_0 r_0}{\rho_0 + r_0}}$

gdzie:

- $\rho_0$ - odległość od nadajnika do płaszczyzny przekroju
- $r_0$ - odległość od płaszczyzny przekroju do odbiornika
- $n$ - numer strefy (1, 2, 3...)

**Maksymalny promień** występuje dla $\rho_0 = r_0$, czyli w połowie drogi między antenami.

### Promień pierwszej strefy Fresnela

Najważniejsza jest **pierwsza strefa** (n=1). W połowie drogi między antenami ($\rho_0 = r_0 = d/2$) jej promień wynosi:

$R_1 = \sqrt{\frac{\lambda d}{4}}$

**Przykład praktyczny:**

- Częstotliwość: 2.4 GHz → λ = 12.5 cm
- Odległość: d = 1 km = 1000 m
- Promień pierwszej strefy: $R_1 = \sqrt{0.125 \times 1000 / 4} \approx 5.6$ m

**Interpretacja:** W połowie trasy między antenami oddalonymi o 1 km powinien być wolny obszar o promieniu co najmniej 5-6 metrów.

### Zależność od częstotliwości

**Kluczowa obserwacja:**

$R_1 \propto \sqrt{\lambda} \propto \sqrt{\frac{1}{f}}$

- **Niższe częstotliwości** (większe λ) → większe strefy Fresnela → wymagają większego wolnego obszaru
- **Wyższe częstotliwości** (mniejsze λ) → mniejsze strefy → "węższa wiązka", fala bardziej zbliżona do linii prostej
- Dla λ → 0 (f → ∞): strefa Fresnela "zbiega" do linii prostej (optyka geometryczna)

### Powierzchnia stref

Interesujący fakt: **wszystkie strefy Fresnela mają taką samą powierzchnię** przekroju poprzecznego:

$S = \frac{\pi^2\lambda\rho_0 r_0}{\rho_0 + r_0}$

Pomimo że strefa 2, 3, 4... mają większy promień zewnętrzny, ich powierzchnia (pierścień między kolejnymi elipsoidami) jest stała.

---

## Podsumowanie praktyczne

### Kluczowe wnioski dla planowania łączy

1. **Wolna droga nie wystarczy** - musi być wolny obszar wokół linii wzroku (pierwsza strefa Fresnela)
    
2. **Im wyższa częstotliwość, tym mniejsze wymagania przestrzenne** - łatwiej o wolną pierwszą strefę
    
3. **Optymalna lokalizacja anten** - tak wysoko, aby pierwsza strefa była wolna od przeszkód
    
4. **Kryteria bezpieczeństwa:**
    
    - Minimum: 60% pierwszej strefy Fresnela wolne (R₁ × 0.6)
    - Zalecane: 80-100% pierwszej strefy wolne
5. **Zależność od geometrii:**
    
    - Największy promień w połowie drogi
    - Blisko anten strefa się zwęża

### Praktyczne zastosowania

- **Łącza radiowe punkt-punkt** - planowanie wysokości masztów
- **WiFi dalekiego zasięgu** - unikanie drzew i budynków
- **Radiolokacja** - analiza zasięgu nad różnym terenem
- **Telekomunikacja mobilna** - optymalizacja lokalizacji stacji bazowych