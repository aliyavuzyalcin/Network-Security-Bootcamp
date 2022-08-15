#NETWORK & SECURITY

##Part - 5
----

	Cisco Packet Tracer kullanılmıştır.

###ADMINISTRATIVE DISTANCE

*	Routing tablosuna giren her "entry"nin (ister statik ister dynamic olsun) bir **administrative distance** değeri vardır.
*	Bu değer en düşük olarak **"statik route"**larda bulunur.
*	Yani hem statik hem de OSPF paket getirdiyse cihaz, statik route tercih eder.
*	Static route'un metriği 0 (sıfır), default route'un metriği ise 1'dir.
*	Bir cihazda hem static hem de default route varsa şu anlama gelir;
	*	Önce **static route**'a bak. Onunla ilgili bir durum yoksa **default route**'a yönlendir. ***(Default route = Default Gateway)***

##Dynamic Routing Protocols

*	Dinamik routing protokolleri ikiye ayrılır;
	*	Distance Vector Protokoller
		*	**Uzaklık vektörü** demektir.
		*	*"Hop count"* parametre olarak kullanılır.
		*	Hız önem arz eder.
		*	RIP bunu kullanır.
		*	64.000 kbps hız kullanır.

	>Zamanla hızlar değişti. Artık **bant genişliği** önem arz etmeye başladı. Dolayısıyla Link State Protokollere geçildi.

	*	Link State Protokoller
		*	Link State, "**hattın durumu** demektir.
		*	*Bandwidth, delay* parametrelerini kullanır.
		*	OSPF, IEGRP bunlara örnek verilir.

Yani, **statik routing**, IP adreslerinin routerlara manuel olarak tek tek verilmesi ve hangisinin nereye gitmesi gerektiğinin öğretilmesidir.
**Dinamik routing** ise bir router'ın altındaki networkü kendi komşularına bildirmesi/haber vermesidir. Bunu da iki yolla yapar;

-	Distance vector
-	Link state


**Distance vector**, uzaklık vektörü demektir. Bu protokolü ***RIP*** kullanır ve eskidir.

###RIP

*	Bir distance vector protokolüdür.
*	Hızı 64000 kbps'dir.
*	Metriği "*hop count*"tur. Her bir router atlamaya 1 ekler.
*	Konfigürasyonu: *">router rip"* ile başlatılır. Sonrasında kendisine direkt bağlantılı olan networkler anons edilir.

		> en
		> conf t
		> router rip
		> network [IP]
		> netowrk [IP-local]

*	**">network 11.0.0.0"**
	*	Bu ifade 11.0.0.0 networkünün diğer ucunda da çağırılınca iki taraf arasında komşuluk kurulacak.
*	**">network 13.0.0.0"**
	*	Varsa başka direkt bağlantı, onlar da anons edilir.

*	**">network 172.16.0.0"**
	*	Bağlantı kurmuş olduğu komşulara kendi **iç** *(local)* networkünü duyurması için yazılır.

###RIP Version 2

*	Versiyon 2'de VLSM desteği bulunur.
	*	**VLSM** (Değişken Uzunluklu Alt Ağ Maskeleri), adres alanının verimli kullanılmasını sağlar. Ayrıca, yönlendiricilerin yönlendirme bilgisi özetinden yararlanmasına imkan veren hiyerarşik IP adreslemesini de sağlar.

*	Versiyon 2'ye geçiş yapmak için;

    	> router rip
    	> version 2
    	> no auto-summary
    	> do wr
    	> do reload
	*	"**do wr**" ile hafızaya yazdırılır. Kalıcı olarak *"save"* edilir.
	*	**"do reload"** ile yeniden başlatır. Böylece yapılan *update* işlenir.

**RIP'i Kapatmak İçin**

	> no router rip
komutu kullanılır.	



---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)