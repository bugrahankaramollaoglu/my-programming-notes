# java notları

- sonuç ne olur?

```java
public class question_3 {

	public static void main(String[] args) {
		int a = 1, b = 2, c = 4;
		a = a + b + (b = c + a);
		System.out.println(a); // a = 1 + 2 + (b = 1 + 4 yani b = 5) -> 3 + 5 == 8
		System.out.println(b); // 1 + 4'ten 5 olmuştu
		System.out.println(c); // 4 kaldı
	}
}
```

- tek satırda birden fazla input alma

```java
public class MultipleInputs {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("İki tamsayıyı boşlukla ayırarak girin: ");

        // İki tamsayıyı boşlukla ayırarak alıyoruz
        int firstNumber = scanner.nextInt();
        int secondNumber = scanner.nextInt();

        System.out.println("Girilen tamsayılar: " + firstNumber + " ve " + secondNumber);

        // Scanner'ı kapatmayı unutmayın
        scanner.close();
    }
}
```

ama eğer sayı çok fazla ise döngü kullanmalısın

```java
public class MultipleInputs {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Kaç adet sayı gireceksiniz? ");
        int numberOfInputs = scanner.nextInt();

        int[] numbers = new int[numberOfInputs];

        System.out.println("Lütfen " + numberOfInputs + " adet sayıyı boşluklarla ayırarak girin: ");

        for (int i = 0; i < numberOfInputs; i++) {
            numbers[i] = scanner.nextInt();
        }

        System.out.print("Girilen sayılar: ");
        for (int i = 0; i < numberOfInputs; i++) {
            System.out.print(numbers[i] + " ");
        }

        // Scanner'ı kapatmayı unutmayın
        scanner.close();
    }
}
```

- StringBuilder ile yarattıgın bir değişkeni normal String ile beraber kullanamazsın, önce castlemen lazım

```java
public static void isPalindrome(String str) {
		StringBuilder rev_str = new StringBuilder(str).reverse();
		if (rev_str.toString().equals(str)) {
			System.out.println("it is palindrome.");
		} else {
			System.out.println("it is not.");
		}
	}
```

- substring(a, b) works like → a included, b excluded
- run-time polymorphism is achieved by method overriding. yani şöyle: subclass inherit ettiği sınıftaki bir fonksiyonu yeniden yazarsa buna method overriding denir

```java
class Animal {
    void makeSound() {
        System.out.println("animal sound");
    }
}

class Cat extends Animal {
    // Overriding the makeSound method of superclass
    @Override
    void makeSound() {
        System.out.println("miyav");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        // Creating objects of the subclasses
        Animal cat = new Cat();

        cat.makeSound(); // miyav
    }
}
```

- bir arrayin sonuna giderken size() değil `length` kullanılır

```java
for (int i = 0; i < arr.length; i++);
```

- because strings in java are immutable, you cannot say

```java
String ss = " a sdn sj ds   ";
ss.trim(); // YANLIŞ
ss = ss.trim(); // doğrusu

ss.substring(3,6); // YANLIŞ vs.
ss = ss.substring(3, 6); // doğrusu
```

- sonuç ne olur?

```java
class Bugra {
	final String message(){
		return "aaa";
	}
}

class Deneme {
	public static void main(String[] args) {
		System.out.println(message());
	}

	final String message() {
		return "bbb";
	}
}
```

- Command line arguments alırken javada cdeki gibi ./a.out’tan başlamıyor, `java program_name`'den sonra başlıyor. söyle ki:

```java
class Deneme {
	public static void main(String[] args) {
		System.out.println(args[0]); // bugra
		System.out.println(args[1]); // kara
		System.out.println(args[2]); // molla
		System.out.println(args[3]); // oglu
	}
}
```

- C’de olmayan bir olay: for-each loops

```java
class Deneme {
	public static void main(String[] args) {
		List<String> arr = new ArrayList<String>();
		arr.add("bugra");
		arr.add("kara");
		arr.add("molla");

		for (String elem : arr) {
			System.out.print(elem + ", ");
		}
	}
}
```

şöyle de kullanabilirsin

```java
my_list.forEach(System.out::println);
```

- sonuç ne olur?

```java
System.out.println("apple".compareTo("pearl"));
```

- 2 ways to sort an ArrayList

```java
Collections.sort(my_list);

my_list.sort(Comparator.comparing(String::toString))
```

- how to get current date

```java
LocalDate ld = LocalDate.now();
```

- sonuç ne olur?

```java
class Deneme {
	public static void main(String[] args) {
		for (int i = 0; i < 10; i = i++) {
			i += 1;
			System.out.println(i);
		}
	}
}
```

- sonuç ne olur?

```java
class Deneme {
	public static void main(String[] args) {
		LinkedList<Integer> list = new LinkedList<>();
		list.add(10);
		list.add(20);
		list.add(30);

		System.out.println(list);
	}
}
```

- javada liste oluşturmanın birkaç yolu var
```java
int[] arr = {10, 20, 30};
int[] arr = new int[3]{10, 20, 30};

List<Integer> arr = Arrays.asList(10, 20, 30);
List<Integer> arr = List.of(10, 20, 30);

List<Integer> arr = ArrayList<Integer>();
arr.methods();
```

- hangisi daha verimli? `==` mi `equals()` mi?

```java
String s1 = "bugra";
String s2 = "buğra";

s1 == s2;
s1.equals(s2);
```

```java
class Deneme {
	public static void main(String[] args) {
		String s1 = "bugra";
		String s2 = new String("bugra");
		System.out.println(s1 == s2); 		 // false
		System.out.println(s1.equals(s2)); // true
	}
}
```

- asList() fonksiyonu şunu yapar

```java
class Deneme {
	public static void main(String[] args) {
		String[] array = { "abc", "2", "10", "0" };

		/*
		 * bir listeden vs. asList() ile yeni bir liste yarattığın zaman
		 * birbirine bağlanır, birinde yapılan değişiklikler öbüründe de olur
		 * yeni listenin boyutu değişmez, fixed olur
		 * add, clear, remove() vs. kullanamazsın
		 */

		List<String> list = Arrays.asList(array);
	}
}
```

- bazı önemli tagler:
    - non-static: her kullanışta yeni kopyalar yaratılır

    ```java
    public class Car {
        String model;   // non-static variable
        int year;       // non-static variable

        public Car(String model, int year) {
            this.model = model;
            this.year = year;
        }
    }
    ```

    - static: burada ise objeye değil, sınıfa özel değişkenlerden bahsediyoruz. bir statik değişkenin yalnızca bir kopyası vardır, sınıfın tüm objeleri arasında bu kullanılır

    ```java
    public class Counter {
        static int count = 0;   // static variable

        public Counter() {
            count++;
        }
    }
    ```

    - final: atandıktan sonra değeri değiştirlmesin istediklerimiz

    ```java
    public class Circle {
        final double PI = 3.14;  // final non-static variable
        static final int RADIUS = 5;  // final static variable
    }
    ```

    - private: sadece sınıf içinden erişilebilen değişkenlerdir

    ```java
    public class Person {
        private String name;   // private variable

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
    ```

- sonuç ne olur?

```java
class Deneme {
	int age = 3;

	public static void main(String[] args) {
		System.out.println("age: " + age);
	}
}
```

hata verir. çünkü fonksiyon dışında tanımladığın bir değişkene fonksiyon içerisinde direkt erişemezsin. iki şey yapabilirsin

```java
public class Deneme {
    static int age = 3; // ya değişkeni statik yaparsın ki classa ait olsun

    public static void main(String[] args) {
        System.out.println("age: " + age);
    }
}
```

ya da bir obje üzerinden erişirsin

```java
public class Deneme {
    int age = 3;

    public static void main(String[] args) {
        Deneme deneme = new Deneme();
        System.out.println("age: " + deneme.age);
    }
}
```

- eleman ekleme

```java
public class User {
	private String name;

	User(String name) {
		this.name = name;
	}

	public String get_name() {
		return name;
	}

	public static void main(String[] args) {
		List<User> list = new ArrayList<User>();
		list.add(new User("bugra"));
		list.add(new User("kara"));
		list.add(new User("molla"));

		for (User elem : list) {
			System.out.print(elem.get_name() + ", ");
		}
	}
}
```

- abstract classes:
- how to convert from String to Int

```java
Integer.parseInt("32");
```

- sonuç ne olur?

```java
class Deneme {
	private String name;

	Deneme(String name) {
		this.name = name;

	}

	public static void main(String[] args) {
		System.out.println(new Deneme("bugra"));
	}
}
```

```java
class Deneme {
    private String name;

    Deneme(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return name;
    }

    public static void main(String[] args) {
        System.out.println(new Deneme("bugra"));
    }
}
```

- **`Overloading`:** Aynı isime sahip birden fazla metod kullanma durumuna overloading denir. Bu durumda, metotları birbirinden ayıran fark, aldıkları parametre olur. Bir metodu overloading yaparken aynı işlemi veya benzer işlemleri de gerçekleştirecek şekilde overloading yapmalısınız.
**`Override`**: Bir metodun tekrardan yazılması anlamına gelir. Kalıtım
ile aldığımız bir metodu değiştirmek istersek o zaman override etmemiz
yani yeniden yazmamız gerekir.w
- sonuç ne olur?

```java
int x = 5;
System.out.println(x++ + ++x);
```

- order of function prototypes doesn’t matter in java. these two are the same

```java
public static void main()
static public void main()
```

- javada mapleri kullanmanın yolu hashMap olayıdır

```java
public class HashTableExample {
    public static void main(String[] args) {
        // Creating a hash table
        Map<String, Integer> hashTable = new HashMap<>();

        // Adding key-value pairs to the hash table
        hashTable.put("John", 25);
        hashTable.put("Jane", 30);
        hashTable.put("Doe", 40);

        // Accessing values using keys
        int johnsAge = hashTable.get("John");
        System.out.println("John's Age: " + johnsAge); // 25

        // Iterating through the hash table
        for (Map.Entry<String, Integer> entry : hashTable.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }

        // Checking if a key exists in the hash table
        String searchKey = "Jane";
        if (hashTable.containsKey(searchKey)) {
            System.out.println(searchKey + " is in the hash table.");
        } else {
            System.out.println(searchKey + " is not in the hash table.");
        }
    }
}
```

key-value çiftlerinin saklandıgı bir map türü. unlike `HashMap`, `HashTable` is synkronized meanings it’s thread-safe. This means that multiple threads can access a hash table concurrently without the need for external synchronization. Neither keys nor values can be null in hash table. thread güvenliğinin olmadığı durumlarda hash map daha verimli oldugundan herkes genelde onu kullanır.

- HashMap: on the other hand is implemented like this

```java
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        // Creating a HashMap
        Map<String, Integer> studentGrades = new HashMap<>();

        // Adding key-value pairs
        studentGrades.put("Alice", 95);
        studentGrades.put("Bob", 87);
        studentGrades.put("Charlie", 91);
        studentGrades.put("David", 88);

        // Accessing elements
        System.out.println("Alice's grade: " + studentGrades.get("Alice"));

        // Iterating over entries
        for (Map.Entry<String, Integer> entry : studentGrades.entrySet()) {
            System.out.println(entry.getKey() + "'s grade: " + entry.getValue());
        }

        // Checking if a key exists
        if (studentGrades.containsKey("Charlie")) {
            System.out.println("Charlie's grade: " + studentGrades.get("Charlie"));
        }

        // Removing a key-value pair
        studentGrades.remove("David");

        // Size of the HashMap
        System.out.println("Number of students: " + studentGrades.size());
    }
}
```

- javada stringi traverse ederken str[i] diyemiyosun

```java
for (int i = 0; i < str.toString().length(); i++) {
			System.out.println(str.charAt(i));
		}
```

- different ways to traverse a string in java

```java
String str = "Hello, World!";

for (int i = 0; i < str.length(); i++) {
    char c = str.charAt(i);
    // Process the character 'c' here
    System.out.print(c + " ");
}

for (char c : str.toCharArray()) {
    // Process the character 'c' here
    System.out.print(c + " ");
}

str.chars().forEach(c -> {
    char character = (char) c;
    // Process the character 'character' here
    System.out.print(character + " ");
});
```

- eğer bir dsa sorusunda case insensitive diyorsa direkt

```java
str = str.toLowerCase();
```

diyerek küçük/büyük harf kontrollerinden kurtulabilirsin

- bir android projesinin içerisinde neler vardır?
    - `src`: .java kaynak dosyalarını tutar
    - `gen`: R.java dosyalarını tutar.
    - `assets`: resource dosyalarını tutar. menu, drawable, layout vs. gibi alt klasörleri vardır
    - `bin`: .apk dosyalarını ve bundle’ları tutar
- activity nedir? activity kullanının etkileşime geçtiği arayüzün adıdır. sayfa olarak düşünebiliriz. her uygulama en az bir aktivite kullanmak zorundadır. aktivitelerin yaşam döngüleri vardır, onCreate, onViewCreated, onDestroy vs. gibi. aktivitelere alternatif olarak daha light-weight olan fragmanlar da kullanılabilir. ilk olarak her zaman onCreate çağırılır.
- intent nedir? intent farklı sayfalara geçmeye yarayan metodun adıdır. iki çeşidi vardır
    - `explicit intent`

    ```java
    Intent intent = newIntent(this, SecondActivity.class);
    startActivity(intent);
    ```

    - `implicit intent`

    ```java
    Intent i = newIntent(Intent.ACTION_VIEW,Uri.parse(“http://www.amazon.com”));
    Intent i = newIntent(Intent.ACTION_DIAL,Uri.parse(“tel:+90505.....”));
    // direkt arar
    Intent i = newIntent(Intent.ACTION_CALL,Uri.parse(“tel:+90505.....”));

    startActivity(i);
    ```

    - `shared preference`: küçük çapta verileri key-value mantıgıyla saklamaya yarar. en güzel yanı uygulama kapansa da silinmemesidir. en kötü yanı ise sadece basit veri yapılarını saklayabilmesidir (string, boolean, float, int ve long). bu verileri xml dosyalarında saklar ve sonrasında çeker
- kaç farklı şekilde data saklayabiliriz?

    ```kotlin
    // kaydediyoruz
    val sharedPref: SharedPreferences = getSharedPreferences("com.bugra.app", Context.MODE_PRIVATE)
    val editor: SharedPreferences.editor = sharedPref.edit()
    editor.putString("my-key", "bu cümle saklanacak")
    editor.apply()

    // daha sonra kayıtlı bilgiyi çekiyoruz
    val retrievedVal = sharedPref.getString("my-key", "def_value")
    println(retrievedVal)

    // sharedPref içeriğini silmek için
    sharedPref.clear().apply()

    ```

    - `SQLite`: yerel bir sql kütüphanesinde verileri tablo halinde saklamaya yarar

    ```kotlin
    db.execSQL(CREATE_TABLE_QUERY)
    private const val DATABASE_NAME = "my_database"
    private const val DATABASE_VERSION = 1
    private const val CREATE_TABLE_QUERY = "CREATE TABLE IF NOT EXISTS MyTable (id INTEGER PRIMARY KEY, name TEXT);"
    private const val UPDATE_TABLE_QUERY = "DROP TABLE IF EXISTS MyTable; CREATE TABLE MyTable (id INTEGER PRIMARY KEY, name TEXT);"
    ```

    - `Content Provider`: uygulama verilerini diğer uygulamalarla paylaşmaya yarar

    ```kotlin
    val contentResolver = context.contentResolver
    val values = ContentValues().apply {
        put("column_name", "value")
    }
    contentResolver.insert(Uri.parse("content://com.example.provider/mytable"), values)
    ```

    - `File Storage:` dosyaya yazdırıp dosyadan okuma

    ```kotlin
    // Dosyaya yazma
    context.openFileOutput("filename.txt", Context.MODE_PRIVATE).use {
        it.write("Hello, World!".toByteArray())
    }

    // Dosyadan okuma
    context.openFileInput("filename.txt").bufferedReader().use {
        val content = it.readText()
        println(content)
    }
    ```

    - `View Model`: belli bir veri yapısının içeriğini farklı yerlerden çekip/değiştirme

    ```kotlin
    class MyViewModel : ViewModel() {
        private val _data = MutableLiveData<String>()
        val data: LiveData<String>
            get() = _data

        fun updateData(newData: String) {
            _data.value = newData
        }
    		fun getData() : String {
    			return _data
    		}
    }
    ```

    daha sonra bir aktivitede

    ```kotlin
    val sharedViewModel:SharedViewModel
    sharedViewModel.setdata("new")
    sharedViewModel.getData() // new vs.
    ```

- şöyle tanımlarsan

```java
String s = "asd";
```

java bunu string pool’da saklar. bir sonraki string yaratışında string poolu tarar, eğer birebir aynı stringi yaratmak istediysen bir daha yaratmaz ve var olanı kullanır.

```java
String s = new String("asd");
```

böyle yaparsan heap’te tutar.

```java
String s1 = "hello";
String s2 = "hello";
System.out.println(s1 == s2); // true

AMA

String s3 = new String("hello");
String s4 = new String("hello");
System.out.println(s3 == s4); // false
```

- bir listeyi .reversed() ile tersine çeviremezsin.

```java
LinkedList<Integer> tmp = list.reversed(); // YANLIŞ

LinkedList<Integer> tmp = list;
Collections.reverse(tmp); // DOĞRU
```

- javada != operatörü referansları ya da primitif tipleri karşılaştırırken kullanılır (int, char gibi). Objectleri karşılaştırmak için != kullanamazsın. çünkü != referans kontrolü yapar (aynı adrese mi işaret ediyor diye, actual valuesları kıyaslamaz). bunun için equals kullanmalısın

```java
Integer a = new Integer(5);
Integer b = new Integer(3);

if (a != b) // YANLIŞ
if (a.equals(b)) // DOĞRU
```

- Dependency Injection en basit haliyle, bir sınıfın bağımlılıklarını kendi yaratması yerine dışardan aldığı metottur.

```kotlin
class Car {
    private val engine = Engine() // araba motoru kendi yaratıyor
    fun start() {
        engine.run()
    }
}
```

yerine

```kotlin
class Car(private val engine: Engine) {
    fun start() {
        engine.run()
    }
}

val myEngine = Engine()
val myCar = Car(myEngine) //motor artık dışarıdan veriliyor
```

peki Dependency Injection’ın avantajları neler?

- test yazmak kolaylaşır (mock motor verebilirsin)
- kod daha esnek olur (daha sonra parametre türünü değiştirebilirsin)
- dependencyleri yönetebilirsin

DI yapmanın 3 yolu vardır

1. manuel yöntem (yukarıdaki gibi)
2. Hilt / Dagger (Google öneriyor)
3. Service Locator (çok önerilmez)

`peki Hilt/Dagger nasıl kullanılır?`

1. dependencyleri ekle
2. MyApplication : Application() (@HiltAndroidApp) ekle
3. manifeste <application name’e bu MyApplication’i ekle
4. MainActivity’ye @AndroidEntryPoint ekle

2 çeşit Injection var

1. field injection
2. constructor injection


* hashSet sıralamaya dikkat etmezken `LinkedHashSet` sıralamayı korur:
*
