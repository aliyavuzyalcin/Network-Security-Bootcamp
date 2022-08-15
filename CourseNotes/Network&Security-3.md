#NETWORK & SECURITY

##Part - 3
----

	Cisco Packet Tracer kullanılmıştır.

##Interface Configuration

*	"*>enable*" ve ardından "*>conf t*" komutları ile terminal açılır.
*	Sonrasında yapılandırılmak istenen interface'in numarası girilir.
	*	>router(config)#**int fa0/0**
		*	**"fa0/0"**, router'ın iç bacağı yani iç networke bakan interface'idir.
*	Verilmek istenen **ip numarası** ve **subnet maskı** ***"ip add"*** komutu ile ilgili *interface*'e verilir.
	*	>router(config-if)#**ip add** 172.16.0.1 255.255.0.0
		*	"**172.16.0.1**" ip adresi gateway olarak verildi.
		*	255.255.0.0 ise ilgili IP'nin ilk 16 bitinin Network ID'yi oluşturduğunu anlatır.
*	Son olarak **"no shutdown"** veya **"no sh"** komutu ile interface aktif hale getirlilir.
	*	>router(config-if)#**no sh**

*	Verilen IP'lerin durumlarını görebilmek için;
	*	>router(config)#**do show ip int brief** kullanılır.
		*	Interface up durumda mı,
		*	IP ve Subnetmask ne verilmiş gibi bilgilere ulaşılabilir.


###Clock

*	ISP tarafından verilir.
*	**Hattın** maximum sinyalleşme hızıdır. 
*	Bu hıza **CLOCK RATE** denir.
*	İki unsurdan oluşur;
	*	**Data Control Equipment**
		*	Clock'un verildiği (belirlendiği) taraftır.

	*	**Data Termination Equipment**
		*	Clock'un verilmediği (belirlenmediği) "**müşteri**" tarafıdır.

###Bandwidth

*	**Interface**'lerin maximum sinyalleşme hızıdır.


>Özetle, **Clock rate** bir otobanda ***yapılabilecek*** *maximum sürati* ifade ederken, **Bandwidth** o otobanda giden aracın ***yapabildiği*** *maximum sürati* anlatır.


>***Bootcamp'te güncel en yüksek hız olan 2mbps bandwidth ve 2000000 clock rate kullanıldı.***

*	Clock rate vermek için **"clock rate"** komutu kullanılır.
	*	>int s0/0/0
		*	ilgili interface'e girilir.

	*	>clock rate 2000000
		*	komnutu ile clock rate'in 2000000 olacağı belirlenir.

	*	>ip add 11.0.0.1 255.255.255.252
		*	komutu ile bu interface'in IP'sinin "**11.0.0.1**" olacağı Subnetmask'ının da "**/30**" olacağı ifade edildi.

	*	>no sh
		*	komutu ile interface aktif hale getirildi.
		

>*	**Burada hem IP yapılandırılması hem de "clock rate" yapılandırılması gerçekleştirildi.**

*	Yapılandırılmış **Broadcast** domainini kontrol etmek için **Router** terminalinden aşağıdaki komut çalıştırılır;
			
		>do ping [IPADRESS]

**Örneğin** yapılandırılmış olan *192.168.1.0/24* networkü için router'da yukarıdaki komut çalıştırılır.

	>do ping 192.168.1.2

*	Eğer **"!"** işareti dönüyorsa yapılandırma başarılı olmuş demektir.
*	Eğer **"."** işareti dönüyorsa yapılandırma başarısız olmuş demektir.


>**Router'lar arası ping testleri de yine aynı şekilde yapılır.**























---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)
