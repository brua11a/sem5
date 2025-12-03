Często certyfikaty CA kupuje się od vendora. Mają one różny "poziom" zaufania w zależności od *klasy*. Nie jest to ustandaryzowane, zatem klasy zależą od sprzedawcy.

![[Pasted image 20251130022326.png]]

"Zaufanie" może też zależeć od architektury PKI.  

### Single-Root PKI
Najprostsza architektura, w której Root CA rozdaje certyfikaty urządzeniom końcowym w swojej organizacji.  
- Wygodne w małych środowiskach  
- Źle się skaluje przy dużych sieciach  
- Wymaga scentralizowanego zarządzania  

### Cross-Certified CA
W tym modelu CA nawzajem się weryfikują.  
- Urządzenia ufające swojemu CA ufają też CA, których ufa ich CA  
- Pozwala na budowanie większych, wzajemnie zaufanych środowisk  
- Przydatne w organizacjach współpracujących ze sobą  

### Hierarchical CA
Struktura drzewiasta, w której Root CA jest na samej górze i rozdaje certyfikaty zarówno urządzeniom końcowym, jak i Subordinate CA.  
- Subordinate CA może wydawać certyfikaty lokalnie, zmniejszając obciążenie Root CA  
- Ułatwia delegowanie zaufania w dużych organizacjach  
- Skaluje się lepiej niż Single-Root PKI  