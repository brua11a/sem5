Tablice adresów MAC są podatne na [[Bezpieczeństwo warstwy 2|ataki]], ponieważ switch działa w prosty sposób - uczy się adresów MAC i portu z którego one przyszły. Decyzje na temat "przekazywania dalej" ramek zależą tylko i wyłącznie od adresu warstwy 2. 

Tablice mają stały rozmiar i da się ją przepełnić poprzez zalanie nieprawdziwymi adresami MAC. Gdy tablica się przepełni, KAŻDA ramka jest traktowana jako nieznany unicast i wysyłana na każdy port w LANie i/lub VLANie (poza portem wejściowym). 

![[Pasted image 20251129142254.png]]

Najważniejsze tutaj jest [[Ograniczanie ataków na tablicę adresów MAC|zabezpieczenie portów]] tak, by były w stanie się nauczyć tylko określonej ilości adresów MAC i potem się blokowały. Ta lista dozwolonych adresów MAC może być ustawiona przez administratora manualnie lub nauczona dynamicznie.