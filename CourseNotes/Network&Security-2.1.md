#NETWORK & SECURITY

##Part - 2.1
----

	Cisco Packet Tracer kullanılmıştır.

## IP Adresi

*	Her biri ***"oktet"*** olarak adlandırılan ve uzunluğu 8 bit olan 4 oktet'ten oluşan 32 bit uzunluğunda bir mantıksal tanımlayıcıdır.


		192		.	168		.	1		.	1		/24	
		---			---		   ---		    ---
		8 bit 	+	8 bit	+   8 bit	+   8 bit		= 32 bit

	*	Daha detaylı incelersek;

    		192				.			168			.		1		 .		1	       /24
			11000000		.		10101000		.	00000001	.	00000001
			\------------------------------------------------------/\------------/	  \----/
							Networkü İfade Eder							Hostu 		  Subnet
																	  İfade Eder	   Mask
			Bu Binary'de (2'lik tabanda):
							192				.			168			          .				1		            .		         1	              /24
			--- --- --- --- --- --- --- --- | --- --- --- --- --- --- --- --- | --- --- --- --- --- --- --- --- | --- --- --- --- --- --- --- --- 
			2^7 2^6 2^5 2^4 2^3 2^2 2^1 2^0	. 2^7 2^6 2^5 2^4 2^3 2^2 2^1 2^0 . 2^7 2^6 2^5 2^4 2^3 2^2 2^1 2^0 . 2^7 2^6 2^5 2^4 2^3 2^2 2^1 2^0

*	**IP Sınıfları**
	*	A sınıfı
		*	İlk okteti ***1-127*** arasında olanlardır. İlk oktetin ilk biti her zaman ***"0"***dır.
		*	Subnet Mask'ı ***255.0.0.0*** dır.

	*	B sınıfı
		*	İlk okteti ***128-191*** arası olanlardır. İlk oktetin ilk iki biti ***"10"*** olarak ayarlanır.
		*	Subnet Mask'ı ***255.255.0.0*** dır.
	*	C Sınıfı
		*	İlk okteti ***192-223*** arasında olanlardır. İlk oktetin ilk üç biti ***"110"*** olarak ayarlanır.
		*	Subnet Mask'ı ***255.255.255.0*** dır.

*	Bazı IP adresleri özel kullanım için ayrılmıştır. Bunlar yerel ağlar (local networks) için kullanılır. BUnlara ***Private Ip*** denir.
	*	Örneğin;
		*	192.168.0.0 - 192.168.255.255
		*	172.16.0.0 - 172.31.255.255
		*	169.254.0.0 - 169.254.255.255
		*	10.0.0.0 - 10.255.255.255

##Subnetting/Subnet Mask

*	 IP adreslerini daha verimli kullanmak için kullanılır.
*	 Broadcast trafiğini azaltmak için kullanılır.
*	 Network'ü daha kolay yönetmek için kullanılır.
*	 Güvenlik sağlamak için kullanılır.

**Subnet Mask**; yani ***Alt Ağ Maskesi***, bir IP adresinin *hangi network*'te olduğunun belirlenmesi için kullanılan bir adrestir.

*	Subnet Mask 32 bitten oluşur.

**Subnet Mask ile IP adresinin**

	*	Network Adresini,
	*	Broadcast Adresini,
	*	Kullanılabilir İlk Adresini,
	*	Kullanılabilir Son Adresini
**tespit edebiliriz. Böylece kullanabileceğimiz IP'leri tespit edebiliriz.**

[Figure 1. IP-Subnetting]

*	Subnet Mask'ın **"1"**leri kadar olan kısım IP adresinin *Network* bilgisini verir.
*	Subnet Mask'ın **"0"**larının olduğu kısım ise *Host* bilgisini verir.

###Örnek
**-> IP; 192.168.1.10/24**

[Figure2. IP_Subnetting_Example]

*	Peki bulduğumuz sonuca göre bir Switch'e kaç tane end device bağlayabiliriz?
	*	Bu da son IP adresinin **1** eksiği ile bulunur.
	*	Yani;

			192.168.1.254 - 1 = 192.168.1.253

	*	Toplamda **253 cihaz** bağlanabilir.


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)

