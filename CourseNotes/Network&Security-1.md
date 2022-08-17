# NETWORK & SECURITY

## Part - 1
----

	Cisco Packet Tracer kullanılmıştır.

## Device OS Bilgileri

*	Cisco işletim sistemleri ***Unix*** tabanlı ve büyük-küçük harf duyarlıdır.
*	OS seviyesinde açılabilmesi için " ***> enable*** " komutu kullanılır.
*	Device'a ait temel konfigürasyon parametrelerini tasarlayabilmek için " ***> conf*** " komutu kullanılır.
*	Konfigürasyon terminaline erişebilmek için " ***> conf t*** " komutu kullanılır.
*	Device'ın ismini değiştirmek için " ***> hostname [HOSTNAME]*** " komutu kullanılır.
*	Cisco OS, girilen konfigürasyon parametrelerini iki dosyadan çeker;
	*	**Running Configuration** --> RAM üzerinde çalışan kısımdır. Kalıcı değildir. Cihaz aktif haldeyken kullanılır.
	*	**Start-up Configuration** --> Bu kalıcıdır. Kaydedilmiş konfigürasyonları barındırır.
*	Running Configuration dosyasını görebilmek için " ***> do show running-config*** " komutu kullanılır.
*	Start-up Configuration dosyasını görebilmek için " ***> do show startup-config*** " komutu kullanılır.
*	Running Config dosyasındaki bilgileri yani RAM üzerinde duran bilgileri kalıcı belleğe yani Startup Config dosyasına aktarmak için " ***> do wr*** " veya " ***> write memory*** " ya da " ***> copy running-config startup-config*** " komutları kullanılır.
*	Cihazlarda iki farklı "**password**" kullanılır;
	*	**Plain text (Düz metin)**
		*	Girilen parolayı düz metin olarak saklar.
		
			>enable password [YOURPASSWORD]

	*	**Encrypted text (Şifreli metin)**
		*	Girilen parolayı şifreleyerek(encrypt ederek) saklar.
		
				>enable secret [YOURPASSWORD]

*	Girilmiş veya saklanan **plaintext (düz metin)** olan parolaları şifrelemek içinse;
			
		>service password-encryption
*	Verilen şifreleri kaldırmak içinse;

		>no enable password

	YA DA	
		

		>no enable secret

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)