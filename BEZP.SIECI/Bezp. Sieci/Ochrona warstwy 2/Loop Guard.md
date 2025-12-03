**Loop Guard** chroni przed powstaniem pętli L2 w sytuacji, gdy łącze staje się jednokierunkowe.  
W STP porty designated wysyłają BPDUs, a porty niedesignated odbierają je.  
Jeśli port, który powinien odbierać BPDU nagle przestaje je dostawać, STP błędnie uzna, że może przejść do forwardingu i tworzy pętlę.

Port z włączonym Loop Guardem, który przestanie otrzymywać BPDUs, nie przejdzie do forwardingu. Zamiast tego przechodzi w loop-inconsistent (blokujący), chroniąc sieć przed pętlą.

![[Pasted image 20251129213927.png]]

#### `S1(config-if)# spanning-tree guard loop`