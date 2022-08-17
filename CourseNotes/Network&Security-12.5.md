# NETWORK & SECURITY

## Part - 12.5
----

	Cisco Packet Tracer kullanılmıştır.

## IPv6 REDISTRIBUTION

*	Router'larda konfigurasyonlar;

*	Ankara Router'ı 

		> ipv6 router eigrp 100
		> eigrp router-id 3.3.3.3
		> no sh
		> int fa0/0
		> ipv6 eigrp 100
		> int s0/0/0
		> ipv6 eigrp 100

*	İzmir Router'ı

		> ipv6 router ospf 1
		> router-id 5.5.5.5
		> int fa0/0
		> ipv6 ospf 1 area 0
		> int s0/0/0
		> ipv6 ospf 1 area 0

*	İstanbul Router'ı

		> ipv6 router eigrp 100
		> eigrp router-id 1.1.1.1
		> no sh
		> int s0/0/0
		> ipv6 eigrp 100
		>
		> ipv6 router ospf 1
		> router-id 1.1.1.1
		> int s0/0/1
		> ipv6 ospf 1 area 0


> ***Yapılanları kontrol etmek için *> do show ipv6 route* komutunu kullanırız.***

### Redistribution Konfigürasyonu

*	İstanbul Router'ında

		> ipv6 router eigrp 100
		> redistribute ospf 1 metric 100 10 125 125 1500
		> 
		> ipv6 router ospf 1
		> redistribute eigrp 100
		> redistribute connected
		> ipv6 router eigrp 100
		> redistribute connected 100 10 125 125 1500

	*	***> redistribute connected***
		*	komutu ile İstanbul'un iç networkünün bilgisini dışarıdaki komşularına dağıttık.
		*	İç network için de yine ilgili metric'leri yazdık.
 

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)