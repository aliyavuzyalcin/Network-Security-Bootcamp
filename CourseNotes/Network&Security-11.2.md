#NETWORK & SECURITY

##Part - 11.2
----

	Cisco Packet Tracer kullanılmıştır.

##SWITCHING

###TelNet Açmak

*	Bir device'ta **TelNet açmak** için yapılacak konfigurasyonlar;

		> en
		> conf t
		> line vty 0 15
		> password [PASSWORD]
		> login
		> enable secret [PASSWORDCISCO]

*	**> line vty 0 15**
	*	0'dan 15'e kadar 16 tane session açmak için bu switch üzerinde izin verildi.

*	**> enable secret [PASSWORD]**
	*	Cihaz üzerinde eğer bir **enable secret PASSWORDCISCO** olmazsa kendisini ***TelNet*** sonrası erişime açamaz. Çünkü TelNet bir uzaktan bağlantıdır ve güvenli olması gerekir.

*	TelNet bir TCP/IP bağlantı metotu olduğundan Switch'e bir IP vermemiz gerekir. Layer 2 cihaz olan Switchlere IP ataması **"ip add"** ile doğrudan interface'e yapılamaz.
*	Bunun için Vlan 1 interface'ine girerek Vlan 1'e IP ataması yapılır.

		> int vlan 1
		> ip address 192.168.1.1 255.255.255.0
		> no sh

*	Bir network sorumlusu gelip TelNet ile ağlardaki bütün switchlere bağlanabilir.
*	Bunun için bilgisayarın CMD ekranından;

		> telnet 192.168.1.1
		> Password:[PASSWORD]
		> en
		> Password:[PASSWORDCISCO]
		> conf t

*	Artık istersek ağ içerisindeki diğer Switchlere de buradan TelNet çekilebilir.

		> telnet 192.168.1.2

	gibi.

*	Böylece **administrative vlan 1** kullanılmış olur.
*	Administrative Vlan 1'e bağlanan network sorumlusunun laptopu da:
	*	Vlan 1'e bağlanır.
	*	Kendi IP'si örneğin 192.168.1.111/24 olur.
	*	TelNet'i de verilmiş olan IP'ye yani bizim durumda 192.168.1.1'e çeker.

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 