Jest to open source Network [[IPS]] wykonujący [[Alarmy Snort|analizę ruchu sieciowego]] na żywo, generując przy ty alerty gdy zostaną wykryte anomalie. Pozwala na analizę protokołów, przeszukiwanie treści i wykrywanie powszechnych ataków takich jak buffer overflow. 

Na routerach Cisco da się uruchomić Snort Engine jako _virtual service container_ - czyli odizolowaną maszynę/kontener działający na routerze, w której wykonywane są operacje IPS. Współpracuje z innymi mechanizmami zabezpieczeń, takimi jak [[ZPF|ZPF firewall]] czy VPN. 

![[Pasted image 20251127160509.png]]

**Jak każdy IPS, Snort składa się z:**
1. **Snort Engine** - IPS detection and enforcement engine
2. **Snort rule software subscription for signature updates** - odpowiednik IPS attack signatures package
   >Gdzie paczka z [[Sygnatury|sygnaturami]] zależy od naszego tieru subskrypcji. Jest **Community Rule Set** i **Subscriber Rule Set**, gdzie ten płatny jest ofc lepszy.
   
#### Działanie Snorta
Może on działać jako [[Wykrywanie ataków|IDS]], gdzie będzie ataki jedynie wykrywał:
- Alert - **wygeneruj alarm** według określonej metody
- Log - stwórz log dotyczący pakietu
- Pass - przepuść/zignoruj pakiet
Ale może też działać jako [[IPS]], gdzie poza wszystkimi feature'ami IDS może dodatkowo:
- Drop - zablokuj i loguj pakiet
- Reject - zablokuj i loguj pakiet, dodatkowo wyślij TCP reset albo ICMP port unreachable
- Sdrop - zablokuj pakiet ale go NIE loguj

Jako część inline urządzenia, do kontenera z działającym Snort jest przekazywany ruch sieciowy przechodzący przez router, który zostaje oceniany. Do komunikacji pomiędzy sprzętem a Snortem służy VPG (Virtual Port Group), gdzie sam Snort potrzebuje dwóch takich interfejsów:
1. Management interface - wymaga routowalnego adresu IP, służy do logów i pobierania nowych [[Sygnatury|sygnatur]]
2. Data interface - do przekazywania danych między routerem a Snortem

![[Pasted image 20251127162031.png]]