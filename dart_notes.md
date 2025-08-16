# Dart Notes

* dart is both strongly typed and not. `int a`, `String b` vs. `var c`, `dynamic d`.

* benzer bir şekilde dart, hem interpreted hem compiled olarak çalışır.
* spread operator:
	```dart
	var list = [1, 2, ...otherList, 6];
	var otherList = [3, 4, 5];
	```
* cascade operator:
	```dart
	var obj = Object()
	..method1()
	..method2();
	```

* dart'ta interfacelere özel bir anahtar kelime yoktur. interface'leri blueprint gibi düşünebilirsin. içerisine içi boş metot isimleri yazarsın, bu arayüzü kullanan diğer sınıflar da (dartta bunu `class .. implements ...` ile yaparsın) bu metotları override etmek zorundadır. böylelikle hangi sınıfların hangi metotlara mutlaka sahip olacağını garanti edersin. bu sorun, java, dart vs. gibi dillerdeki multiinheritance olayının olmayışına bir çözüm olarak sunulur.

	```dart
	class MyInterface {
		void doSomething();
		}

		class MyClass implements MyInterface {
		// MyClass must implement the doSomething method
		void doSomething() {
			print('Class implementing interface');
		}
	}
	```
* dartta farklı constructor türleri
  * default constructor: class içerisinde constructor yazmadığımız, otomatik olarak kendinin anladıgı tür:
	```dart
	class Araba {
		String? marka;
		int? modelYili;

		// Default constructor'ı biz yazmasak bile bu şekilde arka planda mevcut.
		// Araba();
		}

		void main() {
		var araba1 = Araba(); // Default constructor ile nesne oluşturma
		araba1.marka = 'ford';
		araba1.modelYili = 2000;

		print(araba1.marka);
		print(araba1.modelYili);
	}
	```
  * parametre constructor: class içerisinde kendimiz yazariz constructori
	```dart
	class Araba {
		String marka;
		int modelYili;

		// Parametreli constructor
		Araba(this.marka, this.modelYili);
		}

		void main() {
		// Parametreli constructor ile nesne oluşturma
		var araba2 = Araba('Mercedes', 2023);

		print(araba2.marka);     // Çıktı: Mercedes
		print(araba2.modelYili); // Çıktı: 2023
	}
	```
  * named constructor: bütün parametreli vermek istemediğimiz durumlarda named constructor kullanırız
	```dart
	class Araba {
		String name;
		int model;
		String renk;

		Araba.ucuzAraba(this.name, this.model) : renk = 'Bilinmiyor';
		// Araba.ucuzAraba(this.name) : model = 0, renk = 'Bilinmiyor';
		}

		void main() {
		var araba = Araba.ucuzAraba('clio', 2001);

		print(araba.name);
		print(araba.model);
		print(araba.renk);
	}
	```
  * factory constructor: singleton yaratmada kullanılır. bir sınıftan sadece bir obje üretilebilir.
  ```dart
	class Logger {
		static final Logger _instance = Logger._internal();

		factory Logger() {
			return _instance;
		}

		Logger._internal();
	}
  ```
* Must Know in OOP:
  * Polymorphism
    * compile-time polymorphism
      * function overloading
      * operator overloading
    * run-time polymorphism
      * function overriding
      * virtual functions
  * Abstraction
    * data abstraction
    * process abstraction
  * Inheritance
    * public inheritance
    * private inheritance
    * protected inheritance
  * Encapsulation
    * data hiding
    * access control
* 
