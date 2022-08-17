# NETWORK & SECURITY

## Part - 13.2
----

	Cisco Packet Tracer kullanılmıştır.

### Access Control Lists

Bir senaryo üzerinden gidelim.


> **Senaryo**
> 
> ***172.16.0.2 dış dünyaya erişsin.***

*	Bunun için Standard ACL kullanalım.

		> en
		> conf t
		> access-list 11 permit host 172.16.0.2
		|---------------------------------------------------------|
		|														  |----| 
		| Eğer "host" değil de "network"e izin vermek isteseydik; |  N |
		| > access-list 11 permit 172.16.0.0 0.0.255.255   	      |  O |
		| yazacaktık.									 	 	  |  T |
		|										  			      |----|
		|---------------------------------------------------------|
	
*	***> access-list 11 permit host 172.16.0.2***
	*	Yazılan bu listenin interface'e de bildirilmesi gerekiyor. Böylece yazılmış bu liste işleme alınabilsin.

*	Interface'e bildirme işlemi:

		> int fa0/0
		> ip access-group 11 in
*	***> ip access-group 11 in***
	*	**11 ID'li Access-List'i inbound *(in - giriş)* yaparken denetle** demektir.
	*	Ya da s0/0/0'dan çıkış yapıp fa0/0'a giderken denetle de denebilir.

* Yazılmış olan kuralı kaldırmak için;

		> no ip access-group 11 in

 *	Yönleri toparlayabilmek adına router'ı **fa0/0 iç dünyamız ve s0/0/0 dış dünyamız** olarak iki kısma ayıralım;
	 *	**fa0/0** bacağında ***inbound*** olarak yazılırsa **iç dünyadan dış dünyaya** çıkacak bütün trafik denetlenir.

*	Bu oluşturulan kuralları da ***access-list LAN-WLAN*** listesine ekleriz. 
*	Neden ayrı ayrı **access-list**'ler oluşturulmadı ?
	*	Cisco router'larda her bir interface'te bir yönlü olmak kaydıyla **en fazla 1 tane access-list** çalışabilir.
	*	Yani 2 ayrı access-list oluşturulamaz.

*	s0/0/0 bacağında **inbound** olarak yazılırsa **dış dünyadan iç dünyamıza** gelecek bütün trafik denetlenir.
*	Bu oluşturulan kuralları da **access-list WAN-LAN** listesine ekleriz. Çünkü yine aynı sebepten; Cisco routerlarda her bir interface'te bir yönlü olmak kaydıyla en fazla 1 tane access-list çalışabilir.

![ACCESS-LIST-INBOUND-OUTBOUND](https://user-images.githubusercontent.com/63460173/185145644-251b5e5e-4a41-42ac-9f22-aed119f3acee.png)



> **Senaryo-2**
> 
> ***172.16.0.0/16 networkü ve 10.0.0.2 hostu 192.168.1.0/24 networküne erişebilecek.Yani 10.0.0.3 erişemeyecek. Burada hem network hem host bir network'e erişecek.***

*	İstanbul Router'ına uygulanacak

		> en
		> conf t
		> access-list 111 permit ip 172.16.0.0 0.0.255.255 192.168.1.0 0.0.0.255
		> access-list 111 permit ip host 10.0.0.2 192.168.1.0 0.0.0.255
		> int fa0/0
		> ip access-group 111 out

	*	fa0/0 interface'ine **out** olarak uygulanacak. ***(Inbound olarak değil)***


*	Bunu bir de **s0/0/0** ve **s0/0/1** dış bacaklarına uygulayarak görelim. Bu iki interface'e **"in"** olarak uygulanacak. Çünkü *dış dünyadan* **gelip** *iç dünyamıza* **girmek** isteyen network ve host mevcuttur.

		> int fa0/0
		> no access-group 111 out
		> int s0/0/0
		> ip access-group 111 in
		> int s0/0/1
		> ip access-group 111 in
		> ex

***NOT***
--
**Aradaki hat yani s0/0/0 ve s0/0/1 dış dünyaya açılırken örneğin OSPF kullandıkları için router'a konulmuş olan access-list kuralının OSPF üzerinde çalışacağını öğretmemiz gerekir.**

	> access-list 111 permit ospf any any

	any any---> Nereden gelirse gelsin nereye gidiyorsa gitsin demektir.	

*	Yani eğer access-list permit (veya deny) kuralı iç dünyamıza (fa0/0 interface'ine) değil de s0/0/0 veya s0/0/1 gibi serial interface'lere koyulacaksa, o interface'lerin kullandığı dynamic routing protokolü de tekrar bu access-list ile interface'lere hatırlatılmalıdır.


***NOT***
--
**IPv6 ile beraber Standard Access-List'leri kaldırdılar. Sadece Extended ACL'ler yazılabilir.**


>***Bir önceki senaryonun aynısını IPv6 ile yeniden yapalım.***

>**-Senaryo-**

>**1ef0:333:33:3::0/64 networkü ve 1ef0:555:55:5::2 hostu 1ef0:111:11:1::0/64 networküne erişecek.**

*	İstanbul Router'ına config

		> en
		> conf t
		> ipv6 access-list IPv6
		> permit ipv6 1ef0:333:33:3::0/64 1ef0:111:11:1::0/64
		> permit ipv6 host 1ef0:555:55:5::2 1ef0:111:11:1::0/64
		> int fa0/0
		> ipv6 traffic-filter IPv6 out

*	***> do show ipv6 access*** komutu ile access-list görüntülenebilir.

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)