# Claude wysryw
# Metoda alternatywna – pomiar mocy (MDS)

Zamiast pola możemy wyznaczyć **moc promieniowaną**.

**Metoda MDS** (Metoda Detekcji Składowej, ang. _Magnitude Detection Substitute_) – **metoda cęgi absorpcyjnej** – użyteczna w przypadku urządzeń promieniujących przez przewody.

Nazwa metody pochodzi od nazwiska twórcy: **Meyer de Stadelhofen**.

---

## Zasada działania metody MDS

### Układ pomiarowy
Układ zastępczy źródła zakłóceń składa się z:
- Napięcia źródłowego **E_z**
- Impedancji wewnętrznej źródła **Z_z**
- Przewodu sieciowego rozciągniętego z dołączoną impedancją obciążenia **Z_0**

![[Pasted image 20251228233143.png]]
### Istota metody
Metoda polega na pomiarze **natężenia prądu zaburzeń** płynącego przez **znaną impedancję obciążenia** (Z_0 ≈ R_0), którą można przedstawić w postaci pokazanej na schemacie układu pomiarowego.

---

## Zastosowanie metody MDS

### Układ dopasowujący
Za układ dopasowujący stosuje się odcinek linii dołączonej do badanego obiektu o odpowiednio dobranej długości. 

Jeżeli **impedancję obciążającą Z0** umieścimy w miejscu występowania pierwszego maksimum fali stojącej, jaka powstaje w linii dołączonej do badanego obiektu, to następuje **kompensacja składowej urojonej impedancji**.

### Parametry techniczne
W praktycznej realizacji przedstawionej metody impedancje obciążenia:
- **Z_0 ≈ R_0 ≈ 200Ω** stanowią specjalne **cęgi absorpcyjne**
- Moc dysponowana jest z dokładnością do **2dB** równa mocy zaabsorbowanej przez cęgi
- Metoda stosowana dla urządzeń, których składowa rzeczywista impedancji zaburzeń mieści się w granicach **50-2000 Ω**

---

## Cęgi absorpcyjne

### Definicja
**Cęgi absorpcyjne** to transformator prądowy z układem dopasowującym w postaci zestawu pierścieni ferrytowych.

### Budowa układu cęgów absorpcyjnych
1. Urządzenie badane
2. Przewód sieciowy badanego urządzenia
3. Transformator prądowy
4. Zestaw 56 pierścieni ferrytowych
5. Zestaw 60 pierścieni ferrytowych
6. Przewód współosiowy do miernika zakłóceń

### Wzór na moc zaburzeń
**P_ZR[dBpW] = K_M[dB] + U_M[dBμV]**

Gdzie:
- **P_ZR** – moc zaburzeń
- **K_M** – współczynnik korekcyjny cęgów
- **U_M** – napięcie zmierzone na mierniku

---

## Zalety metody MDS
- Możliwość pomiaru emisji urządzeń promieniujących przez przewody zasilające
- Relatywnie prosta konstrukcja stanowiska pomiarowego
- Przydatna dla urządzeń o impedancji w zakresie 50-2000 Ω

![[Pasted image 20251228233044.png]]