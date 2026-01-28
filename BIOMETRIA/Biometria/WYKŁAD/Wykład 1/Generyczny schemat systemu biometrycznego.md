#### Ogólny schemat, składa się z dwóch części:
1. **Rejestracji wzorca** - *enrollment*. Jest to moment, w którym dostarczamy do systemu dane biometryczne, wg. których tworzony jest wzorzec/szablon do porównywania. Ma być jak najmniej szumów i innych artefaktów. 
   >Zaczyna od "miejsca styku" skanera z użytkownikiem - reprezentacja analogowa na reprezentację cyfrową.
   >
   >Potem jest ogromny pipeline przetwarzania danych. Jak najkrócej należy procesować surowe dane biometryczne ze względu na bezpieczeństwo. Przetwarzanie ma być jednostronne, nie można odtworzyć danych z wytrenowanego modelu - przynajmniej w założeniu (przetwarzanie jednokierunkowe). Należy zweryfikować, czy mamy do czynienia z żywą tkanką, czy jest świadectwo żywotności i autentyczności. 
   >
   >Przetworzony model można zapisać w bazie danych, trzeba tylko upewnić się, że nie mamy już takiego wzorca zapisanego.
1. **Weryfikacji/identyfikacji** - części "użyteczniej".
   > W scenariuszu weryfikacji próbka jest porównywana z bazą danych - jeśli próbka wpasowuje się w pewien próg poprawności, użytkownik jest przepuszczany (relacja 1:1). "Czy sprawdzana osoba jest tym, za kogo się podaje?"
   > 
   > W przypadku identyfikacji sprawdzane są WSZYSTKIE próbki w bazie i listowane są potencjalnie pasujące, nawet wszystkie permutacje (relacja 1:N). "Kim jest sprawdzana osoba?"
   > 
   > ![[Pasted image 20260128134919.png]]

#### Podstawowe właściwości systemu biometrycznego
1. **Ochrona wzorca biometrycznego i prywatności**
   > Wzorce biometryczne, surowe dane, powinny być jak najkrócej przechowywane. Wycieki danych biometrycznych mogą pozwolić na pośrednie dostarczanie wniosków.
2. **Podejście anulowalnych biometryk**
   > Dana biometryczna jest trudna do zmiany. Zanim wytworzymy wzorzec, dodajemy element zewnętrzny - funkcję mieszającą. Wykreowana tożsamość nie jest podobna do danych źródłowych. Bez tego zewnętrznego elementu nie będzie możliwe odczytanie biometryki, co czyni ją **anulowalną** - jeśli wzorzec wycieknie, wystarczy zmienić klucz, a nie ucinać palec.
3. **Ergonomia pobierania danych**
   > System ma być użyteczny, wygodny - inaczej ludzie nie będą go używać. Należy jednak pamiętać o stosunku FAR do FRR.
4. **Wykluczenia - dostęp alternatywny**
   > Ma być równie bezpieczny co ten podstawowy. Pozwala dotrzeć do osób, które z jakiegoś powodu nie może użyć domyślnej biometrii - np. ktoś stracił rękę i nie może się nią już identyfikować.
   
#### Tworzenie wzorca z surowych danych biometrycznych
1. Przetwarzanie JEDNOKIERUNKOWE danych biometrycznych
2. Redukcja danych, wytworzenie odcisku będącego szablonem
3. Anulowanie biometryki - *cancellable biometrics*
   > Przy próbach podszycia
4. *Revokowanie* tożsamości i generowanie nowej z tych samych danych biometrycznych
   > Przy próbach podszycia
5. Konieczność dodania elementu zewnętrznego (*auxilary*)

#### Cechy pożądanej biometryki
1. **Uniwersalność**
   >Każdy (albo prawie każdy) człowiek ma tą cechę.
2. **Jednoznaczność**
   >Ta cecha jednoznacznie określa osobę. Np. temperatura ciała nie przejdzie - wiele osób ma 36.6C.
3. **Trwałość w czasie**
   >Np. wzrost nie przejdzie - za szybko się zmienia. 
4. **Techniczna wykonywalność**
   >Te cechy powinno być dosyć łatwo pobrać - zarówno dla urządzenia jak i dla użytkownika.
5. **Akceptowalność**
   >Akceptowalność przez użytkowników pod względem ich kultury, komfortu, higieny.
   
#### Ciągłość weryfikacji
1. **Co jakiś czas ponowna weryfikacja użytkownika podczas korzystania z systemu.**
   >"Zachowanie użytkownika nie odchodzi od jego normalnego"
2. **W czasie rzeczywistym, transparentna i niewymagające atencji.**
   >Użytkownik nie czuje, że jest weryfikowany. Ponowna weryfikacja może być wymagana przy działaniach wymagających podwyższonych uprawnień, takich jak zmiana ustawień bezpieczeństwa - np. w portalach Google nawet będąc zalogowanym ponownie spyta o hasło.
3. **Działa jako SECONDARY metoda, np. *keystroking*, obecność twarzy**
4. ***Liveness detection* - testowanie żywotności**

![[Pasted image 20260128114215.png]]

#### Podejście multimodalne - wiele "biometrii" na raz
1. **Fuzja biometryczna**
   >Np. twarz + oko + odcisk palca.
2. **Zastosowanie wag i mniejszych progów zgodności**
   >Jedne elementy są ważniejsze, inne mniej 
3. **Nomalizacja wyników**

Czasem się robi 1 behawioralną 1 fizyczną - jest to wygodniejsze dla użytkownika.