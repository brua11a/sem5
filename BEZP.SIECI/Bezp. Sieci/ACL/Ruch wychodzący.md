Pakiety są traktowane jako "wychodzące" po wykonanym procesie routingu ale przed wysłaniem ruchu sieciowego dalej (czyli po routingu wewnętrznie ale przed wysłaniem do np. innego routera czy switcha). Filtrujemy na **WYJŚCIU** gdy tych samych zasad filtrowania chcemy użyć do ruchu pochodzącego z wielu interfejsów wejściowych - wtedy zamiast ustawiać zasad na każdym interfejsie wejściowym osobno można to po prostu zrobić na wyjściu.

WAŻNE: Ruch wychodzący jest przetwarzany przez wychodzącą listę ACL po przetworzeniu przez NAT z wewnątrz do zewnątrz.

Czyli przy ruchu wychodzącym najpierw tłumaczy NAT a potem filtruje ACL.