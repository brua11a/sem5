**Root Guard** służy do upewnienia się, że **nieodpowiedni switch nigdy nie zostanie root bridge**. Ogranicza to które porty mogą brać udział w negocjacji wyboru root bridge. Najlepiej stosować go na portach prowadzących do switchy, które nie powinny zostać rootem - tutaj na obrazku porty F0/1 na D1 i D2 prowadzą do S1 bo S1 ma nigdy nie zostać rootem.

Jeśli port z włączonym Root Guardem **otrzyma BPDU lepsze** (superior) od aktualnego,  
to STP uznaje, że ktoś próbuje zostać rootem  i taki port przechodzi do stanu **root-inconsistent** (odpowiednik stanu _listening_, brak przekazywania ruchu).

Port automatycznie wraca do pracy, gdy „złośliwe” albo niepożądane BPDU przestaną nadchodzić.

![[Pasted image 20251129213536.png]]

#### `S1(config-if)# spanning-tree guard root`