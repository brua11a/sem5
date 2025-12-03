Najczęstszym sposobem jest HMAC - **Keyed-Hash Message Authentication Code**. Jest on wykorzystywany w SSL, IPsec i SSH.

HMAC wykorzystuje algorytm hashujący wraz z kluczem symetrycznym, który zna jedynie nadawca i odbiorca. Do oryginalnego teksu jest dołączany ten klucz, po czym całość jest hashowana. Odbiorcy jest wysyłana plain wiadomość wraz z hashem policzonym z plain+key. Odbiorca może wtedy na podstawie plaintextu (który po prostu dostał) i sekretnego klucza (który z założenia ma) policzyć ten sam hash. **Jeśli są identyczne, to nie doszło do modyfikacji treści i jest ona integralna.**

![[Pasted image 20251130015218.png]]

Ten algorytm jest też wykorzystywany przy uwierzytelnianiu routingu dynamicznego za pomocą OSPF. Tworzony jest hash na podstawie LSU (Link State Update) + sekretnego współdzielonego klucza, po czym LSU+hash są wysyłane do innych routerów uczestniczących w OSPF. Skoro mają one ten sam klucz, mogą policzyć ten sam hash, co pozwala na zweryfikowanie integralności tego LSU. Jeśli hashe nie są identyczne to update jest odrzucany.