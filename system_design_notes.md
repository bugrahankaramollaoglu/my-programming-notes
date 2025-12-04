# SYSTEM DESIGN NOTES

- iki tür IP vardır: IPv4 (192.168.1.1 gibi) ve IPv6 (2001:0db8:85a3:0000 gibi). ipv4 tipinde yaklaşık 4.5 milyar ip olabiliyor, o da tükendi. ipv6 ise sınırsız (340 desilyon falan).
 sen https://asd.com adresine baglanırken arkaplanda aslında 142.152.1.53 gibi bir adrese baglaniyosun. bu geçişi arkaplanda DNS hallediyor.  
- DNS Records
    * A -> ahmet.com aslında 156.244.20.32 gibi bir adrese gidiyoduk demistik. ahmet.com'un bu sayısal adrese refere ettigi bilgisini A kaydı sayesinde yapiyoruz. ahmet.com -> A -> 156.244.20.32
    * AAAA -> A kaydı IPv4'ler için kullanılırken AAAA IPv6'larda kullanılır. peki neden AAAA deniyor? çünkü v4 32bit, v6 128 bit. yani v6, v4'ten 4 kat daha büyük. bir websitesinin A ya da AAAA kaydını öğrenmek için `dig` komutunu kullanabilirsin: `dig google.com AAAA` gibi. 
    * CNAME -> Canonical Name. eğer IP 156.244 ... gibi sabit bir IP değilse, ama sabit bir servisten aliyorsa (Medium, Blogger vs.) o zaman CNAME tanımı yapmak gerekiyor: blog.ahmet.com -> CNAME -> blog.ahmet.medium.com
    * MX -> bir adrese mail almak için Google'dan hizmet almalısın. buna MX (Mail Exchange) deniyor. ahmet.com -> MX -> aspmx.l.google.com
    * TXT -> bu site benim diye ispat etmek için kullanırsın. Mesela siteni Google Search Console'a ya da Facebook Business'a kaydedeceksin. Ama Google bu domain'in gerçek sahibinin sen oldugunu nereden bilebilir? sana bir kod veriyolar: google-site-verification=AbCdEf123 gibi. bunu websitende doğru ve gizli bir yere koymanı ister. 
- Routing: verinin client'tan server'a gidene kadar gittigi yerlerde yolunun tekrar tarif edilmesidir. şöyle ki: 
    * Your phone → WiFi router → ISP Router → Internet Backbone → Cloud Load Balancer → App Server
    gidene kadar 20 küsür router'a ugrayabilir. bir router asla verinin icine bakmaz, gidecegi ip'ye göre şuraya/buraya git der. standart olarak bir routier if/else blogundab baska bir sey degildir. OSPF, BGP (google, aws vs. kullaniyor) gibi routing protokollerini kullanır.
- mesela flutterdan bir api'ye istek atiyosun:
    * `final result = await http.post("https://www.deneme.com/login");`
    * arka planda şunlar olur
        * uygulama önce DNS sunucusuna gider (genelde Google'ın 8.8.8.8'i) ve ona bu adresin A kaydının (sayısal IP adresinin) ne oldugunu sorar. eğer bu başarısız olursa `SocketException` alırsın. 
        * A kaydı öğrenildikten sonra telefon gönderdigi json body'sini küçük frame'lere böler ve bu dijital veriyi 0.1 olarak, içindeki wifi donanımı sayesinde radyo dalgalarına çevirip havaya saçar. evindeki modem bu dalgaları yakalar ve tekrar dijital veriye çevirir. telefonun ip'si muhtemelen yerel oldugu icin (192.168.1.5) NAT IP işlemi uygulanır. NAT bir ağda bulunan bilgisayarın, kendi ağı dışında başka bir ağa veya İnternete çıkarken farklı bir IP adresi kullanabilmesi için geliştirilmiş bir İnternet protokolüdür. Yani NAT bilgisayarın sahip olduğu IP adresini istenilen başka bir adrese dönüştürür.
        * ISP (Internet Service Provider: türk telekom, superonline vs.) senin paketini alır ve kıtalararası fiber kablolara yönlendirir. buna `backbone of internet`denir. 
        * buradan LoadBalancer'a gelir. loadbalancer  hangi paketin nereye gidecegine karar veren, verimlilik odaklı bir duraklama noktasıdır. https decryiption'i, sertifikalar vs. loadbalancer'da tanımlanır. 
        * oradan da server'ina , mesela django serverina gider. django cevabi üretir -> LB'a verir, LB onu şifreler -> backbone of internet -> ISP -> Modemin -> telefonuna geri döner. 
- internete gönderdigin veriler `paket`ler halinde tutulur.
