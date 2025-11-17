Dane ogólnie mówiąc są bardziej narażone w ruchu, niż w [[Szyfrowanie danych w spoczynku|spoczynku]]. Znanym atakiem jest MITM (man in the middle) - narażenie na podsłuch i nieuprawnioną modyfikację informacji. 

#### Sposobami ochrony danych w ruchu są:
1. **SSL/TLS**
   >Pozwala na bezpieczne pobieranie i wysyłanie danych dzięki HTTPS
2. **Szyfrowanie**
   >Dane są zaszyfrowane w ruchu zanim dotrą do [[Ochrona S3|S3]]
3. **Wykorzystywanie endpointów Amazon [[VPC]] żeby ograniczyć dostęp do zasobów**
   >Tylko z niektórych zasobów można dostać się do innych zasobów