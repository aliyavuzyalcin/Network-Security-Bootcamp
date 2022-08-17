# NETWORK & SECURITY

## Part - 11.3.1
----

	Cisco Packet Tracer kullanılmıştır.

## SWITCHING

### Intervlan Routing with VTP & Etherchannel (Layer 3 Switch)

![Intervlan_Routing_2](https://user-images.githubusercontent.com/63460173/185140666-13ceb0ee-aae0-46a6-a62d-951f94d3257f.png)

*	Network'te oluşan **bottleneck**leri yani **yoğun-darboğazları** güçlendirmek amacıyla kullanılan teknolojiye ***Link Aggregiation*** denir.
*	Bu teknolojinin Cisco tarafınaki isimlendirmesi ise **Etherchallenge**'tır.
*	Birden fazla **Link (bağlantı)**'i tek bir Link'miş gibi yönetebiliriz.
*	Çok büyük network'lerde bütün Vlanları bütün Switchler üzerinde teker teker açmak çok zordur.
*	Bunu kolaylaştırmak için ***VTP*** teknolojisi kullanılır.
*	**Trunking** yapıldıktan sonra bir ***VTP*** domaini oluşturulur.
*	**VTP** domainine ***PASSWORD*** verilir ki güvenli olsun.
*	**VTP mode**'ları seçilir;
	*	Server/Client
	*	Transparent

*	Server yapılan makineden Vlan basıldığı zaman basılan o Vlan Switch üzerinde **replike** olabilir.
*	Yani merkezi olarak Vlan yönetimi gerçekleştirilebilir.

### Etherchallange Config:

*	***STEP-1***

*	Multilayer Switch0

		> en
		> conf t
		> int range fa0/1-4
		> channel-group 1 mode desirable
	*	***> channel-group 1 mode desirable***
		*	Port-channel 1 oluşturuldu.

*	***STEP-2***
*	Multilayer Switch1

		> en
		> conf t
		> int fa0/1-4
		> channel-group 1 mode desirable
		
	*	***> channel-group 1 mode desirable***
		*	Port-channel 1 oluşturuldu.

*	***STEP-3***
*	Multilayer Switch0

		> int po1
		> switchport mode trunk  (ÇALIŞMADIĞINI GÖRDÜK)
		> switchport mode dynamic desirable (ÇALIŞIR HALE GETİRDİK)
		> switchport mode trunk
	*	***> int po1***
		*	Port-channel interface (po), channel-1 olduğu için **po1**'dir.

*	***STEP-4***
*	Multilayer Switch1

		> int po1
		> switchport mode dynamic desirable
		> switchport mode trunk

*	***STEP-5***
*	Multilayer Switch1

		> int fa0/5
		> switchport mode dynamic desirable
		> switchport mode trunk

*	***STEP-6***
*	Switch0

		> en
		> conf t
		> int fa0/1
		> swithport mode trunk



---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)