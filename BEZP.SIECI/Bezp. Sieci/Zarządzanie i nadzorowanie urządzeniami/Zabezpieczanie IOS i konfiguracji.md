Stare urządzenia Cisco mają taki feature jak *resilient configuration*, pozwala on na zachowanie lokalnej, bezpiecznej, działającej kopii obrazu systemu routera i bieżącej konfiguracji. 

Zachowanie obrazu do bootowania jest możliwe dzięki `secure boot-image`, a bootowalnej konfiguracji dzięki `secure boot-config`. 

Zapisane w ten sposób pliki nie są widoczne w wyniku wpisania komendy `dir` jak normalne pliki. Zamiast tego do weryfikacji należy użyć `show secure bootset`. 

```
R1# show secure bootset
IOS resilience router id FTX1449AJBJ
 
IOS image resilience version 15.4 activated at 12:47:09 UTC Tue Sep 22 2020
Secure archive flash0:c2900-universalk9-mz.SPA.154-3.M.bin type is image (elf) []
  file size is 103727964 bytes, run size is 103907016 bytes
  Runnable image, entry point 0x81000000, run from ram
 
IOS configuration resilience version 15.4 activated at 12:47:18 UTC Tue Sep 22 2020
Secure archive flash0:.runcfg-20200922-124717.ar type is config
configuration archive size 1683 bytes
```

#### Ładowanie zapasowego obrazu
1. `reload`
2. Z ROMmon mode, wpisz komendę `dir` wskazując na directory, w którym jest zachowany backup (tutaj plik to `flash0:c2900-universalk9-mz.SPA.154-3.M.bin`, zatem cała komenda to `dir flash0:`).
3. Po potwierdzeniu, że plik instnieje, zbootuj z niego - `boot nazwa` (tutaj byłoby to `boot flash0:c2900-universalk9-mz.SPA.154-3.M.bin`).
4. Wejdź w privileged EXEC mode i config mode, żeby odzyskać konfigurację - `secure boot-config restore ścieżka` (tutaj na przykład `flash0:rescue-cfg`).
5. Skopiuj odzyskaną konfigurację z wyznaczonej ścieżki do running config `copy flash0:rescue-cfg running-config`.

#### Bezpieczna kopia
Cisco IOS Resilient pozwala zabezpieczać pliki tylko lokalnie, ale jest protokół **SCP** (*Secure Copy Protocol*), który pozwala na bezpieczne kopiowanie do zdalnej lokacji dzięki [[Podstawy SSH|SSH]] i AAA.

Poza podstawową konfiguracją SSH (gdzie, uwaga, musi powstać osoba z [[Privilege level|privilege 15]]), należy stworzyć prosty model `aaa`. Na końcu serwer SCP trzeba włączyć.

```
...konfiguracja ssh...
R1(config)# aaa new-model                          
R1(config)# aaa authentication login default local
R1(config)# aaa authorization exec default local  
R1(config)# ip scp server enable
```

Po tym można skopiować konfigurację z lokalnego storage do zdalnej lokacji.

```
R2# copy flash0:R2backup.cfg scp:
Address or name of remote host []? 10.1.1.1
Destination username [R2]? Bob
Destination filename [R2backup.cfg]?  
Writing R2backup.cfg  
Password: <cisco12345>
!
1381 bytes copied in 8.596 secs (161 bytes/sec)
 
R2#
```

