*Adnotacja: **Domeną rozgłoszeniową** nazwiemy całą sieć złożoną z połączonych przełączników - zawiera wszystkie urządzenia sieci LAN, które otrzymają ramki rozgłoszeniowe wysłane przez hosta a potem zalane na switchu. Przełącznik ramki rozgłoszeniowe wysyła na każdy port poza tym, z którego przyszło. Broadcastów raczej chcemy unikać bo zaśmiecają sieć ruchem. To, co rozdzieli domeny rozgłoszeniowe to albo brak kabla (obvious) albo router.* 

VLANy to sieci rozgłoszeniowe, ale **PVLANy** zapewnia izolacje pomiędzy portami w tej samej domenie rozgłoszeniowej na poziomie warstwy 2. Rozpoznajemy trzy typy portów PVLAN:
1. **Promiscuous**
   >Może porozumiewac się z kazdym interfejsem
2. **Isolated**
   >Może porozumiewać się tylko z promiscuous portami, jest zupełnie odizolowany od innych portów nawet w tym samym PVLAN.
3. **Community**
   >Może porozumiewać się z promiscuous portami i portami w tym samym community.
   
![[Pasted image 20251129161207.png]]

### [[Ataki na PVLAN]]