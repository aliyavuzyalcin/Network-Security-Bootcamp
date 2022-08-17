# NETWORK & SECURITY

## Part - 7.2
----

	Cisco Packet Tracer kullanılmıştır.

## OSPF (Open Shortest Path First)

### OSPF Authentication

*	İki komşu aralarında (veya tüm komşular arasında) **hello** ve **dead** **interval**lar gönderirler.
*	***Hello Interval***
	*	Birbirlerine *"hello"* paket yollarlar. Böylece hangi hattın *"up"* hangi hattın *"down"* olduğunu öğrenirler. 4 defa 10'ar saniyelik aralarla Hello paket gönderilir. Dördüne de cevap alınamazsa 40. saniyede **dead interval** gönderilir ve komşuluğun aktif olmadığı anlaşılır.
	*	Hello Interval 10 saniyedir. 
	*	Dead Interval 40 saniyedir.
	*	4x10 şeklinde olup eğer 4 tane hello paketine cevap gelmezse komşuluk bozulur.

**Az Güvenli Authentication Metot**
---
	> int s0/0/0
	> ip ospf authentication
	> ip ospf authentication-key [PASSWORD]

**Daha Güvenli Bir Metot**
--
	> en
	> conf t
	> int s0/0/1
	> ip ospf authentication message-digest
	> ip ospf message-digest-key 1 md5 [PASSWORD]

*	***> ip ospf authentication message-digest***
	*	Mesajlar karılarak karşıya iletilecek demektir. Bir poker kartlarının karılması gibi.

*	***> ip ospf message-digest-key 1 md5 [PASSWORD]***
	* ***key 1*** için (2,3,4 key olabilir) **md5** ile hashlenerek ***"PASSWORD"*** parolasıyla işlemleri **encrypt** olarak yap ifadesidir.

### Hello & Dead Interval Configuration

*	Hello ve Dead interval eşit olmazsa komşuluk gerçekleşmez.
*	Bir tarafta hello interval 10 verildiyse diğer tarafta da yine aynı şekilde hello interval 10 verilmelidir.
*	Bunun için **Hello** ve **Dead Interval** *time*'ları parametre olarak **router**'lara geçilmelidir.

		> en
		> conf t
		> int s0/0/1
		> ip ospf hello-interval 11
		> ip ospf dead-interval 44

*	Aralarında "x4" ilişki vardır. Çünkü 4 adet **hello** paketi gider. Bu nedenle ***" 4 x 11 = 44 saniye Dead Interval olmalıdır."***


### OSPF Çalışma Metotu

*	Ağda bir değişiklik olduğu zaman güncelleme paketi (LSA- Link State Advertisement) yayınlanır.
*	Bu paket tüm komşulara iletilir. Her yönlendirici kendi LSDB (Link State Database) günceller.
*	Böylece her komşu ağ bilgilerini alır ve LSDB ile en kısa yol hesap edilir.
*	İletişimi **Router ID** ile yapar; router'ın interface'lerinden aktif olan ***en yüksek IP*** adresidir.
*	Ancak ***loopback*** varsa o önceliklidir ve ***Router ID*** o ***loopback*** olur.
*	**Hello Interval** 4 defa gönderilir. (10 saniye)
*	**Dead Interval** ise topla 4 * 10 = 40 saniyedir.

### OSPF Hiyerarşik Yapısı

*	OSPF bir **kral** seçer. Buna **DR** yani **Designated Router** denir.
*	Bir de **back-up** (yedek) router seçilir. Buna da **BDR** yani **Back-up Designated Router** denir.
*	Her router kendi **nümerik olarak en yüksek IP**'sini seçer ve onu **Router ID** olarak belirler.
*	**OSPF PAKETLERİ**
	*	Hello Interval Paketleri
	*	Dead Interval Paketleri
	*	Network Anonsu
	*	Router ID yer alır.

*	Bu paketler tüm routerlardan alınıp birbirlerine dağılınca **ID**'lerden **en düşüğü "KRAL"** yani **Designated Router** seçilir.
*	Herkes bir database oluşturulması amacıyla tüm **root**ları bu **kral**a yani **Designated Router**a aktarır.
*	Böylece **tüm network, router'lar ile paylaşılmış olur.**

### ÖZETLE

*	OSPF, Link State protokoldür. Dynamic routing altında kategorilendirilir.
*	Link State protokolü olmasından dolayı yol bilgisini hızlı öğrenir. 
*	Büyük-karmaşık ağlarda iyi çalışır ve güvenilirdir.
*	Sınıfsız (classless) bir yapıya sahiptir.
*	VLSM (Variable Length Subnet Masking) ve Supernetting destekler. Daha iyi adresleme yapılır.
*	Ağ üzerine alınan yük sunuculara eşit dağıtılır. (Load Balancing)
*	AD (Administrative Distance) değeri 110'dur.
*	"Area" değeri önemlidir.

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)
 