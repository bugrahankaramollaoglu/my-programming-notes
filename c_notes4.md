# necati ergin c ders notları

**28aug22** 

## kaynak: necati ergin c ders notları pdf

### giriş

- yazılım programlamayla ilgili konuların geneline verilen isimdir. mevcut olarak bine yakın programlama dili vardır. bir dil high (insan diline yakın, anlaşılması kolay) ya da low (makine diline yakın, zor) olarak 2ye ayrılabilir. eskiden yalnızca makine dili (0ve1) vardı. Fakat makine dillerinin zorluğu şuydu: bir makine kodu yalnızca hangi bilgisayarda derlenmişse orada çalışabiliyordu. bunun için interpreted (yazılımcının yazdığı kodu kendi derleyicisinde makine koduna çevirip sonra onu çalıştıran) diller ortaya çıktı fakat bunlar yaklaşık 30 kat daha yavaştı. bu da şöyle bulundu: grace hopper isimli bir kadın bu dönüştürücü sistemlerin her seferinde kaynak kodu makine diline çevirmesindense bir kez çevirip sonrasında bilgisayarın o kodu tekrar tekrar kullanması fikrini öne attı, bu buluşuna compiler adı verildi. bunu da assembly ile yapıyorlardı. assembly'den de sonra geliştirilen diller (aka 3rdGen languages) FORTRAN (formula translator), COBOL (common business oriented language), ALGOL dilleri ortaya çıktı. sonra BASIC ortaya çıktı bu dile de OOP eklenerek Visual Basic çıktı (like C, CPP). daha sonra abd savunma sanayisinde kullanılan ADA yaratıldı. ada ismi lord byron'ın kızı Ada Lovelace'tan gelmektedir. Ada Lovelace ilk programcı olarak tarihe geçmiştir. Kendisi delikli kartları hesap makinelerinde kullanarak yazılımın tarihi temellerini atmıştır.
- programlama dillerinde kullanılan 2 temel standart
    1. ANSI
    2. ISO
- 5 types of programming languages
    1. procedural (yapısal) programlama
        - divide and conquer: tek ve bütün olarak yazılması zor programlar daha basit kolay kod bloglarının birleşimi halinde yazılırlar (functions).
        - data hiding: Yapısal programlama tekniğinde, programın diğer parçalarından ulaşılamayan, yalnızca belli bir bilinirlik alanı olan, yani kodun yalnızca belli bir kısmında kullanılacak değişkenler tanımlanabilir. Bu tür değişkenler genel olarak "yerel değişkenler" (local variables) olarak isimlendirilirler. Değişkenlerin bilinirlik alanlarının kısıtlanabilmesi hata yapma riskini azalttığı gibi, programların daha kolay değiştirilebilmesini, program parçalarının başka programlarda tekrar kullanabilmesini de sağlar.
        - single entry - single exit: Yapısal programlama tekniğini destekleyen dillerde her bir altprogram parçasına girmek için tek bir giriş ve tek bir çıkış mekanizması vardır. Bu araç programın yukarıdan aşağı olarak akışı ile uyum halindedir. Program parçalarına ancak tek bir noktadan girilebilir.
        - loops: döngü yapılarının kullanımı programı uzun ve yorucu hesaplamalarda verimli ve fisible hale getirir
    2. object-oriented programming (nesneye yönelik): procedural programlama 60larda, OOPlama ise 80lerde çıkmıştır. Alan Kay kurmuştur. ortaya çıkma sebebi artık programların gittikçe çok daha uzun satırda yazılmaya başlanmasıydı.Nesneye yönelmiş programlama tekniğinde, programa ilişkin veri ile bu veriyi işleyen kod, nesne isimli bir birim altında birleştirilir. Yani bu tekniğin yapı taşları nesnelerdir. Bu tekniğin prosedürel programlamada en önemli farkı, programcının programlama dilinin düzleminde değil de doğrudan problemin kendi düzleminde düşünmesi, programı kurgulamasıdır. Bu da gerçek hayata ilişkin bir problemin yazılımda çok daha iyi modellenmesini sağlar. C'ye OOP eklenmesiyle CPP, Pascal'a OOP eklenmesiyle Delphi, Cobol'a eklenmesiyle OOCobol, Ada'ya eklenmesiyle Ada95 çıkmıştır. bazı programlama teknikleri ise direkt OOP ile doğmuştur, bunlara pure OOP languages denir (C#, Eiffel, Java vs.).
    3. functional
    4. logic
    5. scripting
- C orta seviye bir dildir. Ne tam makine dili ne insan dilidir. Sistem programlama (donanım yazılımı yazma) için birebirdir. Çok esnek ve güçlü bir dildir.

### **# sayı sistemleri**

- Günlük hayatta onluk sayı sistemi kullanılır. Onluk sayı sisteminde bir sayının değeri aslında her bir basamak değerinin 10 sayısının üsleriyle çarpımlarından elde edilen toplam değeridir. Örneğin: 1273 = (3 * 1) + (7 * 10 ) + (2 * 100) + (1 * 1000)

Ancak bilgisayar sistemlerinde bütün bilgiler ikili sayı sisteminde (binary system) ifade edilir. Bir sayı sistemi kaçlıksa o sayı sisteminde o kadar simge bulunur. Örneğin onluk sayı sisteminde 10 adet simge vardır: 0, 1, 2, 3, 4, 5, 6, 7, 8 ve 9. bundan başka octal yani 8lik sayı sisteminde 0-7 arası 8 sembol bulunur. ya da 16lık (hexadecimal) sayı sisteminde 0-9 ve a-f olmak üzere 16 sembol bulunur. Aynı şekilde ikilik sayı sisteminde de yalnızca iki adet simge bulunur: 0 ve 1. 2lik sistemde her basamaga bir bit denir. Bit kelimesi 'binary digit'ten gelir. mesela 454, 10, -25 integerları 4bittir. 8bit, 1byte'a eşittir. 1024 adet byte ise 1kbyte'a eşittir.

`kilobyte, megabyte, gigabyte, terabyte, petabyte, exabyte, zettabyte, yottabyte`

- Tamsayı değerlerini göstermek için ikili sayı sistemi iki farklı biçimde kullanılabilir. Eğer yalnızca sıfır ve pozitif tamsayılar gösterilecekse, buna işaretsiz (unsigned) ikili sayı sistemi denir. eğer negatif tamsayıları da göstereceksek, işaretli (signed) ikili sayı sistemine ihtiyaç duyarız.
- 2li sistemden 10lu sisteme çeviri yapma: binary sayıyı en sağdan başlayarak 2'nin kuvvetleriyle teker teker çarparız. bu çarpımları toplarsak decimal karşılığını buluruz. mesela 1011 binary sayisinin decimal karşılığını bulalım. 
`(1 * 2^0) + (1 * 2^1) + (0 * 2^2) + (1 * 2^3) = 11`
    
    binary sayilar sağ taraftan ve 0. indisten başlarlar sayılmaya.
    
- 10luk sayı sisteminde 2lik sayı sistemine çeviri yapma: sayı sürekli olarak 2ye bölünür. her bölümden kalan değer (0 ya da 1) oluşturulacak sayıyı oluşturur. bu işlem sayı sıfırlanana kadar sürer. mesela 87 sayısını 2lik sisteme çevirelim.
87 / 2 = 43 (kalan 1) Sayının 0. biti 1     # 0101 0111
43 / 2 = 21 (kalan 1) Sayının 1. biti 1
21 / 2 = 10 (kalan 1) Sayının 2. biti 1
10 / 2 = 5 (kalan 0) Sayının 3. biti 0
5 / 2 = 2 (kalan 1) Sayının 4. biti 1
2 / 2 = 1 (kalan 0) Sayının 5. biti 0
1 / 2 = 0 (kalan 1) Sayının 6. biti 1
****87 = 0101 0111. bunun kodu

```c
int *binary_converter(int nb) {
	int i;
	int nb2 = nb;
	while (nb2) {
		i++;
		nb2 /= 2;
	}
	int *arr;
	arr = malloc(sizeof(int) * i);
	if (!arr)
		return 0;
	i = 0;
	while (nb) {
		arr[i] = nb % 2;
		i++;
		nb /= 2;
	}
	return arr;
}

int main() {
	int *ar;
	ar = malloc(100);
	ar = binary_converter(87);
	for (int i = 0; i < 10; i++) {
		printf("[%d]", ar[i]);
	}
}
```

İkinci bir yöntem ise, onluk sayı sisteminde ifade edilen sayıdan sürekli olarak ikinin çıkarılabilir en büyük üssünü çıkarmaktır. Çıkarılabilen her bir üs için ilgili basamağa 1 değeri yazılır. kalanlar için 0 yazılır. Bu işlem 0 sayısı elde edilene kadar sürdürülür. Yine 87 sayısı ikilik sayı sisteminde ifade edilmek istensin:

87 - 64 = 23 —> 0100 0000

23 - 16 = 7 —> 0101 0000

7 - 4 = 3 —> 0101 0100

3 - 2 = 1 —> 0101 0110

1 - 1 = 0 —> 0101 0111

87 = 0101 0111

- binary sayılarda one's complement (bire tümleyen) denilen kavram vardır. o da sayıdaki 0ların 1, 1lerin 0 yapılmasıyla elde edilir. bunun bitwise operatör karşılığı **`~`**'dir. bire tümleyeni alınan bir sayıya 1 eklenmesiyle 2ye tümleyeni elde edilir. mesela sayı 1010 1000 olsun. bunun 1e tümleyeni 0101 0111'dir. 2ye tümleyenini bulmak için sayıya +1 eklenirse sayı 0101 1000 olur (binary sistemde 1+1 = 2 olamayacağı için solundaki sayıyı 0sa 1 yapar o da 1se bir soldakine diye gider).
- 8 bitlik bir sayının alabileceği maksimum değer her basamağın 1 olduğu durumdur (1111 111). minimum hali de 0 olma durumu yani 0000 0000. o yüzden 8bitlik bir alana yazılabilecek en büyük sayı işaretsiz ikili sayı sisteminde hepsinin 1 olduğu durum. onun da decimal karşılığı 255'tir. yani işaretsiz 2li sayı sisteminin aralığı 0-255'tir. 255'in binary karşılığı 1111 1111'dir. 256 dersen bu sefer başa sarar ve 0000 0000'dan başlar.
- negatif sayıları binary'de göstermek için 'signed binary system' kullanılır. sayının en solundaki bit işaret bitidir (sign bit). 1 ise sayı negatif, 0 ise pozitiftir. ikilik sistemde bir negatif sayı, sayının pozitif halinin 2ye tümleyenidir.
- mesela 1001 1101 sayısının işaretli sistemde hangi sayıya denk geldiğini bulalım. önce en soldaki işaret bitine bakıyoruz, 1. yani sayı negatif. daha sonra sayının 2ye tümleyenini alıyoruz, o da bize 0110 0011 veriyor. o da 99'a eşit. yani sayımız -99'dur. şimdi de -17 sayısını signed system'e çevirelim. önce 17'yi çeviriyoruz --> 0001 0001. sonra 2ye tümleyenini alıyoruz ve cevap 1110 1110. yani işaretli ikili sayı sisteminde, 0-1'lerden 10'luk tabana çevirmek için
    - önce işaret bitine bakıyoruz
    - sonra sayının 2ye tümleyenini alıyoruz (bire tümleyeni + 1 ekleyerek)
    - sonra işareti neyse onu ekleyip sonucu buluyoruz
    
    10'luk tabandan 0-1'e çevirmek içinse
    
    - sayı negatifse önce pozitife çeviriyoruz
    - sonra 2'nin üslerini toplama metoduyla 0-1'e çeviriyoruz
    - sonra 2'ye tümleyenini alıyoruz
- işaretli ikili sayı sisteminde min, max nedir? önce maksimuma bakalım. normalde (unsigned) maksimum sayı bütün 8 bitin de 1 olduğu (1111 1111) sayısıydı, bu da 255'e denk geliyordu. fakat aynı şeyi signed binary sistemde yazarsan baştaki bir sayıyı negatif yapar. o yüzden baştaki bit 0 kalanı 1 yapıyoruz ve bu sistemde max sayı 127 oluyor. Peki ya en küçük negatif sayı kaçtır, nasıl ifade edilir? 0111 1111 sayısının ikiye tümleyenini alındığında –127 sayısı elde edilir. 1000 0001 (-127). Bu sayıdan hala 1 çıkartılabilir: 1000 0000 (-128). 1000 0000, 1 byte alana yazılabilecek en küçük negatif sayıdır. 1 byte alana yazılabilecek en büyük sayı sınırı aşıldığında negatif bölgeye geçilir. En büyük pozitif tamsayıya 1 toplandığını düşünelim: 0111 1111 (en büyük pozitif tamsayı = 127) + 1. yani işaretli binary sisteminde en küçük sayı 1000 0000 (en küçük tamsayı = -128)
- yani işaretli ikilik sistemde n byte alana yazılabilecek en büyük tamsayıya 1 eklendiğinde n byte alana yazılabilecek en küçük tamsayı elde edilir. aynı şekilde n byte alana yazılabilecek en küçük tamsayıdan 1 çıkarıldığında da n byte alana yazılabilecek en büyük tamsayı elde edilir.
- Onaltılık sayı sisteminde yazılmış bir sayıyı onluk sistemde ifade etmek için, en sağdan başlanarak basamak değerleri onaltının artan üsleriyle çarpılır:
01AF = (15 * 1) + (10 * 16) + (1 * 256) + (0 * 4096) = 431
- Onluk sayı sisteminde yazılmış bir sayıyı, onaltılık sayı sisteminde ifade etmek için onluk sayı sisteminden ikilik sayı sistemine yapılan dönüşüme benzer yöntem kullanılabilir. Sayı sürekli 16'ya bölünerek, kalanlar soldan sağa doğru yazılır.  Onaltılık sayı sisteminde yazılmış işaretli bir sayının pozitif mi negatif mi olduğunu anlamak için sayının en soldaki basamağına bakmak yeterlidir. Bu basamak [8 - F] aralığında ise sayı negatiftir.
- **C dilinde bir program nasıl çalışır?**
    - .c uzantılı bir metin dosyasında kod yazılır
    - normalde bir kodu bir programlama dilinden bir başkasına çeviren şeylere translator denir. fakat eğer hedef dil (çevrilecek dil) makine dili yani binary ise artık compiler yani derleyici adını alır. C'de compiler yukarıda yazılan kaynak kodu alıp windows'ta .obj uzantılı object dosyasına çevirir (linux/unix'te .o). bu derleme sürecinde (compile time) 3 şey olabilir
        - hata mesajı
        - uyarı mesajı
        - başarı (all is well)
    
    bu derleyici programlar aslında .exe uzantılı (gcc.exe ya da cl.exe) programlardır ve yukarıda anlatılan tekniklerle harf ve sayıları 1 ve 0'lara çevirir.
    
- daha sonra bu .o uzantılı dosya bağlayıcı (linker) aracılığıyla çalıştırılabilir bir dosya haline getirilir (windows'ta .exe, unix'te uzantısız).
- ve çalıştırılır. C/CPP'ta kodlar derleyici programdan evvel preprocessor isimli bir programa sokulur.

### veri türleri

- C'nin kendi veri tipleri 11 adettir. 4 tane tamsayı veri tipi vardır (fakat aslında bunların da signed/unsigned halleri olduğundan 8 adet kabul edilir).
    - signed/unsigned char: short for character. her zaman 1 byte yer kaplar ve aralığı -128/127'dir. bunun sebebi 1 byte'ın (8 tane 0'ın) hesaplamasından gelir (discussed in detail above). işaretsiz char'ın işaretli char'dan farkı şudur: 1byte işaretsizde yalnızca 0 ve pozitif sayılar için kullanılabilir. bu durumda 0-255 arasında değer tutar. char veri tipi işaretli mi işaretsiz mi sayılacak buna derleyici karar verir
    - signed/unsigned short: kapladığı yer mimariden mimariye değişir (genelde 2byte). işaretli short'un aralığı -32768 ve +32767'dir. işaretsiz short ise 0 - 65535'tir.
    - signed/unsigned int: 16bitlik sistemlerde genelde 2, 32bit sistemlerde 4byte yer kaplar. aralığı -2147483648/+2147483647'dir. işaretsiz aralığı ise 0 - 4294967295'dir.
    - signed/unsigned long: 4byte kaplar. aralığı daha geniştir inte göre.
    - float: hemen her zaman 4byte'tır.
    - double: 8byte yer kaplar.
- örnek

```c
int a, b, c;   // doğru
int a, long b; // yanlış
```

- bir tamsayının sonuna
    - u ya da U gelmesi unsigned oldugunu, (20u)
    - L gelmesi long oldugunu (353943L)
    - f ya da F gelmesi float oldugunu (1.31F) gösterir
- char constants, tek tırnak icinde yazılan karakterlerdir mesela 's', '&', ' ' gibi. bunlar aslında integer sayı türünün char veri tipinde yazılmış halinden başka bir şey değildir. mesela 'a' 97 int'ine denk gelir çünkü ascii tablosunda a 97 numaradır.

```c
char c = 'a' + 5; // doğru (97 + 5)
```

- \ is called escape sequence. bu ifadeler \ + harf'ten oluşsa da tek bir char (1 byte) kabul edilir

```c
write(1, "a\n", 1);
```

### fonksiyonlar

- C'de fonksiyonların genel şeması şöyledir:

```c
return_type function_name(parameter_type parameter_name) {
	// code blocks
	// thing to return
}
```

eğer bir şey döndürmek zorunda değilse şöyle yazılır: 

```c
void myFun(int nb) {}
```

yahut parametre almak zorunda değilse 

```c
void myFun(){
	if (a == 3)
		return ; // void fonksiyondan çıkmak istediğinde return ; demelisin
}
```

şöyle bi ayrıntı var, yukarıdaki fonksiyona parametre verirsen işlemez fakat hata da vermez, hata versin istiyosan içine void yazmalısın 

```c
void myFun(void) {}
```

ayrıca

```c
fun() {}
```

- fonksiyonlar iç içe yazılamaz fakat birbirleri içinde yalnızca çağrılabilirler
- main() fonksiyonu bütün c kodlarında olması zorunlu tek fonksiyondur. main'in return 0 ile dönmesi sorunsuz çalıştığını gösterir.
- C'de 2 tip yorum satırı vardır
    - **// asdasd**
    - **/* asdasd**
- there are 3 sorts of operators in C:
    - unary operators: ++ ve --
    - binary operators: +, - , *, / vs.
    - ternary operator aka conditional operator.
    
    ```c
    return (a == 3 ? 1 : 0);
    ```
    
    eğer a 3’e eşitse 1 değilse 0 döndürür
    
- difference between post/prefix: Normalde --c; ve c--; deyimleri tamamen birbirine denk olup c = c - 1; anlamına gelir. fakat bir ifade içinde diğer işleçlerle birlikte kullanıldıklarında, prefix ve postfix biçimleri arasında farklılık vardır: prefix (++x) durumunda kullanıldığında, işlecin ürettiği değer, artırma ya da eksiltme yapıldıktan sonraki değerdir. Yani terimin artırılmış ya da azaltılmış değeridir. postfix (x++) durumunda ise işlecin ürettiği değer, artırma ya da eksiltme yapılmadan önceki değerdir. Yani terimi olan nesnenin artırılmamış ya da azaltılmamış değeridir. fakat gene de nesnenin değeri ifadenin tümü değerlendirildikten sonra mutlaka artırılır ya da eksiltilir. mesela

```c
int x = 10;
int y = ++x; // bu durumda x ve y 11 olur

int a = 10;
int b = a++; // bu durumda a 11 b 10 olur çünkü arttırmadan önce atadı b'ye
```

### scope

- C'de değişkenler, fonksiyonlar vs. yalnızca scope'ları yani bilinirlik alanları içerisinde tanınırlar. scope türleri
    - file scope (dosya bilinirlik alanı): bir nesne tanımlandıktan sonra tüm dosya (asd.c) içinde bilinir olmasıdır
    - block scope (blok bilinirlik alanı): yalnızca bir blok içinde bilinir olması
    - function scope (fonksiyon bilinirlik alanı): Bir ismin, bildirildikten sonra yalnızca bir blok içinde bilinmesidir. Yalnızca goto etiketlerini kapsayan özel bir tanımdır.
    - function prototype scope: fonksiyon parametrelerinin bilinirlik alanı
- bir değişken tanımlandığı scope’a göre lokal ya da global olabilir:

```c
int a = 20; // this is global and can be used everywhere
int fun() {
	int b = 30; // this is local and can only be used within this scope
}
```

scope'ları farklı oldukları müddetce aynı isimde degiskenler tanımlayabilirsin

- nesnelerin ömürleri (storage duration): nesnelerin programın çalışma zamanı içinde hafızada yer tuttukları süreye denir (ne zaman yer ayrıldı - ne zaman otomatik ya da manuel freelendi). ömürleri bakımından nesneler 3e ayrılır
    - static duration: program başlayınca bellekte bunlara yer ayrılır, program bitene kadar da bellekte yer kaplarlar.
    - otomatik duration: programın belli bir evresinde yaratılıp belli bir süre çalıştıktan sonra yok olan nesnelerdir.
    - dynamic duration
- Bilgisayarların aritmetik bir işlemi gerçekleştirmesi için genellikle işleme sokulan terimlerin uzunluklarının aynı olması, yani bit sayılarının aynı olması ve bellekte aynı formatta ifade edilmeleri gerekir. Örneğin işlemci 16 bit uzunluğunda iki tam sayıyı doğrudan toplayabilir ama 16 bit uzunluğunda bir tam sayı ile 32 bit uzunluğundaki bir gerçek sayıyı doğrudan toplayamazsınız. C otomatik olarak basit tür dönüşümleri yapabilir. 2 tür tür dönüşümü vardır:
    - explicit type conversion (açık): değişkenin başına parantez içinde veri tipi yazilir
    
    ```c
    int a = 5;
    float b = 4.2;
    (float)a + b >> 9.2
    ```
    
    - implicit type conversion (gizli): C'nin otomatik yaptıgı degisimlerdir. mesela
    
    ```c
    char x = 'y';
    int a = 10;
    a + x >>> 89
    ```
    

### loops

- C'de 3 tür loop vardır
    - for
    - while
    - do ****while
- while (n) demek while (n>0) demektir

```c
int a = 3;
while (a--)
	// this works 3 times
while (--a)
	// this works 2 times
```

- do ile do-while arasındaki fark şudur: while'da eğer şart sağlanmıyorsa kod blogu calısmaz fakat do-while koşul saglamasını sonda yaptıgı icin en az bir kere calıstırılır

```c
int main() {
	int val;
	do {
		printf("enter a val: 0-10");
		scanf("%d", &val);
	} while (val > 0 && val < 10);
	printf("val:%d\n", val);
}
```

- for döngüsünün temel şeması şöyledir:

```c
for (int i = 0; i < 10; i++) {
	printf("%d ", i);
}
```

bilerek sonsuz döngü olusturulmak istendiginde for(;;) kalıbı kullanılır (while(1) gibi)

- bir döngüden ne zaman çıkılır?
    - kontrol ifadesi yanlışa düştüğü zaman
    - return -> return dediğin zaman direkt bütün .c dosyasını sonlandırır
    - break --> break dediğin zaman sadece o döngüden çıkar döngü devamında kod varsa oradan devam eder işlemeye
    - goto
    - exit(), abort() vs.
- ternary örnekleri

```c
p = (x==5) ? 10:4;
return x > y ? x : y;
myFun(a==b ? 4 : 7);
```

- C derleyicileri 2 modülden oluşur:
    - önişlemci modülü: önişlemciler (preprocessor), işlemci ya da donanımla alakalı olmayıp tamamen birer yazılımdırlar. # ile başlayan satırları ele alırlar. mesela #include, #define, #ifndef, #if, #else, #elif etc.
    - derleme modülü
    C bir kodu derlerken önce yazılan kod preprocessor modülüne girer, o bu modülü alıp compiler modülüne verir o da compile eder.

#include komutu 3 farklı şekilde yazılabilir

- `#include <stdio.h>`
- `#include "stdio.h"`
- `#include "C:\myC\headers\libft.h"`

genelde programcının yazdıgı kutuphaneler " " içinde, standart kutuphaneler < > icindedir.

- symbolic constant'lar tanımlarken şöyle tanımlarız:

```c
#define SIZE 10
#define PI 3.14
int arr[SIZE];
cevre = 2*PI*r;
```

- random mantığının kullanımı: C'de bazen rastgele sayı üretmek isteyebiliriz. o zaman rand() fonksiyonunu kullanırız. bunun için stdlib.h import edilmelidir. her çağrıldığında rand[0, INT_MAX] aralığında bir int döndürür. genelde bu max 2147483647'dir. örnek:

```c
int main() {
	for (int i = 0; i < 10; i++) {
		printf("[%d]", rand());
}
```

peki neden her çalıştırıldığında aynı random sayılar geliyor? bunun sebebi rand() fonksiyonunun random sayı üretme mekanizmasıdır. C, random sayı üretirken evvela bir seed value, yani ilk değer belirler, sonra onu karmaşık işlemlere tabi tutarak yeni random sayılar üretir. rand() fonksiyonunda bu değer sabit, işlemler de aynı oldugu icin sürekli aynı sayı zinciri gelip durur. srand() ise bu seedValue'yu değiştirdiği için sürekli yeni random sayılar gelir. 

```c
int main() {
	srand(35);
	for (int i = 0; i < 10; i++) 
		printf("[%d]", rand());
}
```

srand() değiştikçe random sayılar da değişir. fakat bir sorun var, bu sefer de srand()'ı degismedigimiz müddetce gene aynı random sayılar geliyor. bunun onune gecmek icin time.h kütüphanesini kullanacagız. time() fonksiyonu kendisine 0 tarihi gönderildiğinde önceden belirlenmiş tarihten (genelde 1ocak1970) fonksiyonun cagrıldıgı tarihe kadar gecen saniyeyi hesaplar ve döndürür. bu döndürülen sayı srand()'a argüman olarak gider ve her çağrıldığında belli bir zaman geçmiş olacağı için srand()'a farklı değer gider, dolayısıyla rand() da farklı bir random sayı oluşturur. 

```c
int main() {
	int t;
	srand(time(0));
	for (int i = 0; i < 10; i++) 
		printf("[%d]", rand());
}
```

### array

- hafızada veri tutma, saklama ve işleme tekniklerine veri yapıları denir. hafızada sıralı bir biçimde saklanan, aynı veri tipindeki nesneler dizisine array denir.

```c
int arr[5];        // birinci yol
int *arr;          // ikinci yol
int arr[] = {...}; // üçüncü yol
```

burada elemanlarının her biri integer olan, 5 elemanlı bir array tanımladık. bu arrayin elemanları 0. indisten basladıgı icin son elemanının indisi 4'tür.

- arraye eleman sayısı atarken bazı kurallar vardır:

```c
#define SIZE 25;

int arr[SIZE]; // geçerli  +
int arr[3*5];  // geçerli  +

int a = 20;
int arr[a];    // geçersiz X
int arr[0];    // geçersiz X
int arr[-5];   // geçersiz X
```

- arraylerde**`[]`** ifadesi bir pointer operatörüdür, içine yazılan şeyin adresine tekabul eder.
- bir arraye ayrılması gereken minimum yer (sizeof(verinin_türü) * veri_adedi)'dir. eğer statik değil pointer tanımlarsan sonrasında yer ayırman gerekir:

```c
int arr[] = {10, 20, 30}; // eğer []'i boş bırakacaksan ilklendirmelisin
int arr[3]; // bırakmayacaksan doldurmana gerek yok
int *arr = malloc(sizeof(int) * 3); // ptr array kullanacaksan yer ayır
```

- \x0 (aka \0 or NULL) karakteri 0 ile karıştırılmamalıdır. 0'ın ascii değeri 48ken bunun 0'dır.
- ilklendirme yaparken " " içinde string de tanımlayabilirsin:

```c
char arr[] = "bugrahan";
```

- null da diğer karakterler gibi 1 byte yer kaplar. o yüzden bugra stringi 5 değil 6 byte uzunlugundadır.
- puts() standart bir C fonksiyonudur. ekrana char str yazdırmak icin kullanılır. printf()'ten farkı sonuna otomatik olarak \n koyar. putchar()'ın döngü hali gibidir.
- bir arrayin eleman sayısını bulmanın en kolay yolu: **`sizeof(arr) / sizeof(arr[0])`** metodudur. eleman sayısını hesaplamak içn byte'lardan yararlanır. dizinin kapladığı tüm byte sayısı / bir elemanın kapladıgı byte sayisi gibi.
- çok boyutlu arrayler: int a[10][3] dizisi iki boyutlu int türünden bir dizi (array)dir. 2 boyutlu arrayler matris olarak da bilinir. yukarıdaki a arrayi aslında her bir elemanı 3 elemanlı bir array olan 10 elemanlı bir arraydir. toplam boyutu sizeof(int)*30'dur. mesela bu arrayin 6. elemanının 2. elemanına ulasmak icin array[5][1] demelisin. bir eksik olma sebebi arraylerin 1 değil 0. elemandan başlamalarıdır. o yüzden bir arrayin son elemanı her zaman (eleman_sayisi - 1). elemanıdır.
- how to random-fill a 2-D array?

```c
#define ROW 3
#define COLUMN 5

int main() {
	int ar[ROW][COLUMN];
	int i, i2;
	srand(time(0));
	for (i = 0; i< ROW; i++) {
		for (i2 = 0; i2 < COLUMN; i2++) {
			ar[i][i2] = rand() % 100;
		}
	}
	for (i = 0; i < ROW; i++) {
		for (i2 = 0; i2 < COLUMN; i2++) 
			printf("[%2d]", ar[i][i2]);
		printf("\n");
	}
}
```

- **m**esela arr[2][3] oldugunu farz edelim. bu dizinin ilk elemanı arr[0] olacaktır. bu arr[0] bilindigi gibi 3 elemandan oluşan bir baska dizidir. peki bu arr[0]'ın adresinin yani &arr[0]’ın tuttuğu değer hangi türe karşılık geliyor olabilir? int * ya da int ** değil. bu ifadenin türü
int (*)[3]'tür.
- char matrisleri de tanımlanabilir

```c
char words2D[10][30];
```

### dynamic memory allocation

- programlar RAM'de yer tutarlar. RAM'de bunlara yer ayırma süreci 2 şekilde olabilir
    - derleme zamanında
    - calısma zamanında (aka dynamic memory management)
    
    int a[100] dediğin zaman derleme zamanında 400byte'lık yer ayrılır ve sonrasında eksiltilip azaltılamaz. eğer bu array local ise otomatik ömürlüdür yani içinde tanımlandığı kod blogu bitince bu arrayin yeri de hafızada serbest bırakılır.
    
- en ünlü dinamik memory fonksiyonu malloc()'tur:

```c
int *arr = (int *)malloc(sizeof(int)*10); // baştaki malloc'un sol tarafı olmasa da olur
char *str = malloc(sizeof(char) * 100);
```

malloc'un return değeri void oldugu icin her tipten veride kullanılabilir. malloc her kullanıldıktan sonra kontrol edilmelidir. eğer başarısız olup null dönmüşse biz de null döndürmeliyiz: 

```c
char *str = malloc(10);
if (!str)
	return 0; 

// ya da 

if(!(char *str = malloc(10))
	return 0;
```

- malloc işlevinin geri dönüş değeri void pointer oldugu icin bu adres sorunsuzca herhangi bir türden bir gösterici değişkene atanabilir. Ancak okunabilirlik açısından malloc işlevinin geri dönüş değeri olan adresin, tür dönüştürme işleci yardımıyla, kullanılacak gösterici değişkenin türüne dönüştürülmesi önerilir. Böylece malloc işlevi ile elde edilen bloğun hangi türden nesne ya da nesnelermiş gibi kullanılacağı bilgisi kodu okuyana verilmiş olur. yani

```c
char *str;
str = malloc(strlen(str)); // de diyebilirsin ama for readability
str = (char *)malloc(sizeof(char) * strlen(str)); // denmelidir
```

- malloc kullanınca hafızadaki adres blogu çöp değerlerle doldurulur.
- malloc birden çok çağrılarak birden fazla dinamik hafıza alanı elde edilebilir fakat bunların contiguous olmaları garanti değildir. ayrıca çok fazla malloc() kullanımı heap'i şişireceği için stackoverflowa sebep olabilir.
- ideal olarak her malloc( ) kullanımın sonrası free( ) ile ayırdığın yeri ram’e geri vermelisin. eğer vermezsen ve program ver-e-meden biterse leak dediğimiz şey oluşur

```c
void fun() {
	char *str = malloc(1000);
	if (!str)
		return 0;
}
```

leaklere bakmak için valgrind kullanabilirsin 

```c
gcc main.c
valgrind ./a.out
```

- calloc() malloc()'la aynı işi yapar fakat ayırdığı yeri garbage value yani random şeylerle değil NULL'larla doldurur.
- global ya da static tanımlamadığın bütün **`int`** değerlere garbage-value atanır. bu ikisine ise 0 atanır

```c
int a; // a == 0

int main() {
	static int b; // b == 0
	int c; // c == allah_bilir_ne
```

### constants

- Belirleyiciler (storage class specifiers), bildirimler yapılırken kullanılan ve nesnelerin özellikleri hakkında derleyicilere bilgi veren anahtar sözcüklerdir.
    - auto: nesnenin otomatik ömürlü oldugunu, yerelde tanımlandıgını vurgulamak icin kullanı/labilen bir keyworddür. neredeyse hiç kullanılmaz.
    - register: değişkenin "bellekte değil de CPU yazmaçlarının içinde" tutulması isteğini derleyiciye ileten bir anahtar sözcüktür. Değişkenlerin bellek yerine doğrudan yazmaçlarda tutulması programın çalışmasını hızlandırır. Yazmaç (register) nedir? Yazmaçlar CPU (central processing unit) içinde bulunan tampon bellek bölgeleridir.
    - static: static belirleyicisi ancak yerel ya da global değişkenlerin bildiriminde kullanılabilir. Bu belirleyici, parametre değişkenlerinin bildiriminde kullanılamaz. static anahtar sözcüğünün global ve yerel değişkenlerin bildiriminde kullanılması farklı anlamlara gelir.
        - static kelimesinin yerel değişkenlerle kullanımı: static anahtar sözcügüyle beraber kullanılan yerel degiskenler program süresi boyunca bellekte tutulur. normalde yani staticsiz icerinde tanımlandıkları kod blogu boyunca tutuluyordu:
        
        ```c
        void fun() {
        	int x = 5;
        	printf("x = %d\n", x);
        	x++;
        }
        void fun2() {
        	static int y = 5;
        	printf("y = %d\n", y);
        }
        int main() {
        		for (int k = 0; k < 5; ++k)
        			fun1(); // 5 5 5 5 5 verir
        		for (int l = 0; l < 5; ++l)
        			fun2(); // 5 6 7 8 9 verir
        ```
        
        - global kullanımı: Statik yerel değişkenler ömür açısından global değişkenler ile aynı özellikleri gösterirler. Yani programın çalışmaya başlaması ile yaratılırlar ve programın çalışması bitince ömürleri sona erer. Ama bilinirlik alanı (scope) açısından farklılık gösterirler. Global değişkenler dosya bilinirlik alanına uyarken statik yerel değişkenler blok bilinirlik alanına uyar. Statik yerel değişkenlerin blok bilinirlik alanına sahip olması verilerin gizlenmesini (data hiding) kolaylaştırır ve kodun yeniden kullanılabilirliğini (reusability) artırır. Çünkü global değişkenlere bağlı olan işlevler bir projeden bir başka projeye kolayca taşınamazlar.
    - extern
    - typedef
    - tür niteleyicileri
        - volatile
        - const: atandıktan sonra nesnenin içeriğinin modifiye edilemeyeceğini gösterir. yani atama, değiştirme vs. yapılamaz:
        
        ```c
        const int a = 10;
        a++; // geçersiz
        ```
        
        local bir değişkeni **`const`** tanımladıysan muhakkak ilklendirmelisin (yarattıktan sonra değer vermelisin) yoksa garbage value değiştirilemez.
        
- constlar pointerlarla 3 farklı şekilde kullanılabilirler
    1. **`pointer-to-constant`**: böyle bir pointerın gösterdiği nesne modifiye edilemez fakat pointerın kendisi bir başka nesneyi gösterecek şekilde değiştirilebilir. 
    
    ```c
    int main() {
    	char str[] = "bugra";
    	char str2[] = "cemre";
    	const char *strPtr = str;
    	// const oldugu icin degistiremezsin
    	*strPtr = 'B'; // ya da
    	strPtr[2] = 's';
    	// ama başka stringi gösterecek şekilde pointerı değiştirebilirsin
    	strPtr = str2;
    }
    ```
    
    1. **`constant-pointer`**: bu pointerlar ilklendirilirken nesneleri adres atama yoluyla değiştirilemezler. yani pointer hep aynı nesneyi gösterir. fakat gösterdiği nesneyi modifiye etmek mümkündür 
    
    ```c
    int	main(void)
    {
    	char str[] = "bugra";
    	char str2[] = "cemre";
    	char *const strPtr = str;
    	// str'yi değiştirebilirsin
    	strPtr[0] = 'B'; // ya da 
    	*strPtr = 'B';
    	// ama başka stringi göstertemezsin
    	strPtr = str2;
    }
    ```
    
    1. **`constant-pointer-to-constant`**: the data pointed to by the pointer is constant and cannot be changed. The pointer itself is constant and cannot change and point somewhere else. 
    
    ```c
    int main() {
    	char str[] = "bugra";
    	const char *const strPtr = str;
    }
    ```
    

### pointers

- C'de garbage collector olmadıgı için hafızalarla işlem yaparken pointers kullanıyoruz. bu temel anlamıyla su demektir: bilgisayar, biz kod yazarken tanımladıgımız degiskenleri, fonksiyonları vs. tekrar kullanabilmek icin bunları Random Access Memory yani RAM'de tutuyor. bu hafıza alanı geçicidir, HDD/SSD'ler gibi değildir. bilgisayar her kapatıp açıldığında bütün verileri gider, tekrar tanımlanır, tekrar kullanılır. bir `char c = 's'` degiskeni tanımladıgımızı farz edelim. bu char değişkeninin 's' değerine sahip oldugunu hatırlamak icin bilgisayar bu ilişkilendirme bilgisini RAM'deki hücrelerde saklar. bu hücrelerin her birinin bir adresi vardır. bu adresler hexadecimal, yani 1A00... gibi sayılardan oluşur (harf + sayi).

![](necati%20ergin%20c%20ders%20notlar%C4%B1%200662c25412974b26a3c99cb963fe8fc8/image2.png)

yukarıda ram'in 1A02 numaralı hücresinde (her hücre genelde 1 byte) ch degiskeninin depolandıgını görüyoruz. yani ch değişkeninin değeri 's', adresi ise adresi alınan değişkenin türünden bir sayı olan 1A02'dir. eğer bir adres hücresine sığan bir char değil de en az 2 hücre isteyen bir int tanımlasaydik o zaman hangi hücrenin adresi değişkenin adresi olacaktı? cevap, ilk hücrenin adresi.

![](necati%20ergin%20c%20ders%20notlar%C4%B1%200662c25412974b26a3c99cb963fe8fc8/image9.png)

bu değişkenin adresi 1C02'dir.

- yani bir pointer, bir nesnenin hafızada tutuldugu hücrenin adresini tutan bir baska degiskendir ama özel olarak sadece o adresi tutar. xx pointerı yy değişkenini gösteriyor dediğimizde bunu kastederiz. mesela

```c
int a = 10; // bu bizim normal degiskenimiz
int *aPtr = &a; // bu da a'ya atadığımız pointer
printf("%d", *aPtr); >>> 10
printf("%p", aPtr);  >>> 0x123594f
```

- bir adres'in türünün o adresin tuttugu degiskenin türünden geldiğini söylemistik (known as derived type). bu tür eger degisken int ise (int *) seklinde, char ise (char *) seklinde gösterilir. yani x T türünden bir değişken ise x'in pointerının türü yani veri tipi (T *)'dir.
- pointerların 3 tane operatorü vardır
    - **`*`** (dereferencing operator): iki görevi vardır [1] değişkenin pointer oldugunu belirtmek [2] tanımlanmış bir pointerın tuttuğu değere ulaşmak
    
    ```c
    int a = 10;
    int *aPtr = &a;     // birinci görev
    print(*aPtr) >>> 10 // ikinci görev
    ```
    
    - **`&`** (adres of operator): başına geldiği değişkenin adresini alır
    
    ```c
    int a = 10;
    printf("%p", &a); >>> 0x7fffe342
    ```
    
    - **`[n]`** (subscript operator): pointerın n kadar ötelenmiş halindeki değerini verir
    
    ```c
    int	main(void)
    {
    	int ar[] = {10, 20, 30};
    	int *arPtr = ar;
    	printf("%d\n", arPtr[2]); >>> 30
    }
    ```
    
- bir pointera adres harici bir şey atmak hatadır. mesela

```c
int i = 123456;
int *ptr = i;
```

dersen burada iPtr'ye i'nin adresini değil (as we normally ought to do), ram'de, 124352 adresinde bir değer varsa onu atamış oluyoruz. 

- printf() ile bir pointer adresi yazdırılmak istendiginde %p conversion specifier'ı kullanılır

```c
int a = 10;
int *aPtr = &a;
printf("a'nin adresi: %p\n", aPtr);
```

- call by value/reference farkı

```c
// call by value
int fun(a);
fun(nb);

// call by reference
int fun(*a);
fun(&nb);
```

- pointer arithmetic: C'de pointerlar yani adres değerleri sayılarla toplanıp çıkartılabilir. buna pointer aritmetiği denir ve sonucunda yine bir adres elde edilir. bir adrese mesela 1 eklendiğinde, adresin adresin sayısal değeri, adresin nesnesinin türünün uzunlugu kadar artar. mesela bir char adresi 1 arttırıldığında adres +1, int 1 arttırıldığında adres +4 artar. bir adres her arttırıldığında artık yeni, incremented adres eski değerden bir sonraki nesneyi gösterir hale gelir:
    - x = p[i]++ örneğinde x'e p[i]'in arttırılmamış (++ eklenmemiş) değeri atanır çünkü postincrement kullanılmıştır. atandıktan sorna p[i] değeri 1 arttırılır.
    - x = ++p[i] örneğinde ise önce [] ele alınır sonra ++. önce p'nin i. indisindeki değer 1 arttırılır. sonra bu arttırılmış değer x'e atılır.
    - x = p[++i] örneğinde p'nin (i+1). indisindeki değer x'e atanır
    - x = p[i++] örneğinde önce i++'nın değeri bulunur, bu ifade i'nin kendi değeridir (çünkü postfix). daha sonra x'e p'nin i. indisteki değeri atanır. daha sonra i 1 arttırılır.
- **`[n]`** ifadesi bir arrayin n ötedeki elemanına erişmek için kullanılır. p[n] ifadesi ile *(p+n) tamamen aynı anlama gelir. çünkü bir arrayin ismi kullanıldıgında C bunu o arrayin ilk elemanının adresi olarak görür. o yüzden C’de, garip ama, arr[5] ile 5[arr] aynı anlama gelir:

```c
char *str = "bugra";
printf("%c\n", 3[str]); // 3
```

- bir pointer fonksiyonlara parametre olabilir. bu durumda iki şekilde yazılabilir
    - void myFun(int *myPtr);
    - void myFun(int myPtr[ ]);
    yani bu fonksiyonlar parametre olarak int array alıyorlarmış

örnek2:

- aşağıdaki fonksiyon bir adres döndürür. bu bir int arrayinin adresidir: /codi

```c
int *reverse_int_tab(int *arr);
int arr[] = {10, 20, 30};
reverse_int_tab(arr);
```

- Nesnelerin Bellekteki Yerleşimleri: Bir byte'tan daha büyük olan değişkenlerin belleğe yerleşim biçimi kullanılan mikroişlemciye göre değişebilir. Bu nedenle değişkenlerin bellekteki görünümleri taşınabilir bir bilgi değildir. Mikroişlemciler iki tür yerleşim biçimi kullanabilir:
    1. Düşük anlamlı byte değerleri belleğin düşük sayılı adresinde bulunacak biçimde. Böyle yerleşim biçimine little endian denir. Intel işlemcileri bu yerleşim biçimini kullanır. Bu işlemcilerin kullanıldığı sistemlerde örneğin `int x = 0x1234;` biçimindeki bir x değişkeni bellekte 1A00 adresinden başlayarak yerleştirilmiş olsun:

![](necati%20ergin%20c%20ders%20notlar%C4%B1%200662c25412974b26a3c99cb963fe8fc8/image5.png)

Şekilden de görüldüğü gibi x değişkeninin düşük anlamlı byte değeri (34H) düşük sayısal adreste (1A00H) olacak biçimde yerleştirilmiştir. 

1. İkinci bir yerleşim biçimi, düşük anlamlı byte'ın yüksek sayısal adrese yerleştirilmesidir. Böyle yerleşim biçimine big endian denir. Motorola işlemcileri bu yerleşim biçimini kullanır. Bu işlemcilerin kullanıldığı sistemlerde örneğin **`int x = 0x1234;`** biçimindeki bir x değişkeni bellekte 1A00 adresinden başlayarak yerleştirilmiş olsun:

![](necati%20ergin%20c%20ders%20notlar%C4%B1%200662c25412974b26a3c99cb963fe8fc8/image3.png)

Şekilden de görüldüğü gibi x değişkeninin düşük anlamlı byte değeri (34H) yüksek sayısal adreste (1A00H) olacak biçimde yerleştirilmiştir. Aşağıdaki kod kullanılan sistemin little endian ya da big endian oldugunu söylüyor: *int* main()

```c
int main() {
	int x = 1;
	if (*(char *)&x)
		printf("little endian\n");
	else
		printf("big endian\n");
	return 0;
}
```

- bir stringin null olup olmadıgını anlamanın birkac yolu vardır
    - if (!str)
    - if (str[0] == '\0')
    - if (str[0] == NULL)
    - if (strlen(str) == 0)
- VOID POINTER: Bazı fonksiyonlar bellek blokları üzerinde genelleştirilmiş işlemler yapar. Bu fonksiyonlar işlem yaptıkları bellek bloklarında ne olduğuyla ilgilenmez. Bir bellek bloğunun içeriğinin bellekte başka bir yere kopyalandığını düşünün. fonksiyon kaynak adresten hedef adrese byte byte kopyalama yaparak bu amacı gerçekleştirebilir. Böyle bir fonksiyonin parametre değişkenleri hangi türden olmalıdır? void göstericiler herhangi bir türden olmayan göstericilerdir. Bu türden değişkenlerin tanımlarında void anahtar sözcüğü kullanılır: void *ptr; void göstericilerin tür bilgisi yoktur. void göstericilerde adreslerin yalnızca sayısal bileşenleri saklanır. Bu yüzden void göstericilerle diğer türden göstericiler (adresler) arasında yapılan atamalar geçerlidir. void türden bir göstericiye herhangi bir türden bir adres sorunsuzca atanabilir. Belirli türden bir gösterici değişkene void türden bir adres de aynı şekilde sorunsuzca atanabilir. normalde

```c
int x = 10;
int *xPtr = &x;
```

ifadesinde xPtr, x'in değerinin saklandıgı ram blogunun adresini tutuyordu yani x'i gösteriyordu. peki what tf is a void pointer? Öyle bir gösterici olsun ki hiçbir nesneyi göstermesin. Hiçbir yeri göstermeyen bir göstericinin değeri öyle bir adres olmalıdır ki, bu adresin başka hiçbir amaçla kullanılmadığı güvence altına alınmış olsun. İşte hiçbir yeri göstermeyen bir adres olarak kullanılması amacıyla bazı başlık dosyalarında standart bir simgesel değişmez tanımlanmıştır. Bu simgesel değişmez NULL simgesel değişmezi olarak bilinir (symbolic constant just like our #define SIZE 10). dolayısıyla bir void pointer'a değer olarak yalnızca NULL atanabilir.  

```c
void fun() {
	int a;
	void *vPtr = a; // geçerli
}
```

### string

- C derleyicileri, derleme aşamasında bir dizgeyle karşılaştığında, önce bu dizgeyi oluşturan karakterleri belleğin güvenli bir bölgesine yerleştirir, sonuna sonlandırıcı karakteri ekler. Daha sonra dizge yerine, yerleştirildiği yerin başlangıç adresini koyar. Bu durumda dizge ifadeleri aslında, dizgelerin derleyici tarafından yerleştirildiği dizinin başlangıç adresidir
- garip fakat aşağıdaki ifade b yazdıracaktir

```c
int	main(void)
{                                                                 
	putchar(*"bugra");
}                                                               
```

- pointerla tanımlanmış stringler değiştirilemez yani immutable yapıdadırlar. o yüzden böyle bir stringi modify edemezsin:

```c
char *str = "abc";
str = "123"; // geçersiz
```

ya da direkt karşılaştıramazsın 

```c
char *str = "bugra";
char *str2 = "cemre";
if (str == str2) // geçersiz
if (strcmp(str, str2) == 1) // demelisin
```

- stringler statik ömürlüdürler yani global değişkenler gibi program başlayınca başlarlar ve bitene kadar hafızada saklanırlar.
- birbirinin aynısı stringler için derleyici 2 farklı şey yapar
    - her biri için ayrı yer de ayırabilir
    - daha modern bir compiler ise aynı olan stringler için bir kopya saklar, ikisinden biri çağrıldığında o kopyayı kullanır
- söylendiği gibi C'de stringler esasen char arrayleridir. bir string tanımlamanın 3 yolu vardır
    - char str[100] = "bugrahan karamollaoglu"
    - char str[ ] = “bugrahan karamollaoglu”
    - char *str = "bugrahan karamollaoglu"

bilinenin aksine **`char str[]`** ve **`char *str`** aynı değildir. char pointer değişkenlere bir ilk değer verildiğinde derleyici bunu bir string olarak anlar. yani string belleğe yerleştirildikten sonra başlangıç adresi pointera atanır. oysa char arraylerinde (char s[10]) önce array için yer ayrılır sonra karakterler tek tek arrayin elemanları olarak yerleştirilirler. Dizi elemanlarına tek tek char türden değişmezlerle ilkdeğer verme işlemi zahmetli olduğu için, programcının işini kolaylaştırmak amacı ile böyle bir ilkdeğer verme kuralı getirilmiştir.

```c
char s[10] = "bugra";
```

demek aslında

```c
char s[10] = {'b','u','g','r','a', '\0'};
```

demenin kısa yoludur. aralarındaki bir diğer fark da **`char *str`** diye tanımladığın stringin **`char str[]`**'nin aksine RAM’de read-only kısımda saklanmasıdır. read-only saklanan bir veri sonrasında *modifiye edilemez.* mesela 

```c
int main() {
	char *str = "bugra";
	char str2[] = "bugra";
	str[2] = 's';  // geçersiz bc *str
	str2[2] = 's'; // geçerli bc str[]
}
```

- pointers that point to an other pointer: mesela **`int *p`** dedigimizde 8 byte'lık bir (int *) türünden pointer tanımlamıs oluruz (bütün pointerlar 8 byte’tır). eğer bunu bir integer'a atasaydık &atadigimiz_int diyince o intin değerini alırdık. fakat direkt olarak &p dediğimizde ne olur? işte o zaman (int * *) türünde bir baska pointer daha devreye girer:

```c
int x = 10;
int *xPtr = &x;
int **xPtrPtr = &p;
```

burada xPtrPtr çift pointerının adresi, xPtr pointerının yani x integerının değerini tutan hücrenin adresini tutan pointerın adres değerinin tutuldugu hücrenin adresidir.......a 

bu durumda nasıl ki *p demek x yani 10 demekse, *pp demek de p demektir.

### structures

- aralarında mantıksal bir ilişki olan fakat veri tipleri olarak farklı (mesela isim yaş boy) birden fazla değişleni hafızada aynı blogda tutabilmeye yarayan kod yapılarıdır. icerinde birden fazla degiskeni tanımlayıp daha sonra bunlara ulasabilirsin. mesela:

```c
struct Person {
	int age;
	float height;
	char name[20];
};

int main() {
	struct Person ahmet, mehmet;
}
```

daha önce global bir structure yarattı, daha sonra main()'de de Person isimli bu struct'a örnekler atadı. bu örnek yaratma işini struct'tan hemen sonra da yapabilirdi: 

```c
struct Person {
	/* ...  */
} ahmet, mehmet;
```

böyle yapmanın dezavantajı artık aynı Kişi structı türünden bir başka değişken daha tanımlayamazsın. 

- nasıl ki array elemanlarına ulasmak icin **`[]`** operatörü kullanılıyorsa struct elemanlarına erisim icin de **`.`** operatörü kullanılır:

```c
struct Cars {
	int year;
	char brand[20];
	char model[20];
};

int main() {
	struct Cars myCar;
	myCar.year = 2001;
	myCar.brand = "Lancia";
	myCar.model = "Thema";
	printf("year: %d\n", myCar.year);
	printf("brand: %s\n", myCar.brand);
	printf("model: %s\n", myCar.model);
}
```

- ptr bir yapı türünden bir gösterici ve mem de o yapının bir elemanı olmak üzere ptr'nin gösterdiği nesnenin mem isimli elemanına aşağıdaki gibi erişilebilir: (*p).mem. bu ifade **`->`** operatörüyle de yazılabilir  (*ptr).mem;

```c
(*ptr).mem == ptr->mem
```

Nokta ve ok işleçlerinin her ikisi de elemana erişmek için kullanılır. Ancak nokta işleci yapı değişkeninin kendisiyle, ok işleci ise adresiyle erişim sağlar.

### linked lists

- birbirine mantıksal açıdan bağlı nesnelerin ardışık biçimde tutulmadıgı fakat birbirine baglı oldugu dizilere linked lists denir. linked listslerde her bir eleman iki bilgiyi depolar
    - içindeki verinin bilgisi
    - kendisinden bir sonraki elemanın adres bilgisi

buna düğüm yani node denir. 

```c
struct Node {
	int data;
	struct Node *next_node;
};
```

- bir arrayin herhangi bir elemanına, dizi kaç elemanlı olursa olsun, ulaşma hızı aynıdır çünkü bütün arrayi baştan itibaren aradıgımız elemanı buluncaya dek tarayarak değil, adresler üzerinden - [20] [100] [10001] - ulaşıyoruz. oysa linked lists yani bağlı listelerde baştan itibaren tek tek arama yapılır. arraylerde eleman ekleme ya da silme için blok kaydırma yapılması gerekir çünkü sıralıdır, oysa bağlı listelerde bu çok daha kolaydır.
- typedef: bu anahtar sözcük kendi veri tipimizi yaratmamızı sağlar. aslında kendi veri tipimizi yaratmıyoruz, sadece var olan veri tipini rename etmemize yarıyor:

```c
typedef int my_int
my_int a = 30;
```

aynı şeyi structlarla da kullanabilirsin 

```c
typedef struct Person {
	int age;
	char name[20];
} p;

int main() {
	p ben;
	ben.age = 20;
	strcpy(ben.name, "bugra");
	printf("%d\n", ben.age);
	printf("%s\n", ben.name);
}
```

### bitwise operators

- bitwise operatorleri bir tam sayının bitleri üzerinde işlemler yapar. daha çok low level ve sistem programlamacılığında kullanılır. işleme soktukları tam sayıları bir bütün olarak değil bit bit ele alırlar. gerçek sayılarla değil integerlarla kullanılabilirler.
- toplam 11 bitwise operator vardır
    - **`~`** → bitwise not: bir bit dizisinde 1’leri 0, 0’ları 1 yapmaya yarar.
    
    ```c
    int a = 14; // 14'ün bitleri 1110
    a = ~a;     // a'nın bitleri 0001 oldu (yani sayımız 1 oldu)
    ```
    
    - **`<< ya da >>`** → bitwise left/right shift: bitleri n kadar sola ya da sağa kaydırır
    
    ```c
    int a = 14; // 1110
    a = a >> 2; // 0011 oldu
    ```
    
    - **`&`** → (bitsel ve) bitwise and: bit karşılaştırır. sadece 1 ve 1 bitlerinde 1 döndürür
    
    ```c
    int a = 14;  // 1110
    int b = 9;   // 1001
    int c = a&b; // c: 1000 (8)
    ```
    
    - **`^`** → (bitsel özel veya) bitwise exor: sadece 0ve1 durumunda 1 verir
    - `|` **→** (bitsel veya) bitwise or: ikisinden en az biri 1 varsa 1 verir
    - **`<<=, >>=, &=, ^=, |=`** → assignment operators:

### command line arguments

- main() fonksiyonu 3 farklı şekilde yazılabilir

```c
int main()
int main(void)
int main(int ac, char **av) 
```

- bütün argümanlarını yazdıran program:

```c
int main(int ac, char **av) {
	int i = 0;
	while (i < ac) {
		printf("av[%d] = %s\n", i, av[i]);
	}
}
```

### dosyalar

- bir dosya açtığında dosya sistem dosyalarında mevcut olan file table isimli veri tablosunda tutulur. dosya açmak için kullanılan open() fonksiyonu dosyanın adını parametre olarak alır, dönüş değeri ise dosyanın sıra numarasıdır.
- close() fonksiyonu ile açtığın dosyayı kapatmalısın.
- bir dosya byte'lardan oluşur.Dosyadaki her bir byte a 0'dan başlayarak artan sırada bir sayı karşılık getirilir. Bu sayıya ilgili byte ın ofset numarası denir. Dosya konum göstericisi içsel olarak tutulan long türden bir değişkendir, bir ofset değeri yani bir byte numarası belirtir. Dosyaya yazan ve dosyadan okuma yapan standart işlevler, bu yazma ve okuma işlemlerini her zaman dosya konum göstericisinin gösterdiği yerden yapar. Bu işlevler, dosyanın neresine yazılacağını ya da dosyanın neresinden okunacağını gösteren bir değer istemez. Örneğin dosya konum göstericisinin gösterdiği yer 100. ofset olsun. Dosyadan 10 byte bilgi okumak için bir sistem işlevi çağrıldığında, 100. ofsetden başlayarak 10 byte bilgi okunur. İşletim sisteminin dosya göstericisini konumlandıran bir sistem işlevi vardır. Dosya ilk açıldığında dosya konum göstericisi 0. ofseti gösterir. Örneğin bir dosyanın 100. byte ından başlayarak 10 byte okunmak istenirse sırası ile şu işlemlerin yapılması gerekir: İlgili dosya açılır dosya konum göstericisi 100. offset'e konumlandırılır Dosyadan 10 byte okunur Dosya kapatılır.

### variadic functions

- C'de bazı fonksiyonlar değişken sayıda argüman alabilir. bunlar fun(a, ...) şeklinde gösterilir. elipsis argüman sayısının belli olmadıgını gösterir. bu belirsiz sayıdaki argümanları handle edebilmek için **`stdarg.h`** kütüphanesinden **`va_arg`** yapısını kullanıyoruz
    - va_list: gelen parametreleri bu veri tipindeki bir elemanda tutacaksın
    - va_start: parametre işleme eylemini başlatan fonksiyondur. ilk parametresi va_list elemanı, ikincisi parametrenin tipidir.
    - va_arg: gelen parametreleri birer birer işlemek için kullanılır. her çağrılışında bir sonraki parametre girer.
    - va_end: parametre işleme eyleminin bittiğini gösterir.
    
    ```c
    int add(int value, ...) {
    	// öncelikle va_list türünde değişkenimizi yaratıyoruz
    	va_list vp;
    	int sum = 0;
    	// sonra va_start() ile argüman işleme prosesini baslatıyoruz
    	va_start(vp, value);
    	while (value) {
    		// va_arg() ilk çağrılışta 10'u alır sonra 20'yi sonra 3'ü en son 40'ı
    		// ilk parametresi va_list değişkeni, ikincisi parametrelerin tipidir
    		sum += va_arg(vp, int);
    		value--;
    	}
    	// yazmasak da oluyor ama just bc readability
    	va_end(vp);
    	return sum;
    }
    
    int main() {
    	// ilk olarak gireceğini parametre sayısı sonra parametreler
    	printf("%d\n", add(4, 10, 20, 3, 40));
    }
    ```
    

---