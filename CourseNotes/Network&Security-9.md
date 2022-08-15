#NETWORK & SECURITY

##Part - 9
----

	Cisco Packet Tracer kullanılmıştır.

##BGP (Border Gateway Protocol)

*	Servis sağlayıcılar arasında çalışır.
*	Diğer protokollere nazaran yavaştır.
*	Internet bu protokol üzerinde çalışır.
*	Bağlantıları **network anonslarıyla** değil **point-to-point** gerçekleştirir.
*	Burada ***BGP-Multi Home*** olarak geçen kısmını işleyeceğiz.
*	BGP, herkesin kendi **"BGP Autonom-System (AS)** numarasıyla processleri başlattıktan sonra karşı komşunun kendisine bakan taraftaki **interface IP'sini** ister.
*	Bunu yaparken de **"> neighbor 11.0.0.1"** syntax içerisine alır.
*	Aynı syntax ve satır içerisinde komşusunun AS numarasını da ister.
*	Bunu da **"> remote as #komsununASnumarası"** komutuyla ekler.
*	**Örneğin**, Ankara'dan İstanbul'a BGP protokolünü uygulayacak olursak;
	*	İstanbul'un Ankaraya bakan Interface'i: s0/0/0 ve IP: 11.0.0.1/30
	*	Ankara'nın İstanbul'a bakan Interface'i: s0/0/0 ve IP: 11.0.0.2/30

*	Ankara için:

		> neighbor 11.0.0.1 remote-as 100
*	İstanbul için:

		> neighbor 11.0.0.2 remote-as 300

*	Protokol kurulduktan sonra kendi networklerini de anons etmeleri zaruridir.

*	İstanbul'a kendi networkünü anons ettirmek istersem:

		> network 192.168.1.0 mask 255.255.255.0
		
*	Ankaraya kendi networkünü anons ettirmek istersem:

		> network 172.16.0.0 mask 255.255.0.0
		
###Basic Configuration

*	Her router kendi **AS numarasıyla** açılır. 
	*	Ankara AS numarası 300.
	*	İstanbul AS numarası 100.

*	Ankara Router'ında Configuration:

		> en
		> conf t
		> router bgp 300
		> neighbor 11.0.0.1 remote-as 100
		> network 172.16.0.0 mask 255.255.0.0

###ÖZETLE

*	**"> router bgp [AS NUMBER]"**
	*	BGP protokol başlatma komutu.
*	**"> neighbor [karşıInterfaceIP] remote-as [karşıASNumber]**
	*	Komşuluk başlatma komutu.
*	**"> network [KendiIcNetworkIP] mask [Subnetmask]
	*	Kendi iç networkünü komşularına bildirme komutu.


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 