**Amazon Cognito** to usługa zapewniająca **uwierzytelnianie, autoryzację i zarządzanie użytkownikami** (rejestracja, logowanie i kontrola dostępu) dla aplikacji webowych i mobilnych. Udostępnia bezpieczny *identity store*, który umożliwia skalowanie nawet do milionów użytkowników.

Cognito obsługuje zarówno bezpośrednie logowanie przy użyciu nazwy użytkownika i hasła, jak i uwierzytelnianie za pośrednictwem zewnętrznych dostawców tożsamości, takich jak Apple, Google, Facebook czy Amazon.

Usługa opiera się na dwóch głównych komponentach: **user pools** i **identity pools**.
- **User pools** to katalogi użytkowników, które obsługują procesy rejestracji i logowania w aplikacji. Mogą integrować się z zewnętrznymi dostawcami tożsamości oraz wspierają funkcje bezpieczeństwa, takie jak MFA (Multi-Factor Authentication) i weryfikacja numeru telefonu.
- **Identity pools** pozwalają natomiast przyznawać użytkownikom tymczasowe, ograniczone uprawnienia AWS poprzez generowanie krótkotrwałych poświadczeń, umożliwiających dostęp do wybranych usług AWS.