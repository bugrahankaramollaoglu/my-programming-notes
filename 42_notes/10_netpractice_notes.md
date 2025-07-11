# 10 - netpractice

<aside>
💡 kaynakça

1) davut abi netpractice pdf’i

2) kendim

</aside>

- interneti ilk defa ABD savunma bakanlığı buluyor.
- IP adresi nedir? ağdaki her bir cihazın kendine özel adresidir. IPv4 ve IPv6 olmak üzere ikiye ayrılır. v4 32 bitlik, v6 128 bitlik adresler tutar o yüzden internet benzersiz ip adresleri yavaş yavaş tükendiği için IPv6’ya kaymaya başlamıştır
- ip’leri alt ağa bölmek için kullanılır. 32 bitlik bir sayıdır ve 8er 8er noktalarla ayrilir. her oktet 0-255 aralığındadır yani 0000 0000 ya da 1111 1111.
- alt ağ maskesi: Bir adresin hangi bölümünün alt ağa ve hangi bölümünün ana bilgisayara karşılık geldiğini açıklamak için kullanılan 32 bitlik bir kombinasyon. bir IP ağını alt ağlara bölmek olarak düşünebilirsin. Neden alt ağ maskesine ihtiyacımız var? alt ağ maskeleme olmazsa, iki IP aynı ağda olup olmadığını nasıl bilecek ve iletişim kuracak?
- routers: IP adreslerini kullanarak iletişim kurarlar. bir ağdan aldığı veriyi bir başka ağa yönlendirir. bir routerın birden fazla portu olabilir. ağları birbirine bağlar.
- switch: bilgisayarları birbirine bağlar ve bunu MAC adresleri üzerinden yapar.
- DHCP: Dynamic Host Configuration Protocol. bir ağdaki bilgisayarlara otomatik olarak IP atar.
- bilgisayar ağlarında iletişimi OSI protokolü sağlar (open systems interconnection)
- TCP/IP (Transmission Control Protocol/Internet Protocol): internet üzerindeki veri iletişiminde kullanılan bir protokol ailesidir. TCP/IP, verilerin ağ üzerinde doğru şekilde yönlendirilmesini sağlar ve verilerin bütünlüğünü korur.  OSI de TCP/IP de birer network modelidir.
- google.com adresinin IP adresi 172.217.22.14’dir
- internetin çalışmasının OSI modeline göre 7 katmani vardır
    - fiziksel katman: bu direkt kablolar vs. ile ilgilidir. elektrik, ışık (fiber) ya da radyo sinyalleri yollar. genelde elektrikle iletilir.
    - data-link
    - network, ağ katmanı: fiziksel katmandan gelen bitleri yorumlar. switchler ve MAC (haberleşme donanım adresi) kullanır.
    - transport, taşıma katmanı: bu katmanda verinin ne şekilde taşındığı bilgisi iletilir ve ona göre işlenir
    - session
    - presentation
    - application, uygulama katmanı: kullanıcıya gösterilen ürünün son hali
- routerla swtich arasındaki fark şu: routerin her bir ayagı birer network agı oluyor ama swithcin tek bir ağ üzerinde bilgisayarları bağlıyor
- [https://www.aelius.com/njh/subnet_sheet.html](https://www.aelius.com/njh/subnet_sheet.html)