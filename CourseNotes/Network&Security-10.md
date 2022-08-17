# NETWORK & SECURITY

## Part - 10
----

	Cisco Packet Tracer kullanılmıştır.

## ROUTE REDISTRIBUTION

*	Çoklu protokol çevreleri ortak bir çatı altında toplanır.
*	Bir router kendisine bağlı her biri farklı protokollü 5 farklı routerı birbirine bağlar.
*	Bu işleme **router redistribution** denir.
*	Ortada bulunur. ***Router0*** kendisine bağlı **5 ayrı routerı** birbirine bağlar.
*	Bu **5 ayrı router** üzerinde bulunabilecek **protokoller**;
	*	OSPF
	*	BGP
	*	RIP-RIPv2
	*	EIGRP
	*	STATIC olarak sayılabilir.

*	Bu protokollerin birbirleriyle konuşmalarını öğretmemiz gerekir.
*	Bunu yapacak olan router'da ortadaki yani **"Router0"** dır.

**ÖRNEK TOPOLOJİ**

![Route_Redistribution](https://user-images.githubusercontent.com/63460173/185138085-f4787dde-ddcc-45bb-93f2-e7151d5462b1.png)


**İŞLEMLER**

***STEP-1***

*	*EIGRP*

*	Router0
	
		> en
		> conf t
		> router eigrp 100
		> no auto-summary
		> network 15.0.0.0 0.0.0.3
		> ex
*	Router5

		> en
		> conf t
		> router eigrp 100
		> no auto-summary
		> network 15.0.0.0 0.0.0.3
		> network 192.168.5.0 0.0.0.3

***STEP-2***

*	*BGP*

*	Router0

		> router bgp 100
		> neighbor 11.0.0.2 remote-as 200
		
*	Router1

		> router bgp 200
		> neighbor 11.0.0.1 remote-as 100
		> network 192.168.1.0 mask 255.255.255.252

***STEP-3***

*	*RIP*

*	Router0

		> router rip
		> version 2
		> no auto-summary
		> network 12.0.0.0
		
*	Router2

		> router rip
		> version 2
		> no auto-summary
		> network 12.0.0.0
		> network 192.168.2.0
		
***STEP-4***

*	*STATIC*

*	Router0

		> ip route 192.168.3.0 255.255.255.252 13.0.0.2

*	Router3

		> ip route 0.0.0.0 0.0.0.0 13.0.0.1

***STEP-5***

*	*OSPF*

*	Router0

		> router ospf 1
		> network 14.0.0.0 0.0.0.3 area 0
		
*	Router4

		> router ospf 1
		> network 14.0.0.0 0.0.0.3 area 0
		> network 192.168.4.0 0.0.0.3 area 0

> ***BÜTÜN BİLGİLER ROUTER0'DA TOPLANDI. ŞİMDİ PROTOKOLLERİN DAĞITIMINA BAŞLANIR.***

***STEP-1***

*	*RIP DAĞITIMI*
*	*RIP, BGP ile bağlantı kuramaz.*

*	Route0

		> router rip
		> redistribute ospf 1 metric 1
		> redistribute eigrp 100 metric 1
		> redistribute static metric 1

***STEP-2***

*	*BGP DAĞITIMI*
*	*BGP, RIP ile bağlantı kuramaz.*

*	Route0

		> router bgp 100
		> redistribute ospf 1
		> redistribute eigrp 100
		> redistribute static


***STEP-3***

*	*OSPF DAĞITIMI*

*	Router0

		> router ospf 1
		> redistribute eigrp 100 subnets
		> redistribute rip subnets
		> redistribute bgp 100 subnets
		> redistribute static subnets

***STEP-4***

*	*EIGRP DAĞITIMI*
*	Router0

		> router eigrp 100
		> redistribute bgp 100 metric 100 10 125 125 1500
		> redistribute ospf 1 metric 100 10 125 125 1500
		> redistribute rip metric 100 10 125 125 1500
		> redistribute static metric 100 10 125 125 1500



***redistribute bgp 100 metric 100 10 125 125 1500***

*	**100**
	*	100 mb Bandwidth kullanılacak.

*	**10**
	*	10 milisaniye Delay olacak.
	
*	**125**
	*	Bu network 1 milyar defa mı kopar yoksa hiç mi kopmaz? 
	*	255 hiç kopmaz.
	*	0 sürekli kopar.
	*	125 ara bir değerdir.
	
*	**125**
	*	Bu networkte **load** ne kadar?
	*	255 çok dolu.
	*	0 boş.
	*	125 ara bir değerdir.
	
*	**1500**
	*	**MTU**, *Maximum Transmission Unit*
	*	Her zaman 1500 mb'dir.

> ***BURADAKİ DEĞERLER RASTGELE VERİLMİŞTİR. GERÇEK SİSTEMLERDE GERÇEK DEĞERLER NEYSE O VERİLMELİDİR.***

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 

