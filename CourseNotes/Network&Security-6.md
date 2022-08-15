#NETWORK & SECURITY

##Part - 6
----

	Cisco Packet Tracer kullanılmıştır.

###Bandwidth Atama

*	Link State protokoller hattın durumunu kontrol ederler. Burada onlar için önem arz eden parametre ***"bandwidth"*** tir.
*	Diğer önemli olan parametre ***"delay"***dir.
*	Fakat hattın hızı aynı olursa (her hızın belli bir sabir bir delay'i vardır) delay de aynı olacağı için algoritma/protokoller ***"bandwidth"*** parametresine bakacaklardır.
*	Bandwidth'i biz atarız.
*	**RIP** *bandwidth* parametresini değil, *hop-count* parametresini kullanır.
*	**ERGP** ve **OSPF** ise ***bandwidth*** parametresini kullanır. Yol seçiminde kullanılır.
*	Bandwidth, verilmiş olan **clock rate**'e göre belirlenir.

		> bandwidth [BandwidthAmount]
		
*	Örneğin; 2 mbps (2000000) göre bandwidth 2000 olur.
*	Veya 64000 kbps göre bandwidth 64 olur.

		> en
		> conf t
		> int s0/0/0
		> bandwidth 2000

Şeklinde bandwidth verilir.


---

@author ***[Ali Yavuz YALÇIN](https://www.linkedin.com/in/ali-yavuz-yalcin/)***

###Network & Security Bootcamp --> [techcareer.net](https://www.techcareer.net/en)