# kotlin notları

- bir arrayin indisleri arasında gezinmek istiyosan

```kotlin
val arr = intArrayOf(0, 4, 2, 61)
for (i in arr.indices) {
	arr[i] // 0, 4, 2, 61 ... diye gider
}
```

- higher order fonksiyonlar bir fonksiyonu parametre olarak alan ya da fonksiyon döndüren fonksiyonlara denir. map, forech ve filter() gibi
- aynı satırda birden fazla değişkene koşullu değer atamak istiyosan

```kotlin
val (shorter, longer) = if (len1 < len2) str1 to str2 else str2 to str1
```

- data class genelde api modelleri için kullanılır. javanın boilerplate kodlarını otomatik yapar.
- companion object sayesinde metot ve değişkenlere class-level yani nesne oluşturmadan ulaşabiliriz

```kotlin
class MyClass {

	companion object {
		var x = 10
		fun method() {
			println("this is my method")
		}
	}
}

fun main() {

	println(MyClass.x)
	MyClass.method()

}
```

javada bunu static anahtar kelimesiyle yapiyoduk

```java
class MyClass {
    static int version = 1;

    static void method() {
        System.out.println("my method.");t
    }
}
```

- enum c’deki structure yapisidir

```kotlin
enum class Renkler {
	Beyaz, Siyah
}

val renk = Renkler.Beyaz
val renk2 = Renkler.Siyah
```

- kotlinde inheritance ile composition farkı nedir?

```kotlin
// composition bir sınıfın içine başka bir sınıfın objesini
// vererek onun metotlarını kullanabilme olayıdır
// inheritance'a göre daha esnektir

class ClassA(val b: ClassB) {} // artık classB metotlarını kullanır
class ClassA() : ClassB {} // B'den miras aldi
```

- kotlinde süper class `open` anahtar kelimesiyle tanımlanır

```kotlin
open class Araba {}
class Nissan : Araba() {}
```

- Dp kavramı, farklı ekranlarda aynı oranları yakalayabilmek için tasarlanmıştır. • Not : Ekran dokunuşlarında yeterli alanı sağlamak için önerilen parmak genişliği 50dp ‘ dir.
- Sp ise ölçekten bağımsız aynı kalır, mm gibi düşünebilirsin.
- navigation birden fazla aktivitede kullanılabilir ama her biri için ayrı navgraph oluşturman lazım
- eğer normal value yerine live value dersen bir değişkenin verisine .value metoduyla ulaşırsın
``` kotlin

// view model
class DenemeViewModel : ViewModel() {
	var sonuc = MutableLiveData("0")

	fun arttir() { sonuc.value += 10 }

}

// main activity

class MainActivity: AppCompatActivity() {

	onCreate() {

		viewModel.sonuc.observe(this) {
			var degisken = it
		}

	}

}
```

- `data class` ve `class` farkı:
  - data class genelde data modellemek için kullanılır
  ```kotlin
	data class User(val name: String) // gibi
  ```
  - data yazarsan başına `toString()`, `hashCode()`, `copy()`, `equals()` gibi bazı metotlar default gelir.
      - equals() bir sınıftan türetilen iki objenin eşit olup olmadığını kontrol ederken kullanılır.
	  ```kotlin
	data class User(val name: String)

	fun main() {
		val user1 = User("bugra")
		val user2 = User("bugra")
		println(user1.name)
		println(user2.name)

		println(user1 == user2) // true
		println(user1.equals(user2)) // true

		// ama eğer data class olmasaydı true verirdi
		// çünkü class'ın equals() metodu data class gibi
		// override edilmemiştir
		// değerleri/datayı değil bellek adresini karşılaştırır
	}
	```
	neden?
   - ayrıca data class içerisine en az 1 primary constructor vermek zorundasın
   ```kotlin
	data class myData() // X Hata verir
	data class myData(var name: String) // V okay
   ```
   - bununla beraber normal class çok daha özelleştirilebilir ve soyutlanabilirdir.
- hashCode() kotlin'de bir nesnenin sahip olduğu id'dir. unique olmayabilir. hashMap gibi çağrılarda nesnelerin aynı olup olmadığını kısaca hashcodelarını karşılaştırıp buluruz.
- google mvvm'i destekliyor. nedir mvvm?
  - model: API, veritabanı, Repository'ler
  - view: Aktiviteler, Fragmanlar, XML'ler vs.
  - viewmodel: Livedata, Stateflow vs. Model ve View katmanı arasındaki köprü.
  esas amacı, uygulamada kullanıcının gördüğü, etkileşime geçtiği UI katmanıyla arka planda çalışan business mantığını birbirinden ayırmaktır. böylelikle katmanlar arasındaki bağımlılıklar azalır, atomik bir yapıya dönüşür.
-
