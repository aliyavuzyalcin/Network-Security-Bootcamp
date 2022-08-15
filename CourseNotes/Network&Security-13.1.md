#NETWORK & SECURITY

##Part - 13.1
----

	Cisco Packet Tracer kullanılmıştır.

###Access Control Lists

*	Erişim kontrol listelerinin oluşturulmasıdır.
*	Erişim listelerinin **yazılma sırası** ve **okunma sırası**, **hangi kuralın altta hangi kuralın üstte** olduğu çok önemlidir.
*	İki adımdan oluşur;
	*	Listenin oluşturulması,
	*	Listenin uygulamaya konması.

*	Ali'nin Galatasaray olduğu bir senaryoda eğer ilk adım için ***" Ali içeri girebilir "*** yazar ama ikinci adım için ***" Galatasaraylılar giremez "*** yazarsa *Ali içeri girebilir* fakat diğer *Galatasaraylılar giremezler*.
*	 Böylece erişime sahip olmasını istediğimiz kişiler için izin (*permit*) verildi.
*	 Bu izin (*permit*) listesinin en altında bir kural daha bulunur. Bu kural listede görünmez durumda olabilir. Ama kural şunu ifade eder;
	*	 ***Belirtilmiş, izin verilmişler hariç herkesi REDDET.***

*	Bu durum ***confidantially*** olarak yüksek olan **networkler**de geçerlidir.
*	İkinci bir network çeşidi ise ***ticari network***lerdir. 
	*	Örneğin; gittigidiyor.com, hepsiburada.com gibi.

*	Bu tür networkler her zaman daha fazla kişiyi alabilme kapasiteli olması gereken networklerdir.
*	Diğer adıyla **Erişim (Access)** ihtiyacı olan networklerdir.
*	Bu networklerde ise erişime sahip olmasını istedğimiz kişileri tek tek yazman yerine herkese izin verilir.
*	Fakat kötü amaçlı olanlar **yasaklı** listeye alınır. Yani **confidantial** networklerin tam tersi işlem yapılır.
*	Bir host'u *Access List* içerisinde kullanmak istersek onu **host ID**'si ile çağırırız.
	*	**> host 192.168.1.2**

*	Bir network'ü *Access List* içerisinde kullanmak istersek onu **Network ID**'si ve **Wildcard mask** ile çağırırız.
	*	**> 192.168.1.0 0.0.0.255** 	 *===> 192.168.1.0/24 demektir*.

*	4 adet erişim permütasyonu vardır;
	*	HOST >====ACCESS====> HOST
	*	HOST >====ACCESS====> NETWORK
	*	NETWORK >====ACCESS====> HOST
	*	NETWORK >====ACCESS====> NETWORK

*	Access List'ler 4'e ayrılır;
	*	***Access List, verilen ID'ye göre yapılandırılır.**
	
	*	**Standart ACL**
		*	0 ile 99 arasında nümerik bir değer alabilen erişim listesidir.
		*	ACL'nin adını 11 yaparsak bu ACL otomatik olarak *Standart ACL* olacaktır.

	*	**Extended ACL**
		*	100 ile 199 arasında nümerik bir değer alabilen erişim listesidir.

	*	**Named ACL**
		*	Numerik olmayıp ***String*** olan erişim listeleridir.

	*	**VLAN ACL**
		*	Vlanlar arasındaki trafiği kontrol eden ACL'dir.

	*	**IPv6 ACL**
		*	IPv6 için oluşturulan ACL'dir.


*	***SYNTAX***	

[RESİM: ACL-SYNTAX]

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)