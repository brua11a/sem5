Pakiety filtrujemy na **WEJŚCIU** zazwyczaj gdy sieć dołączona do interfejsu wyjściowego jest jedynym źródłem informacji - czyli cały ruch do przefiltrowania wchodzi jednym interfejsem, zatem można go odfiltrować zanim przejdzie do interfejsu wyjściowego, co jest "lżejsze" dla routera niż przeniesienie pakietu na interfejs wyjściowy i dopiero wtedy go odfiltrowanie.

WAŻNE: Ruch przychodzący jest przetwarzany przez przychodzącą listę ACL przed przetworzeniem przez NAT z zewnątrz do wewnątrz.

Czyli przy ruchu przychodzącym najpierw filtruje ACL, a dopiero wtedy tłumaczy NAT.