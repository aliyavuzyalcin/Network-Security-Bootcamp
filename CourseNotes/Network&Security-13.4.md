# NETWORK & SECURITY

## Part - 13.4
----

	Cisco Packet Tracer kullanılmıştır.

### IPv4 Tek Yön Ping / Tek Yön TCP Session ACL

>***Senaryo;***

>***Ankara dışarı doğru ping atabilecek ve TCP Session açabilecek. Fakat dış dünya Ankara'ya erişemeyecek.***


*	Ankara Router'ı için yalnızca **Echo-reply**'lara izin verilecek. Çünkü atılan echo'nun gidip cevabının dönmesini bekliyoruz.
*	Dolayısıyla Ankara Router'ının fa0/0 interface'ine **out** yönünde şunu betimleyeceğiz; *dış dünyadan nereden gelirse gelsin bizim (172.16.0.0) networke doğru ICMP'nin **echo-reply**'ına müsade edeceğiz.*

*	Ankara router'ında

		> en
		> conf t
		> ip access-list extended ONEWAY
		> permit icmp any 172.16.0.0 0.0.255.255 echo-reply
		> int fa0/0
		> ip access-group ONEWAY out


*	Ankara Router'ına bir **Server** ekleyip IP'sine 172.16.0.4/16 verelim. Böylece Ankara'daki bu server İstanbul ile TCP session açabilecek. Daha sonra İstanbul açılan bu session'a cevap dönebilecek. Ama İstanbul, Ankara Router'ına bağlı server'da TCP Session açamayacak.

*	Ankara Router'ına

		> ip access-list extended ONEWAY
		> permit tcp any 172.16.0.0 0.0.255.255 established

	*	**established**
		*	Sadece 172.16.0.0 networkünde kurulmuş olan TCP sessionlarına izin verir. Bu networkün dışındaki yerlerden bu networke TCP session'ın kurulmasına izin verilmez.


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 