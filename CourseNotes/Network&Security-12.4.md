# NETWORK & SECURITY

## Part - 12.4
----

	Cisco Packet Tracer kullanılmıştır.

## IPv6 EIGRP

*	Router'larda konfigurasyonlar;

*	Ankara Router'ı:

		> en
		> conf t
		> ipv6 router eigrp 100
		> eigrp router-id 3.3.3.3
		> no sh
		> int fa0/0
		> ipv6 eigrp 100
		> int s0/0/0
		> ipv6 eigrp 100

*	İzmir Router'ı:

		> en
		> conf t
		> ipv6 router eigrp 100
		> eigrp router-id 5.5.5.5
		> no sh
		> int fa0/0
		> ipv6 eigrp 100
		> int s0/0/0
		> ipv6 eigrp 100

*	İstanbul Router'ı:

		> en
		> conf t
		> ipv6 router eigrp 100
		> eigrp router-id 1.1.1.1
		> no sh
		> int fa0/0
		> ipv6 eigrp 100
		> int s0/0/0
		> ipv6 eigrp 100
		> int s0/0/1
		> ipv6 eigrp 100

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)