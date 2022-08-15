#NETWORK & SECURITY

##Part - 12.1
----

	Cisco Packet Tracer kullanılmıştır.

##IPv6

*	16'lık sayı sistemiyle toplam uzunluğu 128 bit olan 8 field'tan oluşan yeni bir adres metotudur.
*	NDP (Network Discovery Protocol), daha önce kullanılan ARP'nin (Address Resolution Protocol) yerini aldı.
*	MAC ve IP adresi arasındaki eşleşme **fe80** bloğu olarak geçen ***link local adresleri*** olarak adlandırılan özel bir IPv6 formatındaki unique bir adresle layer 2 adresleme ile yapılır.
*	**Link local adresler :** IP'nin **fe80** ile başlayan bloğu IPv4'te MAC'in yeni karşılığıdır.
*	**Non-rootable IP'ler :** 192.168.0.0 veya 172.16.0.0 bloğu gibi bloklar internet üzerinde non-rootable erişilememesi gibi bu IP'ler de erişilemez.
*	IPv6 deafult olarak **IPSec** gelir.
*	IPv4'te ise bu çeşitli işlemler ile sağlanır.

[Resim: IPv4-VS-IPv6]

*	IPv6 Interface Configuration:

	*	Subnetmask yerine kaç tane **routing bit** varsa **summarize** ***(prefix denir)*** edilir ve eklenir.

*	Ankara Router'ında IPv6 Config:

		> ipv6 unicast-routing
		> int fa0/0
		> ipv6 add 1ef0:333:33:3::1/64
		> no sh
		> int s0/0/0
		> ipv6 add 1ef0:abc:bc:c::2/126
		> no sh

*	İzmir Router'ında IPv6 Config:

		> ipv6 unicast-routing
		> int fa0/0
		> ipv6 add 1ef0:555:55:5::1/64
		> no sh
		> int s0/0/0
		> ipv6 add 1ef0:def:ef:f::1/126
		> no sh


*	**> ipv6 unicast-routing**
	*	Device **router** olsa bile bu komut girilmediği takdirde IPv6 tabanındaki Layer 3 trafiğe kapalı gelir. Bu trafiğin aktif edilmesi için yazılması gereken komutta budur.

*	İstanbul Router'ında IPv6 Config:

		> en
		> conf t
		> ipv6 unicast-routing
		> int fa0/0
		> ipv6 add 1ef0:111:11:1::1/64
		> no sh
		> int s0/0/0
		> clock rate 2000000
		> ipv6 add 1ef0:abc:bc:c::1/126
		> no sh
		> int s0/0/1
		> clock rate 2000000
		> ipv6 add 1ef0:def:ef:f::1/126
		> no sh

>***Yani aslında IPv4'te interface'lere nasıl IP veriyorsak IPv6 için de aynısı geçerlidir. Tek farkı IPv4 için *> ip add"* komutu kullanılırken IPv6 için *"> ipv6 add"* komutu kullanılır.***

###Static Routing IPv6

*	Ankara Router'ı

		> en
		> conf t
		> ipv6 route 1ef0:111:11:1::0/64 1ef0:abc:bc:c::1
		> ipv6 route 1ef0:555:55:5::0/64 1ef0:abc:bc:c::1

*	İzmir Router'ı

		> en
		> conf t
		> ipv6 route ::/0 1ef0:def:ef:f::1

	*	**::/0**
		*	ifadesi *default routing*'i ifade eder. 
		*	Tıpkı IPv4'teki *0.0.0.0 0.0.0.0* ifade gibi.


*	İstanbul Router'ı

		> en
		> conf t
		> ipv6 route 1ef0:333:33:3::0/64 1ef0:abc:bc:c::2
		> ipv6 route 1ef0:555:55:5::0/64 1ef0:def:ef:f::2

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)