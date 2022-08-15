#NETWORK & SECURITY

##Part - 8
----

	Cisco Packet Tracer kullanılmıştır.

##EIGRP (Interior Gateway Routing Protocol - Dahili Ağ Geçidi Yönlendirme Protokolü)

*	Cisco Native olmalıdır. Yani ilgili networkteki tüm router'lar Cisco olmalıdır.
*	Tüm routerlar OSPF gibi bir veritabanı (database) oluşturmaz. Aksine tüm routerlar sahip oldukları **network bilgilerini** diğer **tüm routerlar** ile **sürekli** olarak paylaşırlar.
*	Bir topoloji tablosu (topology table) tutarlar.
*	Olası tüm hatlar bu topoloji tablosu içerisinde yer alır.
*	***Load Balancing*** özelliği vardır. Paket paket gönderilmek istenir ve **eş-topoloji** söz konusuysa (üçgen bir topolojinin her bir köşesinde router olduğunun farz edilmesi gibi) paketlerden biri bir yoldan diğeri ise diğer yoldan hedefe iletilir. Yani, sürekli aynı hattı kullanmak yerine belirli miktarını A yolundan belirli bir miktarını da B yolundan iletir. Buna **load balancing** denir.
*	Bu işlemi paket paket yapmak zorunda da değildir. Bütün tam bir veriyi de yine bu şekilde dağıtarak yollayabilir.
*	Oluşturulmuş olan topolojiyi görmek için:

		> do show ip eigrp topology

komutu kullanılır.

*	Komşu routerların kendisine bakan interface'lerinin IP'lerini görebilmek için;

		>do show ip eigrp neighbors

komutu kullanılır.


						O
					 ISTANBUL
                    /        \
				   /          \
			      O	---------- O
		        Izmir 		  ANKARA

*	İstanbul'un İzmir interface'i -> s0/0/1
*	İstanbul'un Ankara interface'i -> s0/0/0
*	İzmir'in İstanbul interface'i -> s0/0/0
*	İzmir'in Ankara interface'i -> s0/0/1
*	Ankara'nın İstanbul interface'i -> s0/0/0
*	Ankara'nın İzmir interface'i -> s0/0/1

**İzmir ile EIGRP yapılandırmasına başlayalım**

	> en
	> conf t
	> router eigrp 100
	> no auto-summary
	> network 13.0.0.0 0.0.0.3  ---> İzmir-İstanbul yolu
	> network 15.0.0.0 0.0.0.3  ---> İzmir-Ankara yolu
	> network 10.0.0.0 0.255.255.255 ---> İzmir'in kendi iç (local) networkü

**İstanbul ile EIGRP yapılandırması**

	> en
	> conf t
	> router eigrp 100
	> no auto-summary
	> network 13.0.0.0 0.0.0.3  ---> İstanbul-İzmir yolu
	> network 11.0.0.0 0.0.0.3  ---> İstanbul-Ankara yolu
	> network 192.168.1.0 0.0.0.255 ---> İstanbul'un kendi iç (local) networkü

**Ankara ile EIGRP yapılandırması**

	> en
	> conf t
	> router eigrp 100
	> no auto-summary
	> network 11.0.0.0 0.0.0.3  ---> Ankara-İstanbul yolu
	> network 15.0.0.0 0.0.0.3  ---> Ankara-İzmir yolu
	> network 172.16.0.0 0.0.255.255 ---> Ankara'nın kendi iç (local) networkü

*	***> no auto-summary*** ifadesi IP'nin kendi class'ına göre değil kendi belirlemiş olduğum *design pattern*'lerine göre çalışmasını istemektir.
*	***> router eigrp 100*** ifadesinde *"100"* ID'yi ifade eder. Diğer routerlar da bu ID ile EIGRP yapılandırmasını başlatır. Böylece aynı ağ altında olurlar.

###EIGRP Authentication

*	Bir anahtar seti kullanır. (key chain)
*	**"> conf t"** yazıldıktan sonraki ***global config*** alanında düzenlemeler yapılır.

		> en
		> conf t
		> key chain EIGRP-KEYS
		> key 1
		> key-string cisco
		> exit
		> int s0/0/1
		> ip authentication key-chain eigrp 100 EIGRP-KEYS
		> ip authentication mode eigrp 100 md5

*	**"> key chain EIGRP-KEYS"**
	*	**key chain** (ahatarlık) oluşturup adına **EIGRP-KEYS** dedik.

*	**"> key 1"**
	*	**key chain**'e (anahtarlığa) anahtar ***(key 1)*** taktım.

*	**"> key-string cisco"**
	*	**Key**'in (anahtarın) ***"cisco"*** olduğunu vurguluyorum.

*	**"> exit"**
	*	***key configuration***'dan çıkıyorum.
*	**"> int s0/0/1"**
	*	interface s0/0/1'e (İstanbul-İzmir) giriyorum.
*	**"> ip authentication key-chain eigrp 100 EIGRP-KEYS"**
	*	IP düzeyinde *authentication* kullanılacağı için ***"key-chain"*** kullanılacağını,
	*	EIGRP 100 domaini için ***EIGRP-KEYS*** olduğu vurgulanır.
	*	***EIGRP-KEYS*** yerine iki farklı müşterimiz olsaydı **KOÇ** ve **SABANCI** gibi, birisine **KOC** diğerine de **SABANCI** ilişkilendirilmesi yapılacaktı. 
	*	Yani **EIGRP-KEYS** yerine **KOC** diğeri için de **EIGRP-KEYS** yerine **SABANCI** yazılacaktı.

*	**> ip authentication mode eigrp 100 md5**
	*	IP authentication mode'un EIGRP 100 domaini için md5 hashing algoritmasını devreye sokuyorum.
	*	md5 değil de SHA-1, SHA-3 de olabilir.

> AYNI İŞLEMLER KARŞI INTERFACE'DEKİ ROUTER İÇİN DE YAPILIR. BÖYLECE UÇTAN UCA **AUTHENTICATION** SAĞLANMIŞ OLUR.

 
---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)