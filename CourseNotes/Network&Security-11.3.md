# NETWORK & SECURITY

## Part - 11.3
----

	Cisco Packet Tracer kullanılmıştır.

## SWITCHING

### Intervlan Routing

![Intervlan_Routing_1](https://user-images.githubusercontent.com/63460173/185143683-4214338e-392a-4d65-8814-5667e4758260.png)

*	Switch0'ın gig0/1 interface'i ile Router0'ın fa0/0 interface'i arasında bulunan bağlantı Switch0'a bağlı olan bütün Vlanların geçtiği noktadır.
*	Switch'ten gelen bağlantı Router'ın fa0/0'ında verilen IP adresi (default) ile dışarı çıkabilir. Fakat Vlanlar birbirlerinden farklı olduğu gibi bir de barındırdıkları network'ler de farklıdır. Dolayısıyla birinin network ID'si bu default IP'ye verilirse network ID'leri faklı olduğu için diğerleri o hattı kullanamazlar.
*	Bu durumda Router0 ile Switch0 arasındaki yer bir boru hattı gibi düşünülür. Ana boru içerisinden 3 farklı küçük boru geçirebilirsek bu sahip olduğumuz 3 farklı Vlan ve Network aynı hattı kullanarak çıkış yapabilir.
*	İşte bu **3 küçük boru** interface'in altı, yani ***subinterface*** olarak adlandırılır.
*	Bu subinterfaceler **8 bitlik** ***shrink*** adı verilen (aynı zamanda vlan tag'ı da denir) extension'ı veri üzerinden okuyarak **hangi verinin hangi vlan'dan geldiğini anlar**.
*	Bu okumayı yapabilmesini sağlayan **encapsulation protokolünün** adı da **Dot1Q**'dur.
*	Switchler **dot1q** ile çalışır. O yüzden bu 8-bitlik okuma yeteneğine sahiptirler.
*	Subinterface'lere Switch'ten gelen paketleri **normal MTU Size (1500 mb)** olarak değil **12008** olarak işle denmiş olur.

**Konfigürasyon**

*	Router üzerinde

		> int fa0/0.10
		> encapsulation dot1q 10
		> ip add 192.168.10.1 255.255.255.0

*	**> int fa0/0.10**
	*	Vlan 10 için bir Subinterface oluşturduk.
*	**> encapsulation dot1q 10**
	*	Bu komut ile oluşturulan Subinterface'in Vlan 10 için olduğunu öğrettik.

*	**> ip add 192.168.10.1 255.255.255.0**
	*	Ve Vlan 10'un barındırdığı IP'ler için default bir IP atamsı gerçekleştirdik.


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)