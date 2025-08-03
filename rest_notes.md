
# Rest Notes

* rest, http protokolü üzerinde çalışan bir mimarinin adıdır. bu mimariyi kullanan web servislerine ise rest api denir. rest api için ihtiyacımız olan ilk şey bir URL. bir url'ye GET ile istek atınca sana json/xml formatında bir response döndürür. sadece bu aradaki köprü önemlidir, client server'in iç kodlarını bilmek zorunda değildir, or vice versa.
* bir api geliştirmek için başka alternatifler de vardır.
	* REST
	* SOAP
	* gRPC
	* XML-RPC gibi
	ama genellikle modern mimarilerde Rest tercih edilir.
* rest api, iki ayrı ucun (server, yani backendin) ve (client, yani uygulaman) arasındaki internet üzerinden haberleşmeyi sağlayan kural dizisidir.
* Rest, URI tipinde bir resource ile çalışır (Uniform Resource Identifier). URI, istemcinin (mobil uygulama, tarayıcı vs.) hangi veriye erişmek istediğini söyler. REST mimarisinde her kaynak (user, ürün, sipariş) benzersiz bir URI ile temsil edilir. mesela bazı URI örnekleri
	* GET /kisiler
	* POST /urunler
	* DELETE /urunler/25
	get, post ve delete burada http metotları, diğerleri ise URI'lerdir. URI isminde fiil kullanilmaz (/getUser) gibi. Örnek:

	``` javascript
	const express = require('express');
	const app = express();
	app.use(express.json());

	let urunler = [
	  { id: 1, ad: "Kalem", fiyat: 5 },
	  { id: 2, ad: "Defter", fiyat: 15 }
	];

	// GET /urunler — tüm ürünleri getir
	app.get('/urunler', (req, res) => {
	  res.json(urunler);
	});

	// GET /urunler/:id — tek bir ürünü getir
	app.get('/urunler/:id', (req, res) => {
	  const urun = urunler.find(u => u.id == req.params.id);
	  if (!urun) return res.status(404).send("Ürün bulunamadı");
	  res.json(urun);
	});

	// POST /urunler — yeni ürün ekle
	app.post('/urunler', (req, res) => {
	  const yeni = {
	    id: Date.now(),
	    ad: req.body.ad,
	    fiyat: req.body.fiyat
	  };
	  urunler.push(yeni);
	  res.status(201).json(yeni);
	});

	// DELETE /urunler/:id — ürün sil
	app.delete('/urunler/:id', (req, res) => {
	  urunler = urunler.filter(u => u.id != req.params.id);
	  res.status(204).send();
	});

	app.listen(3000, () => console.log("API 3000'de çalışıyor"));

	```
	bunu daha sonra appinde kullanmak istersen de:
	``` dart
	Future<List<dynamic>> fetchUrunler() async {
	    final response = await http.get(Uri.parse('http://localhost:3000/urunler'));
	    if (response.statusCode == 200) {
	      return jsonDecode(response.body);
	    } else {
	      throw Exception('Ürünler alınamadı');
	    }
  }
	```

* mesela bir yemek siparişi uygulaması yaziyosun ve user pizza siparişi verdi. uygulaman, bu siparişi REST API'ye şöyle gönderir

``` dart
POST /siparis
{
	"yemek": "pizza",
	"adet": 2,
}
```

* her requestin 4 parçası vardır [giden]
1. Header: requestin metadatasını tutar
2. Body: requestin esas kısmını tutar. genelde json formatı
3. Operation: requestin türünü tutar (POST, GET vs.)
4. Endpoint: requestin adresini tanımlar: kasim-adalan.pu.he/api/yemekler gibi.
- her response'un da 3 parçası vardır [gelen]
1. header: metadatayı tutar
2. body: sunucudan gelen esas veri. json formatındadır.
3. status line: 3 haneli http statusCode. (200, 500 vs.)
* Rest API'de 4 temel işlem
	* **GET**: veri çekmeye yarar
	* **POST**: veri yüklemeye yarar
	* **PUT**: veri güncellemeye yarar
	* **DELETE**: veri silmeye yarar
* Rest API'nin birkaç farklı cornerstone'u vardır
	* **Stateless** olması: client'tan server'a request atarken session gibi bilgiler tutulmaz, her seferinde baştan kurulur. buna Rest API'nin *stateless* olması denir.
	```javascript
	app.get('/hello', (req, res) => {
		// just responds based on the requested info
		res.send(`Hello, your ip: ${req.ip}`);
	});
	```
	* **Uniform Interface** olması: REST API'nin tüm kaynaklara (kullanıcı, ürün, sipariş...) aynı şekilde erişilmesini sağlayan bir standarttır. Basitçe:
		* Tüm kaynaklar için:      URL’ler net olmalı (/kullanici/1, /urun/5)
		* HTTP metodları düzgün kullanılmalı (GET, POST, PUT, DELETE)
		* Cevap formatı genelde JSON olmalı ama xml, txt, html de olabilir.
		* Kaynaklar "isim" olarak temsil edilmeli, fiil değil
		Yanlış: /getUser, /deleteUser     ✅ Doğru: /kullanici, /kullanici/1
	```javascript
	const express = require('express');
	const app = express();
	app.use(express.json());

	// Veri tabanı gibi davranan basit dizi
	let kullanicilar = [
	  { id: 1, ad: "Ahmet" },
	  { id: 2, ad: "Ayşe" }
	];

	// GET /kullanici — tüm kullanıcıları getir
	app.get('/kullanici', (req, res) => {
	  res.json(kullanicilar);
	});

	// GET /kullanici/1 — tek kullanıcıyı getir
	app.get('/kullanici/:id', (req, res) => {
	  const k = kullanicilar.find(k => k.id == req.params.id);
	  if (!k) return res.status(404).send("Bulunamadı");
	  res.json(k);
	});

	// POST /kullanici — yeni kullanıcı ekle
	app.post('/kullanici', (req, res) => {
	  const yeni = { id: Date.now(), ad: req.body.ad };
	  kullanicilar.push(yeni);
	  res.status(201).json(yeni);
	});

	// DELETE /kullanici/1 — kullanıcı sil
	app.delete('/kullanici/:id', (req, res) => {
	  kullanicilar = kullanicilar.filter(k => k.id != req.params.id);
	  res.status(204).send();
	});

	app.listen(3000, () => console.log("API 3000'de"));

	```
	* **Client-Server Ayrı** olması: İstemci (client) ve sunucu (server) birbirinden bağımsız çalışmalı, sadece veri alışverişi yapmalıdır.
	```javascript
		// SERVER TARAFI
		app.get('/time', (req, res) => {
			res.json( {serverTime: new Date() } );
		});
	```

	```dart
		// APP TARAFI
		Future<void> fetchTime() async {
			final url = Uri.parse('http//localhost:3000/time');
			final response = await http.get(url);
			if (response.statusCode == 200) { // başarılı oldu }
			else { // hata }

	```
	* **Cacheable** olması: REST API’den gelen bazı cevaplar tekrar tekrar değişmediği sürece aynı kalır. Bu cevapları tekrar tekrar istemek yerine, önbelleğe (cache) alıp doğrudan kullanabiliriz.
	``` javascript
		const express = require('express');
		const app = express();
		app.get('/urun/:id', (req, res) => {
		  const urun = { id: req.params.id, ad: "Kalem", fiyat: 10 };
		    // 60 saniye boyunca cache kullanılabilir olduğunu belirtiyoruz
		   res.set('Cache-Control', 'public, max-age=60');
		   res.json(urun);
		});
		app.listen(3000, () => {
		  console.log('Sunucu 3000 portunda çalışıyor');
		});
	```
	* **Layered** olması: bir rest api dizaynında client her zaman sunucuya direkt istek atmayabilir, araya encryption gibi katmanlar girebilir. her bir katman sadece kendi scope'unu görebilir.
	* **Code on demand (optional)** olması: altıncı ve son rest api özelliğidir. restin applet/script formatında kod blogu indirme özelligine denir.
* bazı önemli hata kodları

| Kod  | Durum                  | Açıklama                                                                                     |
|-------|-----------------------|----------------------------------------------------------------------------------------------|
| **201** | Created               | PUT veya POST işlemi başarıyla tamamlandı. Nesne başarıyla oluşturuldu veya güncellendi.       |
| **204** | No Content            | PUT veya POST işlemi başarıyla tamamlandı. İçerik olmadan cevap döner. Dizin veya belgeler başarıyla yüklendi. |
| **400** | Bad Request           | İstek URI’sinde, üstbilgilerde veya gövdede hata olduğunda döner.                            |
| **401** | Unauthorized          | Korumalı bir kaynağa gerekli yetkilendirme sağlanmadan erişim yapılmaya çalışıldığında döner.|
| **403** | Forbidden             | Geçersiz API anahtarı kullanıldığında döner.                                                |
| **404** | Not Found             | İstenen kaynak (resource) bulunamadığında döner.                                            |
| **405** | Method Not Allowed    | İstek yapılan URI ilgili HTTP metodunu desteklemiyorsa döner.                               |
| **406** | Not Acceptable        | Server, client’ın `Accept` header’ında belirtilen medya tiplerinden birini sağlayamadığında döner. |
| **409** | Conflict              | Yazma işlemlerinde çakışma (conflict) olduğunda döner.                                      |
| **415** | Unsupported Media Type| Desteklenmeyen medya tipi ile resource gönderildiğinde döner.                              |
| **500** | Internal Server Error | Server tarafında bir hata olduğunda ve istek yerine getirilemediğinde döner.                |
* **express** nedir, neden kullanırız? express, bir nodejs framework'ü ve işleri kolaylaştırıyor. normalde vanilla http ile
``` javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/urunler' && req.method === 'GET') {
    const urunler = [{ id: 1, ad: "Kalem" }];
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(urunler));
  } else {
    res.writeHead(404);
    res.end('Sayfa bulunamadı');
  }
});

server.listen(3000, () => console.log('Server çalışıyor'));

```
böyle yazmak durumunda kalırdık. express sayesinde çok daha basit:
``` javascript
const express = require('express');
const app = express();

app.get('/urunler', (req, res) => {
  res.json([{ id: 1, ad: "Kalem" }]);
});

app.listen(3000, () => console.log('Express server çalışıyor'));
```




