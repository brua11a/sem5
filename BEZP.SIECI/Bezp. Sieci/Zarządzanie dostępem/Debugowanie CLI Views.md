1. Wejdź w widok jako admin i zobacz do czego masz dostęp
   >```
   >R1# enable view USER
Password: <cisco1>
   >```

Pozwala to zweryfikować dostępne komendy przy pomocy `?`
```
R1# ?
Exec commands:
  <0-0>/<0-4>  Enter card slot/sublot number
  do-exec      Mode-independent "do-exec" prefix support
  enable       Turn on privileged commands
  exit         Exit from the EXEC
  show         Show running system information
 
R1# show ?    banner      Display banner information
  flash0:     display information about flash0: file system
  flash1:     display information about flash1: file system
  flash:      display information about flash: file system
  parser      Display parser information
  usbflash0:  display information about usbflash0: file system
```

2. Zobacz kim jesteś
   >```
   >R1# show parser view
Current view is 'JR-ADMIN'
   >```

Można też podejrzeć wszystkie widoki, gdzie `*` są oznaczone [[Superview]].
```
R1# show parser view
Current view is 'root'
 
R1# show parser view all
Views/SuperViews Present in System:
  SHOWVIEW
  VERIFYVIEW
  REBOOTVIEW
  USER *  
 
  SUPPORT *
 
  JR-ADMIN *
 
-------(*) represent superview-------
R1#
```