# nodejs notes

* bir nodejs + express projesi yaratmak için
```bash
npm init -y
npm install express
```

* nodejs'te bir backend yazmak için routelar belirlemelisin. NodeJS'te basit bir API örneği:

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// middleware so we can send JSON in requests
app.use(express.json());


let books = [
	{ id: 1, title: 'kitap1', author: 'yazar1' },
	{ id: 2, title: 'kitap2', author: 'yazar2' },
	{ id: 3, title: 'kitap3', author: 'yazar3' }
]

// get all books
app.get('/books', (req, res) => {
	res.json(books);
});

// get a book by id
app.get('/books/:id', (req, res) => {
	const id = parseInt(req.params.id);
	const book = books.find(b => b.id === id);

	if (!book) return res.status(404).json({ error: 'Book not Found!' });

	res.json(book);
});

// post a book
app.post('/books', (req, res) => {
	const { title, author } = req.body;

	if (!title || !author) {
		return res.status(400).json({ error: 'Title and author required. ' });
	}

	const newBook = {
		id: books.length + 1,
		title, author,
	}

	books.push(newBook);
	res.status(200).json(newBook);
});

// update a book
app.put('/books/:id', (req, res) => {
	const id = parseInt(req.params.id);
	const { title, author } = req.body;
	const book = books.find(b => b.id === id);

	if (!book) return res.status(404).json({ error: 'Book not Found!' });

	if (title) book.title = title;
	if (author) book.author = author;

	res.json(book);

});

// delete a book
app.delete('/books/:id', (req, res) => {
	const id = parseInt(req.params.id);
	const index = books.find(b => b.id === id);

	if (index === -1) return res.status(404).json({ error: "Book not Found!" });

	books.splice(index, 1);
	res.json({ message: 'Book deleted successfully.' });
});

app.get('/', (req, res) => {
	res.json({ message: 'book API\'e hos geldin.' });
});

app.listen(PORT, () => console.log(`Server running on http://localhost:${PORT}`));

```

daha sonra bunu CURL'de, Insomnia'da ya da Postman'de test edebilirsin.

* verileri persistent yapmak istiyosan veritabanı kullanmalısın. mesela nodejs + postgreSql:

herhangi bir dizinde: 
```bash
sudo apt install postgresql postgresql-contrib
sudo -i -u postgres
createdb bookdb
(kullanici yarat)
psql 
(bunu kodda degistirmeyi unutma)
ALTER USER postgres WITH PASSWORD 'yourpassword'; 
\q
exit
```
proje dizininde
```bash
npm install pg pg-hstore sequelize
```

sequelize bir ORM paketi. Raw sql yazmak yerine otomatik olarak js objelerine ceviriyor.
pg nodejs'in postgresql calistirmasi icin gerekli. 
pg-hstore da yine sequelize'nin kullanması icin key-value işini kolaylaştıran bir paket.

## HTTP Response Yapısı

Bir **HTTP response (cevap)** üç ana kısımdan oluşur:

---

### 1. Status Line (Durum Satırı)

- Cevabın ilk satırıdır.  
- İçerik:
  - **HTTP versiyonu** (`HTTP/1.1`, `HTTP/2`, `HTTP/3`)  
  - **Status code (durum kodu)** → cevabın sonucunu belirtir  
    - `200 OK` → başarılı  
    - `201 Created` → yeni kaynak oluşturuldu  
    - `404 Not Found` → kaynak yok  
    - `500 Internal Server Error` → sunucu hatası  
  - **Status message** → kodun kısa açıklaması  

**Örnek:**
HTTP/1.1 200 OK

markdown
Copy
Edit

---

### 2. Headers (Başlıklar)

- Key–Value çiftlerinden oluşur.  
- Cevapla ilgili **meta bilgi** taşır.  

**Örnek başlıklar:**
- `Content-Type: application/json` → body’nin formatını belirtir  
- `Content-Length: 123` → body’nin uzunluğu  
- `Set-Cookie: sessionId=abc123` → cookie gönderir  
- `Cache-Control: no-cache` → tarayıcıya cache ile ilgili talimat verir  

**Örnek:**
Content-Type: application/json
Content-Length: 57
Date: Wed, 21 Aug 2025 18:25:00 GMT

markdown
Copy
Edit

---

### 3. Body (Gövde)

- Asıl veriyi içerir.  
- Türü `Content-Type` header’ına göre değişir:
  - `text/plain` → düz metin  
  - `text/html` → HTML sayfası  
  - `application/json` → JSON veri  
  - `image/png` → resim dosyası  
- Body opsiyoneldir (ör: `204 No Content` response’unda body yoktur).  

**Örnek (JSON body):**
```json
{
  "id": 1,
  "title": "Learn Node.js",
  "completed": false
}

* JWT nedir? jwt, server -ve- client arasında data alışverişinde kullanılan bir güvenlik protokolüdür. 3 kısımdan oluşan bir string olarak düşünebilirsin. 
	* 1. kısım, *header* : token tipini (JWT) ve imzalama algoritmasını (HS256) tutar.
	* 2. kısım, *payload* : verinin adı. mesela ( {username: "test"} ); gibi. bu kısımda iat (issued_at) ve exp (expired_at) verileri de tutulur.
	* 3. kısım, *signature*: hashlenmiş (şifrelenmiş) bir anahtar. ilk iki kısım değişirse bu da değişir. kendi belirledigin ve .env'de sakladıgın bir SECRET_KEY ile şifrelenir.
	
* BEARER_TOKEN nedir? en sık kullanılan token formatıdır. jwt'den dönen bearer token'ini girdigin zaman giris yapan user'in bilgilerini alabilirsin.
ayrıca, JWT ile ugrasırken bir expiry date belirlersin. dönen token ne kadar süre geçerli olacak (request edildiginde user bilgilerini döndürebilecek) diye. 
* *Access token* vs. *Refresh token* farkı: 
	* *access token*: kısa süreli güvenlik tokeni. her request attıgında yeniden olusturulur.
	* *refresh token*: uzun süreli (days/weeks). client'ta saklanır. böylece user cıkıs yapmadıgı sürece haftalar boyunca logged in kalir.
	
