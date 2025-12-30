![[Pasted image 20251229184426.png]]

Informacja użyteczna może promieniować z różnych dróg, nawet pomimo szyfrowania (przesyłanej i przetwarzanej informacji), **[[Ekranowanie|ekranowania]]**, filtrowania, **uzmiemiania** czy zmniejszania poziomu emitowanej informacji. 

Dla każdej z dróg musi zostać spełniony warunek **stopnia protekcji systemu**:
$$
ps=\frac{E_d}{E_p}>1
$$
$E_d:$ minimalny poziom emisji widma wiadomości, przy którym istnieje potencjalna możliwość detekcji EM wiadomości - właściwie to próg detekcji, możliwość potencjalnego atakującego.

$E_p:$ poziom emisji wiadomości przez system jako całość - ile i jak informacje emituje system.

$\frac{E_d}{E_p}>1\rightarrow E_d>E_p:$ zależy nam na tym, żeby do detekcji potrzebne było więcej informacji, niż jest rzeczywiście emitowane w jakimkolwiek możliwym wektorze ataku.

#### Obszar chroniony
![[Pasted image 20251229190155.png]]

Obszar chroniony to skutecznie ekranowana $S_s$ strefa. Jest wyposażony w filtry elektryczne o odpowiedniej skuteczności $A_{fs}$. Emisyjność urządzeń w takiej strefie powinny mieć ograniczoną emisyjność:
$$E_{pu}=max\{\;E_{pur},\;E_{puc}\;\}$$Oznacza to, że emisja pierwotna $E_p$ zostaje stłumiona tak, że wychodzący sygnał $E_{pu}$ jest pod granicą szumu.

$E_{pur}:$ maksymalna dopuszczalna emisja promieniowania widma wiadomości przez samo urządzenie w obszarze chronionym
$E_{puc}:$ maksymalna dopuszczalna emisja promieniowania ogólnie

Dodatkowo, spełniamy ma być warunek, który jest rozszerzeniem normalnego wzoru na $ps$:
$$
ps(f)\;[dB]=20*log(\frac{E_d}{E_{pu}})+S_s\;[dB] = 20*log(\frac{E_d}{E_p})>0
$$
#### Strefy ochronne
Strefy ochronne wyznacza się wtedy, gdy nie można zapewnić odpowiedniego stopnia protekcji systemu. Są to obszary wokół obiektu, w których natężenie pola EM emitowanego przez system nie przekracza poziomu umożliwiającego detekcję informacji.

Można po prostu fizycznie nie udzielić dostępu w pobliżu emitującego urządzenia - jeśli nikt nie podejdzie to nikt nie zmierzy.

![[Pasted image 20251229191012.png]]