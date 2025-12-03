### Mówimy o:
##### 1. Blokowaniu (zagładzaniu) DHCP
   >Atak typu DoS. Złośliwy użytkownik próbuje zająć wszystkie adresy IP, które serwer DHCP może zaoferować do wydzierżawienia. Wtedy normalny, uczciwy klient nie może skorzystać z usługi DHCP.
##### 2. Fałszowaniu DHCP
   >Obcy, nieautoryzowany serwer DHCP podpina się do sieci i dostarcza fałszywych parametrów konfiguracji IP klientom. Może dzięki temu podsłuchać ich ruch, przenieść ich na podejrzane strony albo po prostu uniemożliwić im kontakt ze światem.
   >
   >Gdy klient aktywuje usługę DHCP to wysyła DHCPDISCOVER i wygra ten, kto szybciej odpowie - niekoniecznie rzeczywisty serwer. Jeśli obcy serwer odezwie się pierwszy to klient zaakceptuje jego parametry konfiguracji. Prawdziwy serwer DHCP zostanie odrzucony. 

### Jak zapobiec?
##### 1. [[DHCP snooping]]