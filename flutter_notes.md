# flutter notları

- dart is a statically typed language.
- all dart programs start with:

```dart
void main() {}
```

- debug banner kaldırmak istiyosan materialApp’e şunu ekle:

```dart
debugShowCheckedModeBanner: false,
```

- everything in flutter is a widget. mesela hello world yazacaksın.

```dart
import 'package:flutter/material.dart';

void main() {
	// MaterialApp widget here is the greatest widget
	// that you’ll use almost every time. on this layer we are writing things
	MaterialApp(
		// Center() bir widgetı ortalar
		home: Center(
			child: Text('merhaba dünya'),
		),
	);
}
```

- // yorum satırı demektir. formatted metindeki // Center, // Material App nerede neyin bittiğini gösterir. mesela // Center yazan yerde center satırı bitmiş. show closing labels ayarı ile bunu kapatabilirsin.
- widgets:
    1. Center() : needs to have a child: after it
    2. Image()
    3. NetworkImage()
    4. Scaffold()
    5. backgroundColor()
- Scaffold(): Implements the basic material design visual layout structure. yani üzerine widgetları yerleştirdiğin arkaplanı Scaffold() ile yaratıyosun. mesela tamamen mavi bir ekran yaratmak için:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
  const MaterialApp(
  home: Scaffold(backgroundColor: Colors.grey),
  ),
 );
}
```

- uygulamaya local resim ekleme:
    1. images isimli bir klasör yaratıyoruz
    2. resimleri buna atıyoruz
    3. pubspec.yaml dosyasında yolunu belirtiyoruz (resim sayısı çoksa subdirectory direkt belirtebilirsin : images/ )

    ```yaml
    flutter:
    assets:
    	- assets/resimler/resmim.png
    	- assets/resimler2/

    ```

- uygulamaya ikon yapma
    1. appicon.co’ya giderek seçeceğin bir resmi uygulama ikonu olarak ayarlayıp zip dosyasını indirmelisin
    2. daha sonra zip dosyasının içindeki mipmap’li dosyaları main.dart dizinindeki android/app/src/main/res klasöründeki mipmaplarla değiştirmelisin
    3. daha sonra ios/runner gidip assets.xcassets dosyasını yine zipteki aynı isimli dosyayla değiştirmelisin. Bu kadar, artık kare şeklinde bir icon verdin.
    4. fakat kare değil de yuvarlak ikon olsun istiyosan android/app/src/main/res’e sağ tıklayıp new 🡪 Image Asset deyip istediğin resmi kesip biçmen gerek. eğer Image Asset çıkmazsa (flutter projelerimde çıkmayabiliyor) Android klasörünü yeni pencerede açıp denemelisin
- be really careful about indentation which is always 2 spaces
- for hotReload to work, you should use a stateless or stateful widget
- widgetlar iki tür olabilir single-child or multi-child. that is to say that they can either have multiple widgets on themselves or only one single text, image etc. container with a single child will cover as much surface as it can. eğer container() metodunun içine mesela text yazdırdın ama yazdırdığın şey görünmüyosa, ekranın kenarlarında kalıp okunmuyorsa container’e alt+enter yapıp wrap with widget diyerek görünür alana taşıyabilirsin.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.grey,
        body: SafeArea(
          child: Container(
            height: 500,
            width: 500,
            margin: EdgeInsets.symmetric(horizontal: 100.0, vertical: 250.0),
            padding: EdgeInsets.all(80),
            color: Colors.white,
            child: Text('Helloo'),
          ),
        ),
      ),
    );
  }
}
```

- columns(), rows() hizalama: mainAxis yatay eksende hizalarken crossAxis dikey eksende hizalamak için kullanılır. yatay eksende hizalamak için diğerlerinden daha geniş görünmez bir container daha yaratmalısın çünkü containerler by nature birbirlerinin sağ yanlarına hizalıyorlar birbirlerini
- eğer bir resim çok büyük oluyosa ve taşıyosa
    1. width ile küçültebilirsin
    2. Expanded kullanabilirsin (it is child of a row or a column. expanded()’ın işlevi mümkün olduğunca taşırmadan ekranı doldurmasıdır. iki tane Expanded() kullanırsan iki resmi de eşit oranda (row()’da yatay, column()’da dikey olacak şekilde) genişletecektir. büyüklüklerinin oranlarını değiştirmek istiyosan you should use a method what is called flex: . Her birinin altına bunu yaz ve 2:1, 3:2 vs. gibi oran ver.

fonksiyonların parametre de alabilir

```dart
void greet(String name, String day) {
	print('hello $name. it\'s $day today.');
}

void main() {
	greet('bugra', 'wednesday');
}
```

parametreleri isimlendirdiğin sürece farklı sıralarda da verebilirsin

```dart
void main() {
	greet(day: 'wednesday', name: 'bugra');
}
```

fonksiyonların output da alabilir

```dart
int return_sum(var a, var b) {
	return (a + b);
}

void main() {
	int a = return_sum(3, 5);
}
```

- dart data types:
    1. strings : ‘hello’ . conventionally we use single quotes in Dart.
    2. integer: 1234
    3. double: 10.6
    4. bool: true false

these are known as primitive data types.

- => işaretinin işlevi nedir? It’s called arrow syntax.

```dart
int add(int a, int b) {
	return a+b;
}

// ifadesi kısaca şöyle yazılabilir
int add(int a, int b) => a+b;
```

ya da

```dart
void main(
	runApp(myApp),
	);
}

// yerine

void main() => runApp(myApp));
```

- daha sonra reminder olması için

```dart
//TODO metodunu kullanabilirsin. bu bir anahtar kelimedir
```

- materialTheme3 kullanmak için

```jsx
 theme: ThemeData(useMaterial3: true),
```

- dartta condition örneği:

```dart
int sum(var a, var b) {
	return (a+b);
}

void main() {
	sum(3,5);
}
```

- as you know dart is an OOP language. its four pillars are:
    1. abstraction:
    2. polymorphism
    3. inheritance
    4. encapsulation
- font ekleme:
    - fonts.google.com’dan font alıp atıyoruz assetlere
    - .yaml’da assets altında fonts altında ekliyoruz konumunu
    - kodda kullanıyoruz
- ses ekleme:
    1. öncelikle pub.dev’den audioplayers paketini indir
    2. installation sayfasındaki yönergeleri uygula
    3. import et
    4. kodda kullan
- dart dilinde bir property’i private yapmak için önüne _getirirsin. Thus in other files you can’t import and use that class, function or variable whatever, because it is hidden. you can only use in its own file.
- back in early days many programming languages were procedural, that is program read the commands from top to bottom and executed by line.
- `named arguments`: spesifik olarak isimleriyle belirttiğin parametrelere denir. { } içlerinde yazılırlar

```dart
void greet({String name, int age}) {
  print("Hello, $name! You are $age years old.");
}

greet(name: "Alice", age: 25);
greet(age: 30, name: "Bob");
```

bunlara default değer de verebilirsin

```dart
void greet({String name = "Unknown", int age = 0}) {
  print("Hello, $name! You are $age years old.");
}

greet(); // Unkown ve 0 verir
```

eğer named parameter kullanmasaydın sıraya riayet etmek zorundaydın. bu tür kullanıma ise `positional argument` denir.

```dart
void subtract(a, b) {
	return a - b;
}

sum(5, 2);
```

aralarındaki fark şudur. named argument kullanırken parametrelerden bazılarını vermeyebilirsin ama positional argument’larda hepsini vermek zorundasın. hata vermesin istiyosan şöyle yazmalısın

```dart
void subtract(a, [b = 1]) {
	return a - b;
}

subtract(6) // 5
```

kesinkes zorunlu olsun istiyosan `required` kullan

```dart
void subtract(required a, required b);
```

ayrıca subtract(int a, int b) demezsen verdiğin değere algılar.

- ister ‘ ‘ ister “ “ kullanabilirsin
- stless/stful widget kullanmazsan hotReload çalışmaz
- dart bir type-safe dildir yani her şeyin kesin bir veri tipi vardır. bir şey birden fazla veri tipine de dahil olabilir. mesela

```dart
int a = 40;
```

darttaki bazı temel veri tipleri

1. int
2. double
3. sum
4. String
5. bool
6. Object
- şu şekil renk seçebilirsin

```dart
backgroundColor: Color.fromARGB(255, 10, 50, 100)
```

- çift renk geçişli ekran yapmak için LinearGradient() widgetını kullanabilirsin
- basic structure of a flutter class

```dart
// myClass burada sınıfının ismi
// StatelessWidget sınıfından inherit ediyor extends sayesinde
class MyClass extends StatelessWidget {
  // constructor ekliyoruz
  const MyClass({super.key});

  // states that we are overriding StatelessWidget
  @override
  // build() fonksiyonu Widget döndürdüğünden başına yazdık
  Widget build(BuildContext context) {
    return Container();
  }
}
```

- dartta değişken tanımlarken başına ya `var` ya da `typeName` getirebilirsin

```dart
var a = 30;
int b = 50;
```

var getirirsen dinamik tanımlamış olursun yani eğer ilklendirmezsen bilgisayar onun hangi veri tipi tutacağını öngöremez o yüzden hata verir

```dart
String name = 'bugra'; // hata vermez
String surname; // hata verir
```

bu hatayı çözmek için sonuna `?` getirmelisin

```dart
String? surname; // hata vermez
```

- bir değişkenin başına `final` getirirsen o değişkene daha sonra yeni bir değer atamayacağını söylersin

```dart
final myName = 'bugra';
var myAge = 20;
```

- column() ve row() widgetları sayesinde düşey ya da yatay bir hizada birden fazla widgetı yan yana ya da üst üste dizebilirsin. ikisi de default olarak bütün ekranın boyunu ya da enini kaplarlar.
- flutter supports 3 different main buttons
    - ElevatedButton() → 3D gözükür
    - TextButton() → sadece metin şeklindedir
    - OutlinedButton() → 2D gözükür
- iki widget arası boşluk koymak için EgdeInsets() ya da SizedBox() kullanabilirsin
- taşma hatalarını çözmek adına SingleChildScrollView() kullanabilirsin. eğer yatay taşıyorsa

```jsx
scrollDirection: Axis.horizontal
```

eğer bir resim fazla büyükse onu sınırlamak için de Expanded() kullanabilirsin.

- bir şeyi transparanlaştırmanın 2 yolu vardır
    - opacity() ile wrap et
    - eğer resimse color: metoduyla
- `const` değişkenler compile-time, `final` değişkenler run-time çalışır. ikisi de sonradan değiştirilemez, ilklendirilmek zorundadırlar.
- `as` takısıyla bir değişkende veri tipi spesify edebilirsin

```dart
var number = 1.5 as double;
var age = 35 as int;
late String name; // kotlindeki private lateinit var
```

- cascade yani **`..`** operatörü

```dart
class Person {
  String name = '';
  int age = 0;

  void printDetails() {
    print('Name: $name, Age: $age');
  }
}

void main() {
  var person = Person();

  // Without the cascade operator
  person.name = 'John';
  person.age = 30;
  person.printDetails();

  // With the cascade operator
  person
    ..name = 'Jane'
    ..age = 25
    ..printDetails();
}
```

- Parametre verirken ismi ile verebilmemiz için parametrelerin etrafında küme parantezi olması gerekiyor
- opsiyonel parametre

```dart
String fun(String a,[String b = 'name']);

void main() {
	fun("hello"); // hello name
	fun("hello", "bugra"); // hello bugra
}
```

- named parameters allow you to give spesific names in your function declaration

```dart
void main() {
  print(greet(name: 'Alice', greeting: 'Hello')); // Output: Hello, Alice!
}

String greet({String name, String greeting='def'}) {
  return '$greeting, $name!';
}
```

- ayrıca fonksiyonlara alias atayabilirsin

```dart
String fun(int a) { return a }

var myalias = fun;

print(myalias(3));
```

- expression body `=>` sayesinde returne gerek kalmadan direkt yazıyoruz

```dart
int square(int number) => number * number;
```

- nullable ifadeleri nasıl kullanabiliriz?

```dart
var myVar? = 4
myVar = myVar!+2 // null olmadıgını söyleyebiliriz
if (myVar != null) // diyebiliriz

```

- map

```dart
void main() {
  Map<String, int> my_map = {
    'ahmet':22,
    'mehmet':66,
    'john':11
  };

  my_map['john'] = 26; // modify

  my_map['jane'] = 50; // change

  my_map.remove('jane'); // remove

  my_map.forEach((key, value) { // iterate
    print('$key: $value');
  });
}
```

- named constructor sayesinde sınıfın belli bir örnegini cagırabilirsin

```jsx
  const HomeScreen.purple({super.key})
      : color1 = Colors.brown,
        color2 = Colors.deepOrange;
```

- Opacity(opacity:0.5) ile bir widgetin saydamligini degistirebilirsin
- when creating a `stateful` class you always need 2 more subclasses

```jsx
class Deneme extends StateFulWidget {
	const Deneme({super.key}); // constructor

	State<Deneme> createState() {
		return _DenemeState();
	}
}

class _DenemeState extends State<Deneme> {
	@override
	Widget build(context) {
		return xxx;
	}
}
```

- setState() fonksiyonunu yalnızca stateful’larda kullanabilirsin
- `positional arguments` vs. `named arguments`

```dart
positional:

void printInfo(String name, int age) {
  print('Name: $name, Age: $age');
}

void main() {
  printInfo('Alice', 30); // Positional arguments
}

named:

void printInfo({String name, int age}) {
  print('Name: $name, Age: $age');
}

void main() {
  printInfo(name: 'Alice', age: 30); // Named arguments
}

mix:

void printInfo(String name, {int age}) {
  print('Name: $name, Age: $age');
}

void main() {
  printInfo('Alice', age: 30); // Mix of positional and named arguments
}

```

- ekranın boyutunu öğrenmek ve ona göre widget tanımlamak için

```kotlin
    double sizeX = MediaQuery.of(context).size.width;
    double sizeY = MediaQuery.of(context).size.height;

    Container(
        width: sizeX,
        padding: EdgeInsets.all(sizeX / 20) ...
```

- Riverpod bilgi
    - **`ref.watch`:** This is used when you want your widget to rebuild automatically whenever the state of the provider changes. It’s typically used inside the `build` method for reactive updates.
    - **`ref.read`:** This is used when you only want to read or update the state without triggering a rebuild of the widget. It’s typically used in event handlers or places where you’re making a one-time update.
- dart’ta pythondaki gibi capitalize() metodu yoktur ama kendi string extensionini yazabilirsin

```dart
extension StringExtension on String {
    String capitalize() {
      return "${this[0].toUpperCase()}${this.substring(1).toLowerCase()}";
    }
}

var aa = "asd";
print(aa.capitalize()); // Asd
```

- flutter'da http request nasıl yapılır?
```dart
Future<void> fetchData() async {
  final response = await http.get('example.com/data');
  if (response.statusCode == 200) {
    // basarili
    final data = json.decode(response.body);
    print(data);
  }
}
```

- shared preferences fonksiyonlarının async yazılmasının sebebi bilgileri memory’e değil disk’e işlemesidir, bu da çok daha fazla zaman ve işlem yükü tutar. bunu da main thread’de yapmak tehlikelidir.

```dart
SharedPreferences prefs = await SharedPreferences.getInstance();
```

-  go_router (for page navigation. recommended way by flutter)

1) define a router

``` dart
final GoRouter _router = GoRouter(
  initialLocation: '/',
  routes: [
    GoRoute(path: '/', builder: (context, state) => HomeScreen()),
    GoRoute(path: '/login', builder: (context, state) => LoginScreen()),
  ],
);
```

2) materialApp'ini değiştir

``` dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final GoRouter _router = GoRouter(
    initialLocation: '/',
    routes: [
      GoRoute(path: '/', builder: (context, state) => HomeScreen()),
      GoRoute(path: '/login', builder: (context, state) => LoginScreen()),
    ],
  );

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router( // material.router
      title: 'My Flutter App',
      theme: ThemeData(primarySwatch: Colors.blue),
      routerConfig: _router,
    );
  }
}
```
3) use them

``` dart
context.go('/login');      // Replaces current page (like Navigator.pushReplacement)
context.push('/login');    // Pushes onto stack (like Navigator.push)
context.pop();             // Goes back (like Navigator.pop)
```

4) authentication check

``` dart

final GoRouter _router = GoRouter(
  redirect: (context, state) {
    final isLoggedIn = /* check your auth logic */;
    final isLoggingIn = state.location == '/login';

    if (!isLoggedIn && !isLoggingIn) return '/login';
    if (isLoggedIn && isLoggingIn) return '/';
    return null;
  },
  routes: [ /* your routes */ ],
);

```

* positional arguments vs. named arguments:
  * positional parametreleri dogru sirayla girmek zorundasın. [] for optional
  * named'ler ise isimle argümanlandirilirlar. {} for optional
```dart

void myFun(String name,[ int age = 0]) {
  print("Hi, my name is $name and I am $age years old.");
}

void myFun2({required String name, int age = 0}){
  print("Hi, my name is $name and I am $age years old.");
}

void main() {
  myFun("bugra", 24);
  myFun2(name: "bugra");
}
```

* Flutter uses a rebuild + diffing approach:
  * When state changes → build() is called again.
  * Flutter creates a new widget tree.
  * It compares the new tree with the old tree (from previous build).
  * It checks which widgets changed and which stayed the same.
  * Only the changed parts of the UI are repainted.

* BuildContext is an object that represents the location of a widget in the widget tree.

* `final`, `const` ve `static` farkı:
  * final ile tanımladıgın bir degisken compile-time'da bilinmez, run-time'da bilinir ve sonrasında degismez. `final date = DateTime.now()` gibi.
  * const ile tanımladıgın da degismez, ama compile-time'da bilinir. `const pi = 3.14`
  * static ise belli bir instance'a degil sınıfa aittir. sınıfın bütün objeleri tarafından paylasılır.
* bir fonksiyona parametre olarak fonksiyon verme (onclick)
```dart
void greet(String yourGreet, void Function() onClick) {
  print("$yourGreet");
  onClick();
}

// when you call it
greet("hello", () {
  print("this is onclick");
});
```
* fat arrow notation: => `onclick => greet()`
* `mount` olayı nedir? stateful widgetlarda kullanilir, asenkronize functionlarla. setState() degistirecegin degiskenin var oldugundan emin olmak için kullanılır. disposed bir widgetla kullanılmasın diye.

```dart
class MyWidget extends StatefulWidget {
  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  String data = 'Loading...';

  @override
  void initState() {
    super.initState();
    loadData();
  }

  Future<void> loadData() async {
    await Future.delayed(Duration(seconds: 2));

    if (!mounted) return;  // Safe check before setState

    setState(() {
      data = 'Data Loaded';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text(data);
  }
}
```
* `mixin` nedir? mixinler flutterda bir sınıftan inherit etme olayını kaldırır. bir metodu farklı sınıfların kullanabilir hale gelir:
```dart

// class yerine mixin diyoruz
mixin merhabaMixin {
    String isim = 'bugra';
    void merhabaDe() => print("merhaba, $isim");
}

// daha sonra bir sınıftan bu mixin'i `with` ile aliyoruz
class Deneme with merhabaMixin {
  merhabaDe();
}

void main() {
  Deneme deneme = Deneme();
  deneme.merhabaDe(); // merhaba, bugra
}
```
bazen de de bir mixini sadece istedigin bir sınıf kullanabilsin istersin. o zaman da `on` anahtar kelimesini kullanırsın
```dart
class Deneme {
  String isim = 'bugra';
}

mixin MerhabaMixin on Deneme {
  void merhabaDe() => print("merhaba, $isim");
}

class DenemeAlt extends Deneme with MerhabaMixin {}

void main() {
  DenemeAlt d = DenemeAlt();
  d.merhabaDe(); // ✅ works fine
}
```
burada şuna dikkat et: `on` kullanacaksan üçüncü bir sınıfa ihtiyacın var. direkt Deneme + Mixin yapamiyorsun çünkü ikisinin de ilklendirilmiş olması lazım.
* null-aware operators
  * ?.
  * ??
* `image.network` ile `NetworkImage` farkı: image.network direkt olarak foto yüklemeni sağlayan bir **widget**tir. NetworkImage ise bir widget degil bir photo provider olarak calısır. fotografın kendisini degil adresini tutar.
* what is `async`, `await` and `future` in flutter?
  * **async**, bir fonksiyonu asenkronize flagleyen anahtar kelimedir. böylelikle fonksiyon içerisinde await calıstırabilir.
  ```dart
  Future<void> loadData() async {
    print('Start loading...');
    await Future.delayed(Duration(seconds: 2)); // 2 saniye bekler
    print('Finished loading');
  }
  ```
  * **await** fonksiyonun beklemesini saglayan kelimedir. genelde httplerde kullanılır:
  ```dart
  import 'package:http/http.dart' as http;

  Future<void> fetchData() async {
    var url = Uri.parse('https://jsonplaceholder.typicode.com/todos/1');
    var response = await http.get(url);

    if (response.statusCode == 200) {
      print('${response.body}');
    } else {
      print('Hata: ${response.statusCode}');
    }
  }

  void main() async {
    await fetchData(); // Future fonksiyon olduğu için await gerekiyor
  }
  ```
  * **Future** değişkenler ve fonksiyonlar ileride ilklendirilecek olan şeylerdir. asenkronize calısır. http requestleri, delaylerde vs. kullanılır.
  ```dart
  Future<String> fetchData() {
    return Future.delayed(Duration(seconds: 2), () {
      return 'Data Loaded'; // cagrıldıktan 2 saniye sonra calısır
    });
  }
  ```
* what is `vsync`? The vsync in Flutter is an abbreviation for "vertical synchronization". It's a feature that ensures that animations and user interface updates are synchronized with the device's screen refresh rate. This prevents visual artifacts, such as screen tearing or stuttering,
* `assert` ne için kullanılır?
```dart
int score = 50;
assert(score >= 60, "Score must be at least 60");
```
eğer 60'tan düşükse puanin, 2nd argüman yazdırılıyor. boolean check için kullanılır.
* `FutureBuild` nedir? bir stream halinde geliyorsa Future objeler bunu kullaniyosun:
```dart
import 'package:http/http.dart' as http;

Future<List<String>> _fetchData() async {
  return Future.delayed(
    Duration(seconds: 2),
    () {
      return ["Item 1", "Item 2", "Item 3"];
    },
  );
}

void main() async {
  print('Application started. Fetching data...');

  try {
    final List<String> data = await _fetchData();

    print('\n--- Data Fetched ---');
    if (data.isEmpty) {
      print('No items found.');
    } else {
      for (var i = 0; i < data.length; i++) {
        print('${i + 1}. ${data[i]}');
      }
    }
    print('--------------------\n');
    print('Application finished successfully.');
  } catch (e) {
    print('Error: $e');
  }
}
```
* flutter'da singleton yaratmanın en kolay yolu: Factory Constructor kullan. 3 seye ihtiyacın var: static instance yarat, factory constructor yarat, instance'ini döndüren static method yarat.

```dart
class MySingleton{

  // 1. static ile sunu basarıyor: bu instance sınıfa ait, objeye degil. tek & unique
  static final MySingleton _instance = MySingleton._internal(); // _makes private

  // normalde, her MySingleton() cagırısında, mesela
  //  var mySingleton = MySingleton();
  //  var mySingleton2 = MySingleton(); [2 farklı obje yaratılır]
  // ama 2. factory constructor sayesinde bu sınıfı singleton yapiyosun,
  // sınıftan ikinci bir obje türetemiyosun.
  factory MySingleton() {
    return _instance;
  }

  // 3. private named constructor
  MySingleton._internal();

  // bu 3 seyle singleton yaratmıs oluyosun

}

// ----------------

var obj1 = MySingleton();
var obj2 = MySingleton();

print(obj1 == obj2); // TRUE
```

* There are two main types of tests in Flutter: unit tests and integration tests. Unit tests focus on individual pieces of code, such as a single function or widget, and test their behavior in isolation. Integration tests, on the other hand, test the app as a whole, including the interactions between different parts of the app. `flutter_test` paketini kullanabilirsin.

* how do you pass data between screens? sayfanda constructor olarak alırsın:

```dart

Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondScreen(data: 'Hello World!'),
  ),
);

// -------------

class SecondScreen extends StatelessWidget {
  final String data;

  SecondScreen({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold( ... );
  }
}

```

* how to create a draggable widget?

```dart
Draggable<int>(
  data: 1,
  feedback: Material(
    color: Colors.transparent,
    child: Icon(Icons.access_alarm, size: 50),
  ),
  childWhenDragging: Container(),
  child: Icon(Icons.access_alarm),
)
```

* 
