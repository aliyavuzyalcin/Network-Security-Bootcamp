#NETWORK & SECURITY

##Part - 11.3.3
----

	Cisco Packet Tracer kullanılmıştır.

##SWITCHING

###PORT SECURITY

[Resim: Port-security]

*	Data dışarıdan olabildiği gibi içeriden de (özellikle içeriden) manipülasyona uğratılıp zarar görebilir.
*	Bunun önüne geçebilmek için **switch portlarına** hakim olunmalıdır. Bu durum network seviyesinde fiziksel güvenliğimizin ilk katmanını oluşturur.
*	**Switchport port-security** komutu ***dynamic portlar*** üzerinde gerçekleşmez. Yani, **mode access**'e alınmalıdır. Daha sonra teknolojiyi devreye alabiliriz.
*	Eğer **mode access**'e almayı unutursak ***command reject*** hatası alınacaktır.
*	Port-security'nin amacı portları farkındalıkla yönetmektir. 
*	Açık olması gereken portlar dışında hepsini kapatmak önem arz eder.
*	Şekilde fa0/1-4 portları kullanımdadır. Dolayısıyla **fa0/5-24** arasındaki **portlar** boş olduğundan **kapatılmalıdır.**

		> int range fa0/5-24
		> sh
		> int range g0/1-2
		> sh

*	Aynı zamanda portlarla alakalı bazı spesifik özelikleri belirler.
*	Bunlardan biri **port-security'nin maximum** özelliğidir.
*	1 Switch 5000'e yakın **MAC** adresini **1 portu** üzerinde tutabilir. Fakat **KaliLinux**'ta bulunan bir *tool* ile o porta **saniyede 25.000 MAC** basılır.
*	Dolayısıyla **Switch** üzerindeki bu **MAC** tablosu sürekli yenileniyor. Bu durumda tüm kaynakların switch üzerinde bu noktaya yönlenmesine neden olur. Bu da **Denial of Service** olarak sonuçlanır.
*	Portun gerçek sahibi kaç taneyse **maximum** değer ona göre belirlenir.
*	Bunun da **best practice**'i *"1"* değeri olacaktır. Yani yalnızca 1 gerçek sahibi olabilir.
*	Ama örneğin yönetim kurulu 12 kişiden oluşuyorsa toplantı odasında her porta 12 tane MAC'i **static** olarak vermemiz gerekir.
*	**Static MAC**, spesifik olarak cihazın üzerinde bulunan **ethernet kartının** *fiziksel adresi* olan **MAC Adresi**dir.
	*	CMD üzerinden **">ipconfig /all"** komutuyla buna ulaşabiliriz.

*	Yani o **belirli portlarda** çalışmasını istediğimiz **belirli cihazların** **yalnızca MAC Adresleriyle** çalışmasını sağlamaya **STATIC MAC** denir.
*	**Sticky** özelliği ise yapmış olduğumuz konfigürasyonu ***ilk*** kendisine bağlanan cihaz neyse onun MAC'ini kullanmak üzere konfigüre eder.
*	Bu sırada aradaki ilişki **maximum** değeriyle de tutuluyor. **12 kişilik** bir odada konfigürasyon yapılıyorsa **her porta maximum 12** değeri verilip ya ***"statik"*** olarak hepsini teker teker MAC adresi olarak yazmak gerekir. Güvenli olması için.
*	Ya da **operasyonel zorluk ve aciliyet varsa** *Sticky* özelliği de kullanılabilir.
*	Switchport **port-security** yapısı **"trunk"** portlarda çalışamaz. **Access** portlarda çalışır.
*	Eğer portun özelliğini **access**'e çekemezsek **command reject** olur.
*	Dolayısıyla **switchport mode access** sonrası çalıştırılmalıdır.
*	Sonrasında **switchport port-security** komutu *yalın* olarak yazılmalıdır.
*	**Violation** değerleri anomali ortaya çıktığında sistemin nasıl tepki vereceğini belirtir.
*	Çeşitleri;
	*	sh (shutdown)
	*	sh vlan (shut vlan)
	*	protect
	*	restrict

*	Violation'ın default response değeri **"sh"**'dir.
*	**"sh"**'nin daha sonrasında bir administrative yükü olur. Admin'in gelip oradaki portu **"sh"** edip **"no sh"** ile tekrar açması/devreye alması gerekir.
*	Bunun bir eksiklik olduğunu fark edip daha sonra **protect** ve **restrict** özelliği ortaya kondu.
*	**Protect** ve **restrict** ise normal trafiği analiz ederken **"forward state"**e geçerek karşı tarafa paketi yolluyor. **Anomali** tespit ettiği anda portu **sh state**'e ***geçirmiyor***, sadece **forwarding state**'e sokmuyor.
*	Yani paketi iletmeyi reddediyor.
*	Switchler birbirleriyle konuşurken Switch0, Switch1'in fa0/2 portundaki MAC değerini kendi fa0/1'ine yazıyor. Switch1 ise Switch0'ın fa0/1'deki MAC değerini kendi fa0/2'ye yazıyor. Switching bu şekilde gerçekleştirilir.
*	**Switch0 üzerinde:**

		> en
		> conf t
		> int fa0/2
		> switchport mode access
		> switchport port-security
		> switchport port-security maximum 2
		**Maximum 2 demek en fazla 2 MAC adresini kabul et demektir. Fazla olursa **shutdown** eder.**
		***port kapandıktan sonra açmak için***
		> sh
		> no sh
		> no switchport port-security (Kaldırma komutu. İstenirse kaldırılabilir.)


###STATIC MAC'ing

*	Çalışmasını istediğimiz Access Device'ın MAC'ini kopyalıyoruz.

*	Switch-1'e konfigürasyon:

		> en
		> conf t
		> int fa0/2
		> switchport mode access
		> switchport port-security
		> switchport port-security maximum 1
		> switchport port-security violation restrict
		> switchport port-security mac-address [DEVICE_MAC_ADDRESS] --> Yalnızca bu MAC çalışacaktır.

		> int fa0/3
		> switchport mode access
		> switchport port-security
		> switchport port-security maximum 1
		> switchport port-security violation restrict
		> switchport port-security mac-address sticky



---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)