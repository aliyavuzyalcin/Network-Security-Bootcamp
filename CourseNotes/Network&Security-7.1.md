#NETWORK & SECURITY

##Part - 7.1
----

	Cisco Packet Tracer kullanılmıştır.

##OSPF (Open Shortest Path First)

###Basic Configuration

	> router ospf 1

*	Komutu ile OSPF başlatılır. Buradaki **"1"** ifadesi OSPF prosesini daha küçük parçacıklar halinde yönetmeyi sağlar.
*	Örneğin; İstanbul'un bir veri merkezi olduğunu düşünürsek Ankara ve İzmir iki farklı müşteri olacaktır. Eğer bu iki farklı alıcıyı **aynı process**'in altında yani **"ospf 1"**in altında toplarsak ***">no ospf 1"*** yazdığımız takdirde iki tarafın da bağlantısı kopacaktır.
*	Halbuki **İstanbul-Ankara** arasını **"ospf 1"**, **Istanbul-Izmir** arasını da **"ospf 2"** yapsaydık ***">no ospf 1"*** yazıldığı zaman sadece **Istanbul-Ankara** arası kopacaktır. Dolayısıyla **"process 1"** ve **"process 2"** olarak ayrılmış olurlar.
*	Farklı process'e bağlı cihazlar birbirleriyle **"routing table"** değişimi yapabilirler.
*	***">router ospf 1"*** yazdıktan sonra network ayarları yapılır;

		> network 11.0.0.0 0.0.0.3 area 0
		> network 15.0.0.0 0.0.0.3 area 0
		> network 172.16.0.0 0.0.255.255 area 0

*	**11.0.0.0** networkünü anons ettik. Çünkü İstanbulla (11.0.0.0'ın diğer tarafı) komşuluk ilişkisi kurduk.
*	**15.0.0.0** networkünü anons ettik. Çünkü İzmir ile (15.0.0.0'ın diğer tarafı) komşuluk ilişkisi kurduk.
*	**172.16.0.0** networkünü (Ankara iç networkü) anons ettik. Çünkü komşuları bu networke bir paket yollamak istedikleri zaman bunu öğrenmeleri gerekir.
*	***"0.0.0.3"*** ifadesi Subnet Mask'ın tersidir (revers).

>Örneğin: 11.0.0.0/30 subnet maskı 255.255.255.252'dir. Bunun tersi 0.0.0.3'tür. 255-252 = 3. Son okteti 255'e tamamlamak için 3 gerekir. Bunun için 3, 252'nin tersi durumunda olur.

*	**area 0** ifadesi haritalandırmak için kullanılır. Turkcell için Türkiye **area 0** iken, Azerbaycan **area 1**, Kazakistan **area 2** olabilir.
*	**area 0** merkez olmak zorundadır. ***area 1*** ile başlatılamaz.
*	**area 0**'a bağlantılı (komşu) olan *area*lar *routing table* değiştirebilir. Komşu olmayanlar ***"Virtual Link"*** olarak adlandırılan **router-id**'sine yapılan işlemle bu değişimi gerçekleştirir.
*	Bu ***area***ların sınırında oturan router'a ***"ABR (area border router)*** denir.
*	OSPF, komşuluk ilişkisinde karşı OSPF komşusuyla konuşmak için ***OSPF Router ID***'yi kullanır.
*	**Router ID**, cihazın üzerindeki ***en yüksek*** nümerik/sayısal değerli **Interface'indeki IP**'dir.
*	Fakat eğer **loopback** interface'i aktif ve **1.1.1.1** IP'si varsa router ID 1.1.1.1 olur. En yüksek numerik değer olmaz. ***Çünkü loopback önceliklidir.***
*	İki tane loopback varsa hangisi yüksekse o **Router ID** olur. 
*	**Loopback** yoksa **en yüksek IP'ye sahip interface** router ID olur.


###Loopback Atama

*	Loopback atamak için ***"> int lo0"*** komutu kullanılır.

		> en
		> conf t
		> int lo0
		> ip add 1.1.1.1 255.255.255.252
		> no sh

*	IP değişimlerinde (OSPF için) sistem sorun çıkartabilir. Bunun için OSPF process'i **"kill"** edilir ve yeniden başlatılır.

		 Önce kaydedilir.
		> do wr
		
		 Sonra OSPF process'i temizlenir;
		> do clear ip ospf process
		
		 Yine olmazsa yeniden başlatılır;
		> do reload

*	Networkte loopback varsa router onu tek bir IP ve Interface olarak kabul eder. Bunu engellemek içinse şu komut girilir;

		> int lo0
		> ip ospf network point-to-point


###Virtual Loopback Kurma

*	İzmir-Adana arası virtual link kurmak istesek;

		> area [Number] virtual-link [RouterID]

*	İzmir Router'ında ilgili config;

		> en
		> conf t
		> router ospf 1
		> area 1 virtual-link 1.1.1.1

	* **1.1.1.1** Adana router'ının loopback'i olduğu için router ID olarak bunu geçtik.
*	Adana Router'ında ilgili config;

		> en
		> conf t
		> router ospf 1
		> area 1 virtual-link 16.0.0.1

	*	**16.0.0.1** İzmir Router'ının nümerik olarak en yüksek değeri olduğu için Router ID olarak anons ettik.






---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)