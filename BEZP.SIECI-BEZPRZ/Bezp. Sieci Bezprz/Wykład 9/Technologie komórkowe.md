Historia radiokomunikacji cyfrowej od 3G do 5G.

"Cegły" miały tragiczny zasięg i brak szyfrowania - wystarczyło się dobrze ustawić żeby podsłuchać. Wykorzystywano TDMA/FDMA.

#### 3G
Przepustowość do 2 Mb/s w budynkach, 384 kb/s w obrszarach zabudowamnych, 144 kb/s w niezabudowanych. UMTS, wprowadzono megakomórki, makrokomórki, mikrokomórki, pikokomórki - zwiększa pojemność sieci. Jeśli chcemy mieć porządny dostęp do Internetu, podłączamy się do jak najmniejszej komórki, co odciąża większe komórki. 

UMTS - architektura dzieli się na User Equipment UE, UMTS Terrestrial Radio Access Network, Core Network (sieć szkieletowa, "tu się dzieje cała magia"), External Networks (sieci zewnętrzne)

Moce nadajników UMTS są małe - średnie BS ma +38 dBm, maksymalna transmitowana moc to 50dBm czyli 100W. Terminale mają większą moc zazwyczaj i są bliżej - 33dBm.

UMTS werscji 6, 7, 8 miały zwiększać przepustowość aż do 14 mega. Warstwy sieciowe w UMTS są podobne do ISO/OSI ale są tylko trzy warstwy - fizyczna, łącza danych i sieciowa. Warstwa MAC przypisuje szerokość pasma (?). W UMTS są dwa dupleksy - FDD i TDD. Adaptacyjne kodowanie mocy powoduje różne szybkości na wyjściu - od 5 do 12 kb/s. 

UMTS pracował w paśmie od 1885 MHz do 2170 MHz na całym globie. W Europie pojawiła się kolizja z innym systemem. TDD ma wąskie pasma, FDD szersze. Przewidziano pasma dodatkowe ale ich nie wykorzystywano.

UMTS bazował na tym, że mamy całe pasmo dostępne dla użytkownika - dany klient dostawał 5MHz lub całą szczelinę czasową 666,67 us. Nie dzielono na kanały, jedynie nadawano kody. Widmo rozszerzano w kanale, rozpraszano, co zwiększało niezawodność. Żeby to działało, należało zsynchronizować wszystko. 

Żeby sieć UMTS była zrównoważona, stacja bazowa kontroluje moc terminali tak, żeby zminimalizować S/N. Urządzenia pracują z minimalną wymaganą mocą. 

Oddychanie komórek - nakłada się je w 30-40% żeby skompensować to, że się one kurczą. DO zwiększania pojemności robiono tak, że jeśli mikrokomórki się przepełniały to ruch szedł do makrokomórek. 

W 2002 pojawiła się nowe zastępstwo UMTS - HSDPA, szybszy downlink i inne modulacje.

#### LTE
Skalowanie szerokości kanału, zwiększona wydajność widmowa w porównaniu z UMTS, opóźnienia poniżej 5ms dla IP, działa do 400 km/h sensownie.

Architektura mało się różni od UMTS, nazewnictwo jest trochę inne ale zasada działania podobna. OFMD mocno zwiększył skalowalność systemu. Pojawiło się kształtowanie wiązki, MIMO 2x2 4x4, adaptacyjna zmiana wartościowości modulacji.

LTE-Advanced wprowadza agregację pasma częstotliwościowego do 100 MHz, MIMO 8x8, mechanizmy retransmisji (naprawia problem wielodrogowości), 

#### 5G 
Założenia - nie przepisałem ;/

