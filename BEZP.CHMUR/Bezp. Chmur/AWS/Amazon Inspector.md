**Amazon Inspector** to zautomatyzowana usługa oceny bezpieczeństwa, która pomaga **poprawić bezpieczeństwo i zgodność aplikacji uruchamianych w AWS**.

Usługa umożliwia identyfikację luk bezpieczeństwa i odchyleń od najlepszych praktyk w aplikacjach, zarówno przed wdrożeniem, jak i podczas pracy w środowisku produkcyjnym. Przykładowo, Amazon Inspector może sprawdzać niezamierzoną dostępność sieciową instancji EC2 oraz obecność znanych podatności na tych instancjach.

Amazon Inspector pozwala również definiować standardy i najlepsze praktyki dla aplikacji oraz weryfikować ich przestrzeganie. Ułatwia to egzekwowanie polityk bezpieczeństwa w organizacji i proaktywne zarządzanie problemami bezpieczeństwa, zanim wpłyną na działanie aplikacji produkcyjnej.

Po przeprowadzeniu oceny, Amazon Inspector generuje szczegółową listę wykrytych zagrożeń, priorytetyzowanych według poziomu ryzyka. Wyniki można przeglądać bezpośrednio w konsoli AWS lub poprzez API, a także jako część szczegółowych raportów oceny bezpieczeństwa.

Amazon Inspector wykorzystuje **AWS Systems Manager Agent** (SSM Agent), który jest szeroko stosowany w AWS, do zbierania inwentarza oprogramowania oraz konfiguracji z instancji EC2. AWS Systems Manager zapewnia widoczność i kontrolę nad infrastrukturą w AWS. Umożliwia przeglądanie danych operacyjnych z wielu usług AWS w jednym, zunifikowanym interfejsie.