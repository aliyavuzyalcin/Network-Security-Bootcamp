# NETWORK & SECURITY

## Part - 12.3
----

	Cisco Packet Tracer kullanılmıştır.

## IPv6 OSPF Routing

*	Interface'lerin üzerinde IPv4 olmadığından dolayı manuel olarak **router-id** verilmesi gerekir.
*	Bunu da ***" >router-id [IPv6] "*** ile veririz.
	*	IPv6 ya örnek olarak: Interface IPv6'sı 1ef0:333:33:3::1/64 olduğunu düşünürsek router-id 3.3.3.3 olabilir.

*	Ankara Router'ında Config

		> en
		> conf t
		> ipv6 router ospf 1
		> router-id 3.3.3.3
		> int fa0/0
		> ipv6 ospf 1 area 0
		> int s0/0/0
		> ipv6 ospf 1 area 0

*	İzmir Router'ında Config

		> en
		> conf t
		> ipv6 router ospf 1
		> router-id 5.5.5.5
		> int fa0/0
		> ipv6 ospf 1 area 0
		> int s0/0/0
		> ipv6 ospf 1 area 0

*	İstanbul Router'ında Config

		> en
		> conf t
		> ipv6 router ospf 1
		> router-id 1.1.1.1
		> int fa0/0
		> ipv6 ospf 1 area 0
		> int s0/0/0
		> ipv6 ospf 1 area 0
		> int s0/0/1
		> ipv6 ospf 1 area 0


> ***Yapılan işlemleri kontrol etmek için *" > do show ipv6 route "* komutunu kullanırım.***

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)

