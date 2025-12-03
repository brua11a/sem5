Gdy port przebudza się z blokowania, to musi 15s spędzić na każdym stanie - nasłuchiwania i uczenia, czyli razem 30s spędza w takim limbo. Jeśli zostanie ustawiony PortFast to port przechodzi od razu z bloku do przekazywania - na urządzeniach końcowych nie doprowadzi to do problemów.

```
S1(config-if)# spanning tree port fast
```

