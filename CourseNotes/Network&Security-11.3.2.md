# NETWORK & SECURITY

## Part - 11.3.2
----

	Cisco Packet Tracer kullanılmıştır.

## SWITCHING

### Intervlan Routing with VTP & Etherchannel (Layer 3 Switch)

![Intervlan_Routing_2](https://user-images.githubusercontent.com/63460173/185140666-13ceb0ee-aae0-46a6-a62d-951f94d3257f.png)

--> ***VTP (Virtual Trunking Protocol) Config***

*	VTP'nin çalışabilmesi için **trunking işleminin her yerde yapılmış ve tamamlanmış olması gerekir.**
*	Sonrasında bir VTP domain oluşturulup hatta basılır.
*	Önceki adımlardan devam ediyoruz:

*	***STEP-7***
*	*Multiswitch0*

		> vtp domain [NAME]	

	*	Ismi **name** olan VTP Domainini oluşturduk.

> ***VTP Domaini oluşturulup hatta basıldıktan sonra diğer cihazlarda (Switch) da bunun replike edilip edilmediğini kontrol et.***

*	***STEP-8***
*	*Multiswitch1*

		> do show vtp status

	*	VTP durumu kontrol edilir **"VTP domain name"** başlığı altında.
	*	Eğer başarıyla görüntüleyebildiysek **trunking doğru ve VTP çalışıyor demektir.**
	*	Dolayısıyla Multiswitch0'dan aşağıya Switch0'a Vlan basılabilir anlamına gelir.



*	***STEP-9***
*	*Switch0*

		> vtp mode client

	*	VTP mode'u **Client**'a çekildi.
	*	Merkezi **Server** olarak *Multilayer Switch0* ayarlanacağı için böyle yaptık.

*	***STEP-10***
*	*Multilayer Switch1*

		> vtp mode client

	*	VTP mode'u **Client**'a çekildi.

*	***STEP-11***
*	*Multilayer Switch0*

		> vtp mode server
		> vlan 10
		> vlan 20

	*	VTP mode'u **Server**'a çekildi.
	*	*Vlan 10*, *Vlan 20* Vlanlarını hatta bastık. 
	*	Switch0 üzerinde bu vlanları kontrol et.

*	***STEP-12***
*	*Switch0*

		> do show vlan

> ***Bu işlemler tamamlandıktan sonra oluşturulan Vlanların içerisine end device'ların access portları eklenir.***

*	***STEP-13***
*	*Switch0*

		> int fa0/2
		> switchport mode access
		> switchport access vlan 10
		> int fa0/3
		> switchport mode access
		> switchport access vlan 20

*	***STEP-14***
*	*Multilayer Switch0*

		> ip routing
		> int vlan 10
		> ip add 192.168.10.1 255.255.255.0
		> no sh
		> int vlan 20
		> ip add 192.168.20.1 255.255.255.0
		
	*	***> ip routing***
		*	Yazılmazsa cihaz kendisini routing'e açmaz.

*	***STEP-15***
*	*BİR END DEVICE'TAN*

		> ping 192.168.10.2
		 VEYA
		> ping -t 192.168.20.2

*	Layer 3 Switch olan Multilayer Switch'leri Router'a çevirmek için;

	*	Multilayer Switch 0'da yapılan config.
	*	Böylece IP layer 3 portu oluşturuldu.

		> int po1
		> no switchport
		> ip add 11.0.0.1 255.255.255.252

	*	Multilayer Switch 1'de yapılan config.
	*	Artık bir *switch portu* **olmadığını** bir router'ın **fa0/0**'ı gibi davranması gerektiğini ifade ediyoruz.

		> int po1
		> no switchport
		> ip add 11.0.0.2 255.255.255.252

	*	Kontrol gerçekleştiriyoruz.

		> do ping 11.0.0.1


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)