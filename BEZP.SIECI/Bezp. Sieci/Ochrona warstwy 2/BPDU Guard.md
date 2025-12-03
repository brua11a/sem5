Chroni urządzenia końcowe przed podpięciem się i zachowywaniem się jak switch - mógłby wtedy wykrzaczyć sieć. Jeśli port z BPDU Guard dostanie BPDU, przejdzie w stan errdisabled. Dzięki temu nie będzie pętli nawet jeśli zdarzy się jakiś błąd lub celowe działanie złośliwego użytkownika.

```
S1(config-if)# spanning tree bpduguard enable
```