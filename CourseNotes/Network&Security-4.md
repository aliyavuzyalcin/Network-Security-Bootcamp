#NETWORK & SECURITY

##Part - 4
----

	Cisco Packet Tracer kullanılmıştır.

##Statik Yönlendirme (Static Routing)

*	Direkt olarak bağlı olmayan uzak networklerin "**Routerlara**" tek tek öğretilmesi işlemidir.
*	Küçük ölçekli networklerde yaygındır.
*	Büyük ölçekli ağlarda kullanılması zordur. Routing tablosunun sürekli manuel olarak yapılandırılması gerekmektedir.

*	İki türlü hata mesajı vardır;

		Destination host is unreachable
	*	Bir cihaz başka bir cihaza erişmek istiyor fakat **onun adresini kendi routing tablosunda bulamıyorsa** alacığı hata mesajıdır.

			Request timeout

	*	Bir cihaz başka bir cihaza erişmek ister ve onu kendi *routing tablosu*nda bulur. Mesajı gönderir fakat alıcı cihaz kendisine gelen bu mesajın gönderenini kendi *routing tablosu*nda bulamazsa gönderici cihazın alacağı hata mesajıdır.
	
>**Özetle;**
>
> Sorun **gönderici** cihazda ise hata mesajı ***"Destination host is unreachable"*** dır.

> Sorun **alıcı** cihazda ise hata mesajı ***"Request timeout"*** olur.


###Router'a Uzak Networkü Öğretme İşlemi (Static Routing);

    > en
    > conf t
    > ip route [Gidilmesi İstenen IP][IP'nin Subnet Maskı][Router Dış Bacak IP'si (alıcı)]

***ÖRNEK***

    > en
    > conf t
    > ip route 192.168.1.0 255.255.255.0 11.0.0.1

*	ifadesi; **192.168.1.0** *networküne* gelen paketleri **11.0.0.1** dış bacak IP'li router'a ver demektir.

##Default Route

    > ip route 0.0.0.0 0.0.0.0 13.0.0.1

*	ifadesi **kendi network'ü** hariç ***herhangi bir uzak network'ün subnet mask***'ı ne olursa olsun **13.0.0.1**'e ver demektir.

**Yazılan IP Route'larını Görmek için;**

    > do show ip route
komutu kullanılır.

**Ayarlanan IP Route'larını ***SİLMEK*** için ***">ip route"*** komutunun başına **"no"** koyulur.

	> no ip route 192.168.1.0 255.255.255.0 11.0.0.1

VEYA

	> no ip route 0.0.0.0 0.0.0.0 13.0.0.1

**--END OF DOCUMENT--**

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)