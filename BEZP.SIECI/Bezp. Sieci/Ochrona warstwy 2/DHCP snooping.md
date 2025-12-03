Pozwala ograniczyć [[ataki na DHCP]]. Weryfikuje, czy DHCP pochodzi z zaufanego czy nieznanego źródła. Ruch z nieznanego źródła jest ograniczany i spowalniany.  Urządzenia w stałej sieci - przełączniki, routery, serwery są zaufane, wszystko z zewnątrz jest niezaufane. Porty dostępu też są niezaufane

![[Pasted image 20251129210835.png]]

1. Włącz DHCP snooping na całym urządzeniu
   >`S1(config)# ip dhcp snooping`
2. Wyznacz zaufane porty
   >`S1(config)# interface f0/1`
	 `S1(config-if)# ip dhcp snooping trust`
	 `S1(config-if)# exit`
3. Ogranicz liczbę komunikatów DHCPDISCOVER, które można odebrać na sekundę z nieznanych portów.
   >`S1(config)# interface range f0/5 - 24`
	 `S1(config-if-range)# ip dhcp snooping limit rate 6`
	 `S1(config-if-range)# exit`
4. Włącz DHCP snooping na wybrane sieci VLAN
   >`S1(config)# ip dhcp snooping vlan 5,10,50-52`
	 `S1(config)# end`

