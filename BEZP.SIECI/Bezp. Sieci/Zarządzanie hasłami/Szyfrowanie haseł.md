Trzeba zawsze je wykonać po [[Najprostsza wersja|podstawowej konfiguracji]]. 

Należy zaszyfrować hasła zapisane w startup-config i running-config - bez tego zapisane hasła (komendy `password`) będą widoczne plaintextem. Oznacza to, że każdy mający dostęp do odczytu mógłby zobaczyć wszystkie hasła wykorzystywane na urządzeniu. Podstawowy, dosyć słaby algorytm można zastosować przy pomocy:
```
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# service password-encryption
Sw-Floor-1(config)#
```

Szyfrowanie można zweryfikować w konfiguracji:
```
Sw-Floor-1# show running-config
!
(Output omitted)
!
line con 0
password 7 094F471A1A0A
login
!
line vty 0 4
  password 7 094F471A1A0A
  login
line vty 5 15
  password 7 094F471A1A0A
  login
!
end
```

Komenda `enable secret` dzięki słowie `secret` domyślnie już szyfruje. Nadal jest to jednak słaby algorytm. 

Jeśli chcemy czegoś mocniejszego, należy wybrać mocniejszy algorytm. Wiąże się to jednak z tym, że po określeniu algorytmu należy wkleić już zahashowane hasło, np. przeklejone z innej konfiguracji, bo komenda `enable secret` nie zamieni plaintextu na mocniejszy hash sama w sobie.

```
R1(config)# enable secret cisco12345
R1(config)# do show run | include enable
enable secret 5 $1$cam7$99EfzkvmJ5h1gEbryLVRy.

R1(config)# enable secret 9 cisco12345
ERROR: The secret you entered is not a valid encrypted secret.
To enter an UNENCRYPTED secret, do not specify type 9 encryption.
When you properly enter an UNENCRYPTED secret, it will be encrypted.
 
R1(config)# enable secret 9  
$9$HZWdzLHwhPtZ3U$D9OlUDSGvBy.m8Tf9vCGDJRcYy8zIMbyRJgtxgRkwzY
R1(config)#
```

Da się jednak wpisać hasło plaintextem i od razu je zaszyfrować mocnym algorytmem, służy do tego komenda **`enable algorithm-type`**:
> `Router(config)#` **`enable algorithm-type`** *`{  md5 | scrypt | sha256  }`* **`secret`** *`unencrypted password`*

#### `enable secret hasło` -> `enable` **`algorithm-type` *`algorytm`*** `secret hasło`

Gdzie preferowany algorytm to `scrypt` (9) bo jest najsilniejszy. 