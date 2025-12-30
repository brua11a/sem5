#### Systemy krótkozasięgowe
Systemy krótkozasięgowe pracują w pasmach takich, jak na slajdzie. Są to po części pasma **ISM** (Industrial, Scientific, Medical) - pasma przemysłowe, naukowe i medyczne, nielicencjonowane. Reszta to **U-NII** (Unlicensed National Information Infrastructure), które jest podzielone an zakresy i ograniczone przez DFS.
1. RFID (13553 kHz, błąd na slajdzie)
2. IoT (LPWAN, SRD)
3. WLAN, Bluetooth, ZigBee

![[Pasted image 20251225154742.png]]

Dwa pierwsze pasma są dość wąskie (13-14kHz, 3MHz), zatem te systemy nie będą bardzo wydajne. Wynika to z twierdzenia Shannona - "jeśli mamy kanał o pewnej szerokości pasma to można na tego podstawie policzyć z jaką maksymalnie szybkością można wysyłać bezbłędnie informacje". 

W pozostałych pasmo ma szerokość 100MHz lub 150MHz - w tych systemach jest "tłoczno", dlatego dla dużych systemów lepiej wybrać pasmo 5GHz. Są wyższe pasma stworzone "na zaś" i raczej nie są używane.
#### Maska promieniowania
Każdy system ma maskę promieniowania - kształt widma sygnału. Kanał fizyczny nie może przekroczyć tego widma w żadnym punkcie. "Widmo nie może być szersze niż ten 1MHz, ewentualnie na poziomie -20dB lub -40dB". Jeśli karta radiowa nie spełnia wymagania to nie może wyjść na rynek.
![[Pasted image 20251225200122.png]]