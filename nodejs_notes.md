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
# kullanici yarat
psql 
# bunu kodda degistirmeyi unutma
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

* 
