### Mówimy o:
##### 1. Manipulacji STP
   >*Adnotacja: By doczytać o STP wejdź w kule z CCNA2 moduł 5*
   >
   >![[Pasted image 20251129213402.png]]
   >
   >Polega na manipulowaniu protokołem STP tak, by zmienić most główny w sieci, a wraz z nim całą topologię. Jeśli atakująca maszyna stanie się mostem głównym to będzie przez nią przepływał cały ruch w sieci. Atakujący wymusi ponowne obliczenie drzewa rozpinającego, a także ogłosi się jako most z niskim (czyli wysokim) priorytetem. 
   >
### Jak zapobiec?
##### 1. [[PortFast]] - zapewnia stabilność
##### 2. [[BPDU Guard]] - rzeczywiste zabezpieczenie
##### 3. [[Root Guard]]
##### 4. [[Loop Guard]]

![[Pasted image 20251129213332.png]]