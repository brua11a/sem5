### Mówimy o:
##### 1. Atakach z przeskokami VLAN (Switch Spoofing Attack)
   >Polega na podpięciu złośliwego komputera do sieci w sposób taki, żeby udawał switcha. Jeśli podepnie się do portu z domyślnymi ustawieniami (`dynamic auto`), to jest w stanie wynegocjować trunk, tym samym zyskując dostęp do każdego VLANu w sieci.
   >
   >![[Pasted image 20251129145745.png]]
##### 2. Atakach podwójnego znakowania VLAN
>*Adnotacja: **Natywna sieć VLAN**: normalnie ruch VLAN jest otagowany, ma identyfikator VLAN. Do natywnego VLAN trafia NIEotagowany ruch, czyli taki NIEnależący do żadnej sieci VLAN. VLAN natywny nie powinien być używany jako normalny VLAN danych, zazwyczaj jeden na całą sieć, takie wysypisko śmieci.* 
>
>Polega na ukryciu dwóch tagów w jednej ramce trunkowej. Zewnętrzny tag VLAN jest taki sam jak natywny VLAN w sieci. Wewnętrzny tag VLAN jest równy docelowemu. 
>
>![[Pasted image 20251129145855.png]]
>
>Gdy ramka dociera do przełącznika, widzi on, że należy ona do VLAN 10, zatem ją "obiera" z tego tagu i wysyła do portów należących do VLAN 10 - tagi teoretycznie nie powinny się znajdować poza trunkami. Jednak w tym wypadku jest jeszcze jeden tag, który dociera do kolejnego przełącznika.
>
>![[Pasted image 20251129145922.png]]
>
>Kolejny przełącznik nie wie o poprzednim tagu, po prostu widzi tag VLAN 20 zatem tam kieruje złośliwą ramkę.
>
>Ten atak działa tylko wtedy kiedy atakujący jest podłączony do portu znajdującego się w tej samej sieci VLAN co VLAN natywny na porcie trunk.



### [[Ograniczanie ataków na VLAN|Jak zapobiegać?]]
##### 1. Wyłącz trunk tam, gdzie nie jest potrzebny - na portach dostępu.
##### 2. Wyłącz automatyczne trunki, nie negocjuj więcej niż trzeba i ustawiaj trunki na sztywno
##### 3. Upewnij się, że sieć VLAN natywna służy TYLKO do połączeń trunk i nie ma w niej normalnych hostów.