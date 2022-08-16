#Network & Security Bootcamp
---

![Bitirme_Projesi](https://user-images.githubusercontent.com/63460173/184718681-2bc58482-7f9b-46ac-9b3d-2caf7ff22552.png)


> ***Yapılan işlemlerin detaylarını proje dosyalarında bulabilirsiniz.*** 

*	**1.ADIM**
	*	IPv4 atamaları end-device'lar için yapıldı.
	*	Cihazlar üzerinde *gateway* ayarlandı.
	*	Cihazlar üzerinde *DNS* atamaları yapıldı.
	*	IPv6 atamaları end-device'lar için yapıldı.
	*	Cihazlar üzerinde *gateway* ayarlandı.
	*	Cihazlar üzerinde *DNS* atamaları yapıldı.

*	**2.ADIM**
	*	Tüm router'larda ***hostname*** yeniden ayarlandı.
	*	Tüm router'larda ***secret*** aktif hale getirildi ve şifre ***cisco*** olarak belirlendi.
	*	Tüm router'larda ***password-encryption*** servisi aktif hale getirildi.
	*	Router'larda interface IP'leri ayarlandı.

*	**3.ADIM**
	*	İstanbul Switch'inde ***Layer 2*** düzenlemeler yapıldı.
	*	Vlanlar oluşturuldu; ***Vlan 4*** ve ***Vlan 6***
	*	***Access*** ve ***Trunk*** portlar belirlendi.
	*	Kullanımda olmayan portlar kapatıldı.
	*	Tüm portlar için ***Port-security*** ayarları yapıldı.
*	**4.ADIM**
	*	İstanbul Router'ında **Subinterface**'ler açıldı.
	*	Subinterface fa0/0.4
	*	Subinterface fa0/0.6

*	**5.ADIM**
	*	Ping kontrolleri yapıldı.

## PROJE-1 Static Routing

*	**6.ADIM**
	*	İstanbul'dan İzmir'e ***Static route*** yazıldı.
	*	İstanbul'dan Ankara'ya ***Static route*** yazıldı.
	*	İzmir'den İstanbul'a ***Static route*** yazıldı.
	*	Ankara'dan İstanbul'a ***Static route*** yazıldı.
*	**7.ADIM**
	*	***Access-List*** kuralı oluşturuldu. 
	*	İstanbul router'ında ***IPv4/IPv6 Port Base Access-List*** kuralları oluşturuldu.

*	**8.ADIM**
	*	Gerekli testler yapıldı.


## PROJE-2 OSPF

*	**6.ADIM**
	*	İstanbul Router'ından Ankara Router'ına OSPF konfigüre edildi.
	*	İstanbul Router'ından İzmir Router'ına OSPF konfigüre edildi.
	*	İzmir Router'ından İstanbul Router'ına OSPF konfigüre edildi.
	*	Ankara Router'ından İstanbul Router'ına OSPF konfigüre edildi.
	*	İstanbul-Ankara arasında ***Authentication*** kuralı yazıldı.
	*	Tüm routerlar arası ***hello-interval*** ve ***dead-interval*** kuralları yazıldı.

*	**7.ADIM**
	*	***Access-List*** kuralı oluşturuldu. 
	*	İstanbul router'ında ***IPv4/IPv6 Port Base Access-List*** kuralları oluşturuldu.

*	**8.ADIM**
	*	Gerekli testler yapıldı.


---

@author [Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 
