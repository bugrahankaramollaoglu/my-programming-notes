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
- for hotReload to work, you should use a stateless or stateful widget.
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

- as you know dart is an OOP language. learn more: https://medium.com/@bugrahankaramollaoglu/pillars-of-oop-ed42fb6d29e8
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

ya da eğer stateful widget'sa

```dart


class SecondScreen extends StatefulWidget {
  final String mesaj;

  SecondScreen({super.key, required this.mesaj});

  @override
  State<SecondScreen> createState() => _SecondScreenState();
}

class _SecondScreenState extends State<SecondScreen> {
  @override
  Widget build(BuildContext context) {

    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => CounterPage()),
            );
          },
          child: Text(widget.mesaj), // widget. ile erişirsin
        ),
      ),
    );
  }
}

```

ikinci bir alternatif ise argümanlı Navigator.pushNamed kullanmak:
```dart
Navigator.pushNamed(context, '/second', arguments: 'Hello');
```
daha sonra bunu gittigin sayfada söyle almak:
```dart
final String data = ModalRoute.of(context)!.settings.arguments as String;
```

ücüncü alternatif ise state managementlar kullanmak, riverpod vs.

dördüncü alternatif sharedPref, dataStorage vs. kullanmak

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

* widget lifecycles in flutter. flutter'da 2 çeşit widget vardır: `Stateful Widget` ve `Stateless Widget`.
	* stateless widget'ın bir tane döngüsü vardır sadece:
```dart
@override
Widget build(BuildContext context) {
  // Called whenever the widget needs to be rebuilt
}
```
setState() sadece `stateful widget`ta calısır. ama diger tür state managementlar her ikisinde de çalışır.
* bir değişken lazy ise sadece kullanıldıgında yaratılır. verimlilik için.
* flutter'da `listview` ile `listview.builder` arasındaki fark nedir?
	* **listview** kullanırsan tüm ögeleri baştan oluşturur ve bellekte tutar. ögelerin sayısı küçük ve sabitse mantıklı. ama değilse performans açısından kötüdür.
	* **listview.builder** ise sadece ekranda o an ne görünüyorsa onu draw eder. kaydırdıkça yeni ögeleri yükler. performanslıdır.

* bütün sayfaların appbarlarının rengini tek seferde nasıl değiştiririm? tema üzerinden:
```dart
MaterialApp(
  title: 'My App',
  theme: ThemeData(
    appBarTheme: AppBarTheme(
      color: Colors.red,  // Bütün AppBar'lar kırmızı olacak
    ),
  ),
  home: MyHomePage(),
);
```

* mesela bir text tanımladın, ona özellikler verdin bir sürü ama bu özellikleri başka text'lerde de kullanmak istiyosun. tekrar tekrar yazmak istemiyosun? bu durumda bu texti bir componente çevirirsen daha sonra kullanabilirsin:

```dart
class CustomStyledText extends StatelessWidget {
  final String text;
  final TextAlign? textAlign;

  const CustomStyledText(this.text, {Key? key, this.textAlign}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Text(
      text,
      textAlign: textAlign,
      style: const TextStyle(
        fontSize: 18,
        fontStyle: FontStyle.italic,
        fontWeight: FontWeight.bold,
        color: Colors.amber,
      ),
    );
  }
}
```
bunu daha sonra söyle kullanabilirsin:
```dart
  body: Center(
    child: CustomStyledText('asd'),
  ),
```

* const kullanınca Flutter o widget’ı bir kere oluşturup tekrar tekrar yeniden oluşturmaz, bellekte aynı instance’ı kullanır. Böylece gereksiz tekrar işlemlerini engeller.
* flutter'da `event loop` nedir? yazdıgın flutter kodunu sırayla isleyen motora denir. flutter, single thread calısır, böylece UI donmaz. uzun süren islemleri (Future, async/await vs.) yan threadde yapmalısın. ana thread'e `main isolate` denir.
* flutter'da, initstate() içerisinde yazdıgın şeyler widget-tree henüz build edilmeden calışır, sayfa ilk yüklendiğinde. widgetların yüklenmesini beklemek istiyosan `addPostFrameCallback` metodunu kullanabilirsin (ideal yöntem):
```dart
@override
void initState() {
  super.initState();

  WidgetsBinding.instance.addPostFrameCallback((_) {
    // Burada widget build edildikten sonra yapılacak işlemleri yazabilirsin
    setState(() {
      backgroundColor = Colors.red;
    });
  });
}
```
bir başka alternatif de `Future.delayed` kullanmaktır. o da şöyle çalışır:
```dart
@override
void initState() {
  super.initState();

  Future.delayed(Duration.zero, () {
    // Widget build edildikten sonra çalışır
    setState(() {
      backgroundColor = Colors.red;
    });
  });
}
```
yine bir başka alternatif ise stateful widget yaşamdöngülerinden olan `didChangeDependencies()` altında yazmaktır:
```dart
@override
void didChangeDependencies() {
  super.didChangeDependencies();
  // Bu method context erişimine uygundur
  // ve build'den hemen önce çalışır.

  // Ancak dikkat: bu method initState'ten sonra çalışır
  // ama build tamamlanmadan önce tetiklenir.
}
```
* sonuç ne olur?
```dart
void main() {
  for (int i = 0; i < 10; i++) {
    if (i.isOdd) {
      print("$i");
    } else {
      Future.delayed(Duration(seconds: 1)).whenComplete(() {
        print("$i");
      });
    }
  }
}
```
şu çıktıyı verir: 1 3 5 7 9 0 2 4 6 8. neden? çünkü flutter'da event loop denilen olay, önce senkronize işlemleri yapar (normal tasks). ancak onlar bittikten sonra asynchronous işlemlere (Future) geçilir. geçilene kadar bunlar heap'te tutulur.

* flutter'da viewmodel oluşturmak native android'den biraz farklıdır. android'de ViewModel() sınıfından inherit ediyorduk. flutter'da ise viewmodellar genelde Provider/Riverpod gibi statemanagementlar yardımıyla implemente ediliyor. 3 yolu var:
  * En sık kullanılan yolu, kendi vm'in + ChangeNotifier kullanmak
  ```dart
  class MyViewModel extends ChangeNotifier {
    int count = 0;

    void increment() {
      count++;
      notifyListeners();
    }
  }
  ```
  * hiçbir kütüphane kullanmadan basit bir sınıf yaz:
  ```dart
  class MyViewModel {
    int count = 0;

    void increment() {
      count++;
    }
  }
  ```
  fakat bu yöntemde notifyListeners() gibi UI'ya haber veremezsin. Kendin setState() ile UI’ı yeniden çizmelisin.
  * Provider, Riverpod, BloC gibi sm'lar kullanmak
* different build types in flutter:
  * **debug**: when developing the app. _hotReload_ is allowed. uses JIT (Just-In-Time) compilation. It compiles the Dart code into machine code at runtime, allowing for hot reload and fast development cycles.
  * **production**: when in production. only _hotRestart_ is allowed. uses AOT (Ahead-Of-Time) compilation. It compiles the Dart code into native machine code ahead of time, resulting in faster startup times and improved performance.

* what are `Future` and `Streams` in flutter? asenkron programlamada kullanılan kavramlardır. Future tek bir value dönerken Stream birçok value döner sürekli olarak.
* `get_it` is used for dependency injection.

* flutterda kotlindeki gibi `data class` ve `class` farkı yoktur. modelleme yaparken class kullanır ve fonksiyonları (toString vs.) override ederiz. maalesef. ama data class haline getiren `freezed` kütüphanesi kullanabilirsin.

*  More precise phrasing helps: Future represents a value that will be available later; async marks a function as asynchronous; await pauses execution until a Future completes.

* In a `Future` function, saying the main thread is blocked is inaccurate — Dart uses an event loop and does not block the UI thread.
*
* flutter'da class constructor yazarken `{}` kullanmak zorunda değilsin `EĞER Kİ` positional parameter ise. named parameter ise zorundasın.

* Stateful widget'ın ise **8** tane yaşamdöngüsü vardır. bunlara `view lifecycle methods` denir:
  1. `createState()`: statefulWidget ilk defa *yaratılma emri verildiginde*, flutter ilk olarak bu metodu cagırır.
  artık `mount` propertysi true oldu bu widgetin. When createState creates your state class, a buildContext is assigned to that state. buildContext is the place in the widget tree in which this widget is placed. All widgets have a bool this.mounted property. It is turned true when the buildContext is assigned. It is an error to call setState when a widget is unmounted.
  2. `initState()`: widgetin ilk *yaratıldıgında* cagrılır. sadece bir kez calısır.
  3. `didChangeDependencies()`: initState'ten hemen sonra cagrılır. sınıfın bağımlılıklarından biri değiştiğinde.
  4. `build()`: widget treeni sürekli rebuild eden metot. içine BuildContext alır. didChangeDependencies'ten hemen sonra execute edilir.
  5. `didUpdateWidget()`: parent class'ın yeni bir veri gönderdi, ama statefulWidget'ının tamamen değişmesi gerekmiyor. flutter o zaman rebuild etmez, bu metodu cagırır ve `oldWidget` ile `yeniWidget`i karsılastırır.
  6. `setState()`: verilerin degistigini haber verir ve real-time UI'i günceller.
  7. `deactivate()`: state widgetTree'den silindiginde calısan metot (ama kaynakları hala tutuyor). mesela bir video uygulaması düşün, kullanıcı başka sekmeye geçiyor ama geri de dönebilir. hem nerede kaldıgının bilgisini tutman lazım hem de bu video widgetini ekrandan silmen lazım. bunu deactive() sayesinde yapiyosun.
  8. `dispose()`: state tamamen kaldırıldı. memory free edilir. `mount` objesi false yapilir.

* Platform Channel nedir? Flutter ile native (Kotlin/Swift) kod nasıl çalıştırılır? Flutter uygulamaları çoğunlukla Dart kodu ile yazılır ama bazı durumlarda native platform (Android/iOS) ile iletişim kurulması gerekir. Bunun için Flutter, Platform Channels yapısını sağlar. Yani flutterda native kodları (kotlin/swift vs.) calıstırmak icin kullandıgımız mekanizmaya `platform channels` deniyor. 3 temel platform channel türü var
  * method channel: en yaygını. flutter->native / native->flutter veri alıp gönderir. mesela kamera erişimi, GPS konum alma, cihaz bilgisi vs. **anlık** veri.

  * event channel: native->flutter'a sürekli veri gönderir. jiroskop, canlı konum vs. **sürekli** veri. method channeldan en büyük farkı bu.

  * basicMessageChannel: flutter->native / native->flutter basit veri alip gönderir. **iki taraflı** sürekli veri.

* Dio paketini kullanarak JWT ile korunan bir API’ye nasıl istek atarsın? Token'ı nasıl saklarsın ve her isteğe otomatik olarak nasıl eklersin? Interceptor nedir?
  * flutterda bir token'ı güvenli bir şekilde saklamak için en sık kullanılan kütüphane `flutter_secure_storage` kütüphanesidir.
  ```dart
  final storage = FlutterSecureStorage();

  // Token saklama
  await storage.write(key: 'jwt_token', value: token);

  // Token okuma
  String? token = await storage.read(key: 'jwt_token');
  ```
* Eğer çok büyük bir listeyi (örneğin 10.000 öğe) göstermen gerekiyorsa performansı nasıl optimize edersin? Builder dışında ne tür optimizasyonlar yaparsın?
  * Mümkün olan yerlerde const constructor kullanarak widget’ların yeniden oluşturulmasını önlersin. Bu sayede Flutter, aynı widget’ı yeniden çizmek yerine cache’den kullanır.
  * listview.builder şart, ama yeterli değil. listview.builder içerisinde `cacheExtent` diye bir ayar var. bu listede ilk kaç px ön ve arkadaki elemanların önyüklenecegini belirliyor. cok verirsek hafıza sorunu yaşarız, az verirsek kaydırırken ögeler tam yüklenmeyebilir. optimize etmek zorundasın:
    ```dart
    ListView.builder(
      cacheExtent: 500, // px cinsinden
      ...
    )
    ```
  * Image veya Ağ Kaynaklı Büyük Veriler İçin `cached_network_image` veya benzeri cache kullanımı Eğer listende çok sayıda resim varsa, networkten gelen resimleri önbelleğe almak performansı ciddi artırır.
    ```dart
    CachedNetworkImage(
      imageUrl: 'https://example.com/image_$index.jpg',
      placeholder: (context, url) => CircularProgressIndicator(),
      errorWidget: (context, url, error) => Icon(Icons.error),
    );
    ```
  * StatelessWidget kullanmak, gereksiz rebuild’leri engeller.
  * `repaintBoundary` kullan. Bir widget’ı RepaintBoundary ile sarmaladığında, o widget ve alt widgetları kendi ayrı "paint layer"ına taşınır. Böylece sadece o bölge değiştiğinde yeniden çizilir, tüm liste değil. mesela:
    ```dart
    ListView.builder(
      itemCount: 10000,
      itemBuilder: (context, index) {
        return RepaintBoundary(
          child: ListTile(
            title: Text('Öğe $index'),
          ),
        );
      },
    )
    ```
* Flutter'da responsive (duyarlı) tasarım için hangi yöntemleri kullanırsın? Tablet ve telefon ekranlarında aynı UI’yi farklı göstermek için nasıl bir yapı kurarsın?
  * build() altında mediaQuery teknigi sayesinde sürekli bir şekilde ekranın boyutunu ögrenirim (ki rotationlarda vs. sorun cıkmasın). mesela width>600 ise tablete göre telefonsa daha küçük fontlar vs. veririm.
  * `flutter_screen_util` paketini kullanarak relative boyutlar veririm: 60.w gibi
  * `LayoutBuilder` kullanırım.
  * `Expanded`, `Flexible` vs. kullanabilirsin.
* FutureBuilder nedir? Ne zaman FutureBuilder kullanırsın, ne zaman StreamBuilder? Aralarındaki fark nedir? Alternatif olarak ne kullanırsın ve neden?
  * `FutureBuilder`, tek seferlik asenkron işlemler için kullanılır. dönüş tipi `Future<>`'dır. Sadece bu future fonksiyon tamamlandıgında UI güncellenir.
    ```dart
    Future<String> fetchData() async {
      await Future.delayed(Duration(seconds:4));
      return "Veri yüklendi";
    }

    FutureBuilder<String>(future: fetchData(), builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return CircularProgressIndicator();
          } else if (snapshot.hasError) {
            return Text("Hata: {$snapshot.error}");
          } else if (snapshot.hasData) {
            return Text(snapshot.data!);
          }
          return Container();
    })
    ```
  * `StreamBuilder` sürekli gelen asenkron işlemler için kullanılır. dönüş tipi `Stream<>`'dir.
    ```dart
    Stream<int> counterStream() async* {
      for (int i = 0; i <= 10; i++) {
        await Future.delayed(Duration(seconds: 1));
        yield i;
      }
    }

    StreamBuilder<int>(
          stream: counterStream(),
          builder: (context, snapshot) {
            if (!snapshot.hasData) return CircularProgressIndicator();
            return Text('sayaç: ${snapshot.data}');
          },
    )
    ```
* Bir widget gereksiz yere sürekli rebuild ediliyor. Bunu nasıl tespit eder ve nasıl engellersin? Flutter’da performans için hangi araçları ve yöntemleri kullanırsın?
  * devTools'tan hangi widgetin fazla rebuild edildigine bak
  * o widget'i const yap + o stateless widgetin constructorini widget yap. artık o widget güncellenmedikçe rebuild edilmeyecek.
* MVVM kullandığını söyledin. Peki Clean Architecture ile MVVM arasında fark var mı? Flutter’da Clean Architecture kullanmak ister misin, neden?
  * `mvvm`: Flutter’da ViewModel, genelde bir ChangeNotifier, StateNotifier, Bloc veya Provider ile temsil edilir. Model-View-Viewmodel olarak 3 katmandan oluşur.
  * `clean architecture`: Uygulamanın tüm katmanlarını katı kurallarla ayırmayı amaçlar. Test edilebilirlik, sürdürülebilirlik. Bağımlılık ilkesi: Dış katmanlar, iç katmanlara bağımlı olabilir ama tersi OLAMAZ.`cleanArch` katmanları:
    * 1. `domain` (Entity, Repository): ilk katman. Temel iş mantığı (mesela getAllUsersCase). saf kurallar. diğer katmanlara bağlı değil. burada Model Entity'sini yazarsın.
    * 2. `data` (API, Database vs): orta katman. domain'e bağlıdır ama presentation'dan bağımsızdır. Veri kaynakları. Modeller, ApiServices vs. burada olur. burada api/db ile iletişim kurarız. domain'de yazdıgın interfaceleri burada Repository implementation ile kullanırsın. buradaki model API'dan gelen json verisini temsil eder. Api isteklerini atar (fetchData() gibi).
    * 3. `presentation` (UI, View + Viewmodel): son katman. kullanıcının gördügü kısım. state yönetimi burada yapılır (riverpod vs.) Widgetlar, Aktiviteler, ViewModellar burada olur. API ile doğrudan konuşmazsın, sadece apiCall'lari yaparsin.
    * 4. `application` main.dart
* Eğer uygulamada 3 farklı sekme varsa (örneğin BottomNavigationBar ile), her sekmede kendi navigation stack’i varsa bunu nasıl yönetirsin? Nested navigation nedir?
  * her sayfaya ayrı bir navigation_key tanımlarız (`GlobalKey<NavigatorState>()`)
  * go_router ile de yapabiliyoduk.
* Flutter'da isolate nedir? compute fonksiyonu ne işe yarar? async ile farkı nedir?
  * Isolate, Dart’ın çoklu iş parçacığı (thread) gibi ama aslında ondan bağımsız çalışan, hafızası ve event loop’u ayrı olan paralel çalışma ortamıdır.
  * Yani her isolate kendi hafızasına ve kod akışına sahiptir, başka isolate’lar ile paylaşımlı hafıza yoktur.
  * Bu, Flutter’da UI thread’ini (ana thread) bloklamadan, arka planda ağır işlemleri yapabilmek için kullanılır.
  * UI thread, uygulamanın arayüzünü çizer ve kullanıcı etkileşimlerini işler. Uzun süren işlemler burada yapılırsa uygulama donar (frame drop, lag olur).
  * async/await'ten farkı async/await aynı thread üzerinde basit işlemler yapar, sadece delayed bir şekilde çalışır. isolate ise kendi iş threadini yaratır ve çok daha büyük computation gerektiren zamanlarda kullanılır.
* basit -> setState, orta -> riverpod, profesyonel -> bloC
* cached_network_image
  * internetten çektiğin resimleri önbelleğe alarak yükleme hızını arttıran flutter paketi.
* Riverpod'un amacı nedir? Riverpod’da Provider, StateProvider, FutureProvider, Notifier farkları nedir? Riverpod kullanarak basit bir sayaç uygulamasını nasıl yazarsın? Kodu yaz.
* Widget tree nasıl çalışır? Build sürecinde neler olur? Widget’ların parent-child ilişkisi neden önemlidir? Widget’ların fazla derin olması (deep widget tree) performansı nasıl etkiler? Bunu önlemek için neler yaparsın?
* flutterda singleton nasıl yaratılır?
```dart
  class Logger {
    static final Logger _instance = Logger._internal();

    factory Logger() {
      return _instance;
    }

    Logger._internal(); // Private named constructor

    void log(String message) {
      print("Log: $message");
    }
  }
```

* http/dio ile api verisi çekerken profesyonel düzeyde hata kotrolü yapmak istiyosan statusCode==200 yeterli değildir:
```dart
Future<void> fetchData() async {
  try {
    final response = await http.get(Uri.parse('mydata.com/users'));
    if (response.statusCode == 200) {
      // API'den veri başarıyla çekildi
    } else {
      // Hata mesajı göster
      throw Exception('Veri çekme başarısız oldu (${response.statusCode})');
    }
  } on SocketException {
    // Ağ bağlantısı yoksa
    throw Exception('Ağ bağlantısı yok');
  } on TimeoutException {
    // İstek timeout olduysa
    throw Exception('İstek timeout oldu');
  } catch (e) {
    // Diğer hatalar
    throw Exception('Bilinmeyen hata: $e');
  }
}
```
ama çoğu zaman bu da yetmez. mesela bir provider/riverpod içerisinde kullanıcıya ekranın loading/finish halini nasıl gösterebiliriz? viewmodel + isLoading flag yardımıyla:

```dart
class MyViewModel with ChangeNotifier {
  bool _isLoading = false;
  String? _errorMessage;

  bool get isLoading => _isLoading;
  String? get errorMessage => _errorMessage;

  Future<void> fetchData() async {
    _isLoading = true;
    notifyListeners();

    try {
      // fetchData implementasyonu
      final response = await http.get(Uri.parse('mydata.com/users'));
      if (response.statusCode == 200) {
        // API'den veri başarıyla çekildi
      } else {
        _errorMessage = 'Veri çekme başarısız oldu (${response.statusCode})';
      }
    } on SocketException {
      _errorMessage = 'Ağ bağlantısı yok';
    } on TimeoutException {
      _errorMessage = 'İstek timeout oldu';
    } catch (e) {
      _errorMessage = 'Bilinmeyen hata: $e';
    } finally {
      _isLoading = false;
      notifyListeners();
    }
  }
}
```

* mesela bir sayfadan başka bir sayfaya geçiyorsun ve bu sayfada bazı verileri göstermek istiyorsun. Ancak, bu verileri göstermek için bazı async işlemler yapman gerekiyor. Bu async işlemler sırasında sayfa değişirse ne olur? Bunu nasıl yönetirsin?
  * `mounted` teknigiyle. mounted, bir stateful widgetin destroy edilip edilmedigini sorar.
    ```dart
    class MyPage extends StatefulWidget {
      @override
      _MyPageState createState() => _MyPageState();
    }

    class _MyPageState extends State<MyPage> {
      bool isLoading = true;

      @override
      void initState() {
        super.initState();
        loadData();
      }

      Future<void> loadData() async {
        // API çağrısı simülasyonu
        await Future.delayed(Duration(seconds: 2));

        // Widget hala mount edilmiş mi kontrol et
        if (mounted) {
          setState(() {
            isLoading = false;
          });
        }
      }

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          body: isLoading ? CircularProgressIndicator() : Text('Veri yüklendi'),
        );
      }
    }
    ```
* `provider` nedir? bir state managementtir. en basit işler için kullanılır. provider'i bilmek istiyosan 3 şeyi bilmen gerek:
  * **changeNotifier** is a simple class that offers change notifications to its listeners. namely, if something is a *ChangeNotifier*, you can subscribe to it (Observable in android). basit uygulamalarda genelde bir ChangeNotifier sınıfı provider kullanmaya yetiyor. provider için changeNotifier şart değil ama genellikle tercih edilir.
    ```dart
    class CartModel extends ChangeNotifier {
      /// Internal, private state of the cart.
      final List<Item> _items = [];

      /// An unmodifiable view of the items in the cart.
      UnmodifiableListView<Item> get items => UnmodifiableListView(_items);

      /// The current total price of all items (assuming all items cost $42).
      int get totalPrice => _items.length * 42;

      /// Adds [item] to cart. This and [removeAll] are the only ways to modify the
      /// cart from the outside.
      void add(Item item) {
        _items.add(item);
        // This call tells the widgets that are listening to this model to rebuild.
        notifyListeners();
      }

      /// Removes all items from the cart.
      void removeAll() {
        _items.clear();
        // This call tells the widgets that are listening to this model to rebuild.
        notifyListeners();
      }
    }
    ```
  * **changeNotifierProvider** is the widget that provides an instance of changeNotifier. it comes from the provider package. runApp'in icerigini bununla wrap ediyoruz.
    ```dart
    void main() {
      runApp(
        ChangeNotifierProvider(
          create: (context) => CartModel(),
          child: const MyApp(),
        ),
      );
    }
    ```
  * **consumer** is used when we start actually using our provider model.
    ```dart
    return Consumer<CartModel>(
      builder: (context, cart, child) {
        return Text('Total price: ${cart.totalPrice}');
      },
    );
    ```
  ama bazen UI'i güncellemesen de bir metot cagırman gerekebilir. bu tür durumlarda Consumer() kullanmak gereksizdir, UI ile işin yok çünkü. böyle bir durumda listen=false parametresini de ekleyerek (aktif olarak dinlemesine gerek yok cünkü) `Provider.of` kullanarak providerinda tanımladıgın bir metoda erişebilirsin:
  ```dart
  Provider.of<CartModel>(context, listen: false).clearData();
  ```
* flutterda hata yönetimi
  * try{catch}, özellikle api'la veri çekerken
  * snackbar, dialog vs.
  *
* flutter kendi grafik motoruyla çiziyor ekrana ögeleri, bu yüzden android ve ios'un kendi UI resimlerine ihtiyaç duymuyor, böylece daha hızlı çalışıyor. bu motor eskiden skia'ydı ama şimdi ios'a yeni bir motor geliştiriyolar, yakında androide de gelecek. rakipleri olan react native, xamarin vs. ise bağlı olduğu platformun kendi grafik ögelerini kullanır.
* What is the difference between "Debug Mode" and "Profile Mode" in Flutter development?
  *
* eğer listen statikse, gerek yok - ama dinamik bir listen varsa (animasyonlu, ekleme/çıkarmalı, sıralamalı vs.) Key (ValueKey, ObjectKey vs.) kullanman gerekebilir. mesela listenin elemanlarının yerini değiştirebilsin istiyosun kullanıcı, peki which item which nasıl hatırlayacaksın? UniqueObject sayesinde.
  * **GlobalKey**: A global key is unique across the entire app, and is useful when you need to identify a widget from a different part of the app.
  * **UniqueKey**: A unique key is unique within a widget's parent widget, and is useful when you need to identify a widget within a list of widgets.
  * **ValueKey**: A value key is based on a value, such as a string or an integer, and is useful when you need to identify a widget within a list of widgets based on its value.
* The onGenerateRoute intercepts route navigation requests and lets you dynamically control how routes (screens) are created — instead of using a fixed map of routes.
```dart
MaterialApp(
  onGenerateRoute: (RouteSettings settings) {
    switch (settings.name) {
      case '/':
        return MaterialPageRoute(builder: (_) => const HomePage());
      case '/second':
        final args = settings.arguments as String;
        return MaterialPageRoute(builder: (_) => SecondPage(message: args));
      default:
        return MaterialPageRoute(builder: (_) => const NotFoundPage());
    }
  },
);
```
! If you define both routes: {} and onGenerateRoute, the routes map takes precedence for known routes. Use one for clarity or ensure onGenerateRoute handles all.

* Can you explain the concepts of "Isolate" and "Event Loop" in Dart?
  * Flutter apps must be fast and responsive, especially on mobile. Dart achieves this through:
    * Single-threaded execution for UI (like JavaScript)
    * Isolates for concurrency (like lightweight threads)
    * An Event Loop for async task handling.
  * what is an ISOLATE in dart? An Isolate is an independent worker in Dart with its own memory and event loop. başka dillerdeki threadlere benzer ama threadlerden farklı olarak ortak bir hafızayı kullanmazlar. kendi hafıza alanları vardır isolatelerin. özellikle heavy computationlarda isolate kullanıyoruz:
  ```dart
    import 'dart:isolate';

    void heavyTask(SendPort sendPort) {
      int sum = 0;
      for (int i = 0; i < 1000000000; i++) {
        sum += i;
      }
      sendPort.send(sum);
    }

    void main() async {
      ReceivePort receivePort = ReceivePort();

      // creates a new isolate
      await Isolate.spawn(heavyTask, receivePort.sendPort);

      // data is sent via ports (like in microservices)
      receivePort.listen((message) {
        print('Result: $message');
        receivePort.close();
      });
    }
  ```
  * what is event loop? The Event Loop is the mechanism that manages asynchronous events (like I/O, timers, Futures, Streams) and schedules tasks for execution. bir flutter uygulaması nasıl çalışır?
    * Dart starts running main isolate.
    * Dart maintains two task queues:
      * Microtask queue (high priority)
      * Event queue (normal priority)
    * Event loop runs tasks in this order:
      * Run all microtasks
      * Then run one event task
      * Repeat…
  yani önce microtasklar (eventlooptakiler, async olmayanlar bitirilir, sonra async calısır). mesela:
    ```dart
    void main() {
      print('Start'); // WORKS #1

      Future(() => print('Future 1')); // WORKS #4
      scheduleMicrotask(() => print('Microtask 1')); // WORKS #3
      Future(() => print('Future 2')); // WORKS #5

      print('End'); // WORKS #2
    }
    ```
* Explain the different "types of Streams".
  * single-subscription stream: Delivers events to only one listener. (i.e http request)
    ```dart
    void main() {
      // Creating a single-subscription stream
      var streamController = StreamController<int>();

      // Adding a listener
      var subscription = streamController.stream.listen((data) {
        print('Received data: $data');
      });

      // Adding another listener would result in an error
      // var secondSubscription = streamController.stream.listen((data) {
      //   print('Another listener: $data');
      // });

      // Adding data to the stream
      streamController.add(42);

      // Cancelling the subscription when done
      subscription.cancel();
    }
    ```
  * Broadcast Stream: birden fazla listenera izin veriyor. Events are pushed to all listeners.
    ```dart
    void main() {
      // Creating a broadcast stream
      var streamController = StreamController<int>.broadcast();

      // Adding multiple listeners
      var subscription1 = streamController.stream.listen((data) {
        print('Listener 1 received data: $data');
      });

      var subscription2 = streamController.stream.listen((data) {
        print('Listener 2 received data: $data');
      });

      // Adding data to the stream
      streamController.add(42);

      // Cancelling the subscriptions when done
      subscription1.cancel();
      subscription2.cancel();
    }
    ```

* `Future` vs. `Stream` basit farkı:
```dart
Future<int> futureMethod(int a, int b) async {
  await Future.delayed(Duration(seconds: 1));
  return a + b;
}


void main() async {
  print('your answer: ');
  int result = await futureMethod(3, 5);
  print(result);
}
```
and
```dart
Stream<int> streamMethod(int item) async* {
  for (int i = 1; i <= item; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

void main() async {
  print('your answer: ');
  await for (var val in streamMethod(5)){
    print(val);
  }
}
```
or here is another alternative for stream usage instead of `await for`:
```dart
void main() async {
  print('your answer: ');
  streamMethod(5).listen((value) {
    print(value);
  });
}
```
* flutterda abstract class ile interface farkı:
	* abstract class kendi instantiate edilemeyen sınıflara denir. works as _blueprints_ for other classes. içinde hem abstract (gövdesiz) hem concrete (gövdeli) metotlar barındırabilir. başka sınıflar **extend** ile miras alır bir abstract class'tan. miras alan sınıf, abstract metotlari overrride etmek zorundadır.
	```dart
	abstract class Animal {
	  void makeSound(); // abstract method
	  void breathe() {  // concrete method
	    print("Breathing...");
	  }
	}

	class Dog extends Animal {
	  @override
	  void makeSound() {
	    print("Bark!");
	  }
	}
	```
	* interface konusu da şöyle: flutter'da bütün sınıflar inherently interface'tir. Bir sınıfın interface’ini kullanmak için **implements**  anahtar kelimesi kullanılır.
	
	
	
* flutterda **provider**in avantajları, dezavantajları
	* temel InheritedWidget anlayışı üzerine kurulu
	* hem senkron hem asenkron değişkenleri ve metotları takip edebiliyor
	* büyük projelerde diğer state managementlar daha mantıklı hale gelir. 	
	
	
	
