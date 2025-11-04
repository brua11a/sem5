Żądania są wysyłane przez menedżera [[SNMP]] i odbierane przez agenta, który wykona polecenie na podstawie wartości polecenia. W wielkim skrócie, instrukcje "**get**" służą do pobrania z bazy MIB agenta jakiś informacji, a "**set**" do ustawienia jakiejś wartości na agencie, a nawet wymuszenie restartu.

![[Pasted image 20250518114609.png]]

Odpowiedzią agenta na żądanie może być wyjęcie informacji z bazy MIB i przesłanie jej do menedżera albo ustawienie wartości jakiejś zmiennej w MIB, po czym odesłanie aktualniejszej konfiguracji do menedżera. 

![[Pasted image 20250518115056.png]]