# NETWORK & SECURITY

## Part - 11.1
----

	Cisco Packet Tracer kullanılmıştır.

## SWITCHING

### VLAN

*	Portları kümeleme işlemidir.
*	Switch üzerinde konteyner görevi görür. Bazı portları belirli Vlanların altına aldığımızda o portlar kendi içlerinde konuşabilir; kendi dışındaki Vlanlar ile konuşamaz hale getirilir.
*	Yani faklı Vlanlar birbirleriyle konuşamaz.

### DOT1Q

*	Bir encapsulation protokolüdür.
*	Paketin (frame) oluşturulma şeklini belirler.
*	MTU size'ı 1500 ile bırakmayıp arkasına (sonuna) 8 bitlik bir extension daha koyar. Bunun adına da ***shrink*** denir.



	
**Vlan**, ***"> vlan"*** diye switch CLI'ında çağırıldığında içerisine *port contain* eden bir konteyner; ***"> interface vlan [NUMBER]"*** diye çağırıldığında IP verebildiğimiz bir **Layer 3** interface gibi davranır.

> ***Buna da SVI (Switch Virtual Interface) denir. Loopback ile hemen hemen benzerdir.***

*	İki tür **device** vardır;
	*	**Access Point Devices**
		*	Layer 7'ye kadar olan paket/data manipülasyonu yapabilen son kullanıcı cihazlarıdır. PC, Laptop vs.

	*	**Network Level Devices**
		*	Layer 2 veya Layer 3'e kadar olan paket yönlendirmelerinin yapılabildiği network cihazlarıdır. Switch, Router vs.

*	Eğer bir switch'in üzerinde tek bir **access device** varsa bu porta **Access Portu** denir. Bu porttan sadece ***1 Vlan'a*** trafik atılabilir.
*	Fakat bir switch'e başka bir switch veya router bağlı yani **Network Level device** bağlıysa buna **Trunk Port** adı verilir.
*	**Trunk Port** ile switch üzerindeki *tüm vlanların trafiği* bu port üzerinden geçebilir.
*	**Access Port** ile switch üzerindeki **sadece o porta ait vlan'ın trafiği** geçebilir.
*	***Vlan 1, default vlandır.*** *(administrative vlan, native vlan)*
*	***Vlan 1, vlan tag'ı açamaz.***
*	Başlangıçta tüm portlar *Vlan 1*"in altındadır. Böylece bütün cihazlar otomatik olarak (konfigürasyon gerekmeden) bağlantı gerçekleştirirler. Bu default olarak Cisco cihazlar üzerinde gelir.
*	Vlan 1 başka bir Vlan'a **root edilemez.**
*	Fakat mesela Vlan 10, Vlan 20'ye **root edilebilir.**


### Bir Vlan Oluşturmak İçin

*	Switch üzerinde Vlan 10 oluşturualım;

		> en
		> conf t
		> vlan 10
		> name LAPTOPS
*	Vlanları görüntülemek için;

		> do show vlan

*	**"> name LAPTOPS"** ile ***Vlan 10***'u *LAPTOPS* olarak adlandırdık.
*	**"> vlan 10"** oluşturulduğunda Vlan 10 port içermez. Yani içi boş olarak oluşturulur.
*	***Portları içine atmak için;***

**Atamak istediğimiz portun** bulunduğu **interface'e** gireriz.

	> int fa0/1
	> switchport mode access
	> switchport access vlan 10
	> do show vlan

*	**switchport mode access**
	*	Bu port bir *access port*tur demektir.

*	**switchport access vlan 10**
	*	Ardından bu portun access'inin **Vlan 10** olduğunu ifade eder.

*	***Birden fazla port*** için yukarıdaki işlemlerin aynısını **tek tek** yapmak yerine ***range*** anahtar kelimesi kullanılır.

		> int range fa0/3-4
		> switchport mode access
		> switchport access vlan 20

*	**int range fa0/3-4**
	*	Verilen aralıktaki (range) portları atamak için hazırla. Ki sonraki komutta da onları Vlan 20'ye aktardık.

*	Eğer atamak istediğimiz **Vlan henüz oluşturulmamış** olsa bile ona **port atamaları**;

		> int range fa0/5-6
		> switchport mode access
		> switchport access vlan 30

*	**> switchport access vlan 30**

	*	Network admini düzeyinde işlem yapıldığı için bu **Vlan 30** oluşturuluyor. 
	*	Sonra *port 5* ve *port 6*'yı bunun içine atıyor.

*	Gigabit'e eklenmiş olan Switch cihazını (yani Trunk hattı olacak) kendi switchimizle birleştirmek için;

		> int g0/1
		> switchport mode trunk

*	**> switchport mode trunk**
	*	Trunk demek bütün Vlanların (Vlan 10, 20, 30) buradan geçmesi demektir. Dolayısıyla Vlan ataması yapılmaz.

*	**> show interfaces trunk**
	*	Trunk interface'lerini görebilmek için kullanılır.

*	***Layer 3 Switch***lerde default olarak **auto** trunk encapsulation olduğu için **trunk** moduna geçilemez.
*	Bu durumu değiştirmek için yani **Auto**'yu **Trunk** moduna alabilmek için:

		> switchport mode dynamic desirable

komutu girilmelidir. Sonrasında;

	> switchport mode trunk

yazılarak **Trunk** moduna alınır.

*	**Vlanların tüm hat boyunca geçen trafiğe dahil olabilmeleri için **dahil edilen** tüm switchlerde de bu vlanlar oluşturulmalıdır.**


### Trunk Yönetimi

*	Yönetimi yapabilmek için Trunk'ın bulunduğu interface'e giriş yapılmalıdır.

		> int g0/1
		> switchport trunk allowed vlan 10, 20

*	Bu komut şunu ifade eder; bu switch portunda trunk üzerinde müsaade edilen vlanlar yazıldığında *(10, 20)* onlara izin verilecektir.
*	Başka bir Vlan eklemek istersek eğer aynı metotu kullanarak, örneğin, Vlan 30'u eklemeye çalışırsak yazılmış olan Vkan 10, 20 ***overwrite*** edilir. Yani daha önceki Vlanlar silinir.
*	Bunu engellemek için;

		> switchport trunk allowed vlan add 30

*	**add**
	*	Vlan ekler.
*	**remove**
	*	Vlan siler.
*	**except**
	*	100 Vlan varsa bunlardan 99'uncusu hariç hepsini yasaklar.
*	**all**
	*	Hepsini geçir.

---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

### Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en) 
 