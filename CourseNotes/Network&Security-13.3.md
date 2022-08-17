# NETWORK & SECURITY

## Part - 13.3
----

	Cisco Packet Tracer kullanılmıştır.

### IPv4 Port Base Access List

*	**DNS**
	*	Domain Name Server
	*	Kendisine sorulan adresleri çözümleyip geri döner.
	*	Örneğin; www.cisco.com adresi sorulur ve IP'si öğrenilir.

*	**Web Server**
	*	Bu server'da *"www.cisco.com"* adresli web service barındırılır.
	*	Birçok hizmet sağlar; HTTP, DHCP, DNS, FTP vs.

*	**NS Kaydı**
	*	DNS Server üzerinde IP adresini bir website adresi ile ilişkilendirmeye denir.
	*	Örneğin; www.cisco.com için 192.168.1.3 IP adresini kaydetmek gibi.

*	Laptop gibi **end-device**lara ***DNS Server***'ın IP adresi öğretilmelidir. Böylece cihazlar aradıkları adresi sorabilecek ve cevap alabilecektir.
*	Web Server ***tcp 80*** portunu çalıştırır.
*	DNS Server ***udp 53*** portunu çalıştırır.


>***Yine bir senaryo üzerinden gidelim;***

> 172.16.0.0/16 Networkü 

> 192.168.1.2 makinesine **udp 53** ile,

> 192.168.1.3 makinesine **tcp 80** ile erişim sağlayacaktır.


*	Named ACL kullanalım.
*	Istanbul Router'ında;

		> en
		> conf t
		> ip access-list extended WEBACL
		> permit udp 172.16.0.0 0.0.255.255 host 192.168.1.2 eq 53
		> permit tcp 172.16.0.0 0.0.255.255 host 192.168.1.3 eq 80
		> int fa0/0
		> ip access-group WEBACL out

	*	**permit**
		*	permit veya deny olabilir.
		*	İzin verilip verilmediğini belirliyoruz.

	*	**udp**
		*	kullanılacak protokol.
		*	TCP veya UDP.

	*	**172.16.0.0 0.0.255.255**
		*	NEREDEN
		*	Network olduğu için wildcard mask kullanıldı. Host olsaydı başında "host" yazacak ve wildcard ifadesi bulunmayacaktı.

	*	**host 192.168.1.2**
		*	NEREYE

	*	**eq**
		*	Equal'ın kısaltması.
		*	Kullanılacak protokolün hangi portu kullanacağı bilgisidir.


### IPv6 Port Base Access List

**Aynı senaryo üzerinden gidelim.**

*	İstanbul Router'ında

		> en
		> conf t
		> ipv6 access-list WEBACL
		> permit udp 1ef0:333:33:3::0/64 host 1ef0:111:11:1::2 eq 53
		> permit tcp 1ef0:333:33:3::0/64 host 1ef0:111:11:1::3 eq 80
		> int fa0/0
		> ipv6 traffic-filter WEBACL out
		> 

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 