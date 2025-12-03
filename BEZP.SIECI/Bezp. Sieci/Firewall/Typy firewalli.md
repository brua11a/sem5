#### Stateless firewall
Filtruje ruch na podstawie informacji warstwy 3 i 4 - czyli adres IP oraz port. Tworzy to prostą tabelę sprawdzaną przed wykonaniem przesłaniem ruchu. Stateless firewall jest szybki, prosty i lekki ale podatny na IP spoofing oraz pojawiają się z nim problemy przy nietypowych rozwiązaniach, np. dnamic port negotiation.

#### Stateful firewall
Najczęściej wykorzystywany. Poza warstwą transportową i sieciową, brana po uwagę jest jeszcze warstwa sesji, gdzie decyzje są wykonywane na podstawie stanu. 
[[Rozszerzone ACL]] to prosta implementacja stateful firewalla dzięki [[established TCP]].
Często jest używany jako główny sposób ochrony przed niepożądanym ruchem ze względu na ich moc, odporność na spoofing i lepsze logi. Problemem jest jednak to, że nie cały ruch sieciowy jest stateful, zatem stateful firewall daje niewiele.  

#### Application Gateway firewall
Zwany też Proxy firewallem. Dodatkowo przy filtrowaniu ruchu jest brana pod uwagę warstwa 7 - aplikacji. Polega na SDN (Software Defined Networking). Gdy klient próbuje łączyć się usługą, proxy w jego imieniu "przekazuje" jego ruch do serwera.

#### Next-generation Firewall
Dodatkowe fancy feature