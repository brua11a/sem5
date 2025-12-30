Polega na bezpośrednim modulowaniu fali nośnej strumieniem danych, który został wcześniej rozproszony za pomocą sekwencji kodowej (rozpraszającej) o znacznie większej szybkości niż dane użytkowe. 

Strumień danych jest rozpraszany przy pomocy sekwencji rozpraszającej - np. przemnaża się XOR oryginalny sygnał z tą sekwencją.

![[Pasted image 20251225203459.png]]

Otrzymany sygnał ma o wiele szersze pasmo częstotliwości niż oryginalny strumień danych, dzięki czemu jest mniej podatny na zakłócenia. Zwiększa się zysk przetwarzania $G_p$. 

![[Pasted image 20251225203709.png]]![[Pasted image 20251225203829.png]]

*Bierzemy sobie strumień danych o jakimś czasie trwania, bierzemy sekwencję rozpraszającą i mnożymy (XOR). Sekwencję bitów zapisujemy w o wiele gęstszej sekwencji, co rozprasza sygnał. Efekt jest taki, że energia wypełnia większy zakres częstotliwości ale jest "niższa", zatem możliwa jest koegzystencja systemów. Podczas skupienia (korekcji) szumy są rozpraszane. Jest to dobre jeśli mamy synchronizację, dobrze skorygowane zegary itd. - w chujowych systemach ten typ rozpraszania nie działa poprawnie.* 