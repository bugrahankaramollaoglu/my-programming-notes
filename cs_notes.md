# cs notes

- wifi: wireless fidelity
- lan: local area network yani bir modeme bağlı birden çok cihazın oluşturduğu sistem. cihazların arasındaki veri alışverişini sağlayan, haliyle internet dediğimiz şeyin arka planındaki protokolün adı tcp. bunun geniş hali wan (wide area network), which is also known as internet.
- IP: internet protocol
- bir websitesine ulaşmaya çalışan tarafa client, ulaşmak istenen tarafa sunucu/server, bu aradaki ilişkiyi yapan protokole de http deniyor
- dynamically typed demek şu demektir: değişkenlerin başında değişken türü belirtmek zorunda değilsin. python buna örnektir, c değildir. aksine de statically typed languages denir.
- internet resmi olarak 1ocak 1983'te doğdu. abd savunma sanayisinin bir projesi olan arpanet bünyesindeki bilgisayarlar arasında tek bir network altında mesajlasma yöntemi gelistirilmek istendi ve internet ortaya çıktı. vinton cerf ve robert khan isminde iki mühendis internet protokollerinin temellerini attı.
- leak yer ayrılmış bir char stringini free’lemediginde oluyor. segfault ise erişim iznin olmayan bir yere erişmeye çalıştığında. leak’leri şöyle kontrol ediyosun

```c
system("leaks a.out");
```

     segfault’u ise lldb ile yapabilirsin  

```c
lldb ./a.out ve sonrasında r'ye basarak bakabilirsin
```

## **bitwise operators**

- bitwise operatörleri
    - ^ xor : sadece 1 ve 0’da 1 verir.
    - ~ complement : 1’leri 0, 0’ları 1 yapar.
    - & and : sadece 1 ve 1’de 1 verir.
    - | or : en az 1 varsa 1 verir.
    - << shift_left : soldaki biti sağdaki kadar sola kaydırır.
    - >> shift_right : soldaki biti sağdaki kadar sağa kaydırır.
- | or :

```c
int	main(void)
{
	int a = 12;
	int b = 25;
	printf("%d", a | b);
}
```

- ~ complement: binary’de 7’nin (111) zıttı (~ yani tildesi) -8’dir (1000).  ~ işareti bitwise complement olarak geçer 0’ları 1, 1’leri 0 yapar. bir sayının binary’de tersini almak için bir fazlasını -’yle çarpmak gerekir. mesela 25’in bitleri 11001’dir. bunun ~’lisi 00110’dır. bu da 5’e denk gelir. fakat 25’in ~’si 5 değil -26’dır. **For any integer n , bitwise complement of n will be `-(n + 1)`.** To understand this, you should have the knowledge of 2's complement. 2’nin tamlayani bitlerin ters çevrilip çıkan sayıya 1 (00000001) eklenmiş haliydi.

```c
int	main(void)
{
	printf("output: %d\n", ~-19);
} >>> 18

int	main(void)
{
	printf("output: %d\n", ~35);
} >>> -36
```

- ^ xor:

```c
int	main(void)
{
	int a = 12;
	int b = 25;
	printf("%d", a ^ b);
}
```

```c
// binary to decimal
int main(void)
{
    int i = 0;
    int j = 1;

    printf("j is initially: %d\n", j);
    while (i < 32)
    {
        j = j << 1;
        printf("j is: %d\n", j);
        i++;
    }
    return 0;
}
```

- çok ilginç bir string bilgisi:

```c
int main()
{
    char *str1 = "hello";
    char *str2 = "hello";

    char *str3 = malloc(sizeof(char) * 5 + 1);
    str3[0] = 'h';
    str3[1] = 'e';
    str3[2] = 'l';
    str3[3] = 'l';
    str3[4] = 'o';
    str3[5] = '\0';

    printf("str1: %c - %c - %c - %c - %c\n", str1[0], str1[1], str1[2], str1[3], str1[4]);
    printf("str1: %p - %p - %p - %p - %p\n\n", &str1[0], &str1[1], &str1[2], &str1[3], &str1[4]);
    /*  str1: h - e - l - l - o
        str1: 0x109c54efa - 0x109c54efb - 0x109c54efc - 0x109c54efd - 0x109c54efe */

    printf("str2: %c - %c - %c - %c - %c\n", str2[0], str2[1], str2[2], str2[3], str2[4]);
    printf("str2: %p - %p - %p - %p - %p\n\n", &str2[0], &str2[1], &str2[2], &str2[3], &str2[4]);
    /*  str2: h - e - l - l - o
        str2: 0x109c54efa - 0x109c54efb - 0x109c54efc - 0x109c54efd - 0x109c54efe */

    printf("str3: %c - %c - %c - %c - %c\n", str3[0], str3[1], str3[2], str3[3], str3[4]);
    printf("str3: %p - %p - %p - %p - %p\n\n", &str3[0], &str3[1], &str3[2], &str3[3], &str3[4]);
    /*  str3: h - e - l - l - o
        str3: 0x7fb6014058b0 - 0x7fb6014058b1 - 0x7fb6014058b2 - 0x7fb6014058b3 - 0x7fb6014058b4 */

    free(str1); // won't work bc str1 is a constant (immutable string, stored in read-only memory)
    free(str2); // same
    free(str3); // works bc str3 is a mutable string (stored in heap)
}
```

- how to open a file?

```c
#include <fcntl.h>

/* önce file1 isminde dosya oluştur */
int main()
{
    int fd;
    // dosyanın id'sini open ile fd'ye atip izinleri belirliyoruz
    fd = open("file1", O_RDWR);
    char *s = "bugra";
    // fd id'li dosyaya (file1) s'nin değerini yazdırıyoruz
    write(fd, s, strlen(s));
}
```

- sonsuz döngüde yarattığımız komutlardan ctrl+c ile çıkabiliyorduk. bununla çıkılamasın istiyosak daemon() fonksiyonunu kullanırız.

```c
int main()
{
    daemon(1, 1);
    while (5)
        printf("Lol\n");
}
```

- As malloc() returns the address of the first byte of the allocated memory, free() accepts, as only parameter, the address of this first byte

```c
char *str = malloc(100);
int *arr = malloc(sizeof(int) * 5);
free(str);
free(arr);
```

- rand() ve srand() ile sonsuz random sayı generatoru

```c
int	main(int argc, char *argv[])
{
	int seed;
	int i = 0;
	seed = time(NULL);
	srand(seed);
	while (1)
	{
		sleep(1);
		printf("rand[%d]= %d\n", i, rand() % 10);
		++i;
	}
	return (0);
}
```

- prime numbers in a specified range:

```c
int is_prime(int nb)
{
    int i = 2;
    if (nb == 1 || nb == 0)
        return (0);
    while (i <= nb / 2)
    {
        if (nb % i == 0)
            return (0);
        i++;
    }
    return (1);
}

int main(int ac, char **av)
{
    if (ac == 3)
    {
        int nb1 = atoi(av[1]);
        int nb2 = atoi(av[2]);
        while (nb1 <= nb2)
        {
            if (is_prime(nb1) == 1)
                printf("%d ", nb1);
            nb1++;
        }
    }
}
```

- in pointers,

```c
char *str = "bugra";
```

- bir pointera başka bir tipte pointerın adresini atayamazsın

```c
int x = 33;
char *charPointer = &x // YANLIŞ
int *intPointer = &x // DOĞRU
*intPointer = 44; // x artık 33 değil 44
```

- recursive kendi kendini çağıran fonksiyon demektir. faktöriyel bulma soruları genelde bu metotla bulunur:

```c
int fac_find(int nb)
{
    if (nb <= 1)
        return 1;
    return (nb * fac_find(nb - 1));
}

int main()
{
    int fac_to_find;
    printf("enter a num:");
    scanf("%d", &fac_to_find);
    int result = fac_find(fac_to_find);
    printf("%d", result);
}
```

string yazdırırken recursive  

```c
void string_recursive(char *str)
{
    if (strlen(str) <= 0)
        return;
    write(1, &str[0], 1);
    string_recursive(str + 1);
}

int main()
{
    string_recursive("bugrahan");
}
```

- uint8_t, uint16_t, uint32_t and uint64_t  are equal respectively to: unsigned char, unsigned short, unsigned int and unsigned long long.
- clean code kuralları
    - DRY - don’t repeat yourself: DRY refers to code writing methodology. DRY usually refers to code duplication. If we write the same logic more than once, we should “DRY up our code.” A common way to DRY up code is to wrap our duplicated logic with a function and replace all places it appears with function calls.
    - KISS – Keep It Simple Stupid
    - YAGNI – You Aren’t Gonna Need It
    - TDD – Test Driven Development:
        1. Decide on the desired functionality
        2. Create the test for that functionality first. The test fails since no code exists yet.
        3. Write the code that implements the desired functionality. The test now passes.
        4. Repeat.
    - BDUF – Big Design Up Front: This acronym is here to remind us not get over carried with super complex architecture. We shouldn’t spend 3 months designing our application before even writing the first line of code. Start small and iterate.
- SOLID kuralları
    1. S – Single Responsibility Principle: Very similar to Unix’s “Do one thing and do it well”.
    2. O – Open-Closed Principle
    3. L – Liskov Substitution Principle
    4. I – Interface Segregation Principle
    5. D – Dependency Inversion Principle
- VALGRIND
- y2k problemi (year 2000 problem) was a disaster in electronic devices in a global scale that was caused by computers when dealing with dates beyond December 31, 1999. they interpreted 00 as 1900, not 2000 which proved a disaster.
- programlama dilleri renkleri yaratmak için RGB denilen sistem kullanır. Red, Green, Blue. Bu üç temel renk farklı oranlarda karıştırılınca diğer renkler ortaya çıkar. 0-255 arası tonlar alabilirler. ayrıca spesifik bir renk #000000 sistemiyle gösterilir. beyazın tonu 255/255/255'tir o yüzden #FFFFFF'tir kodu. bu kod hexadecimal oldugu icin, F'de en yüksek rakam oldugu icin (15) F'e denk gelir. hexadecimal ve decimal aynı hafızayı kullanırlar sadece biri görüntüde daha kolay gelir göze.
- 8 bitle sayabileceğin en yüksek sayı: 255'dir.
- binary sisteminin 0 ve 1'den oluşması şartı yoktur, a ve b, x ve y de olabilirdi. çünkü nihayetinde temsil ettikleri şey yalnızca mantık kapıları (logic gates) ve elektriğin çalışma mantığıdır. çünkü elektrik ya vardır, ya da yoktur bu yüzden ilk bilgisayarlar binary sistem mantığıyla çıkmıştır.
- bir klasörde finder ile işlem yaparsan macos .DS_Store isimli bir dosya oluşturur.
- pdf boyutu küçültme:

```
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
-dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

- leak kontrolü yapan program: leakler normalde run-time’da malloc ve calloc ile açtığımız yerleri kapatmayı unuttuğumuz zaman olur. bu program sayesinde satır ve boyut bilgisiyle beraber öğrenebiliyoruz. [https://www.codeproject.com/Articles/19361/Memory-Leak-Detection-in-C](https://www.codeproject.com/Articles/19361/Memory-Leak-Detection-in-C)
- 3 çeşit hata vardır
    - programcı hatası: leaksler, typolar, yanlış yazılan döngüler vs. bu kategoridedir.
    - algoritma hatası: program görünürde çalışır yani derlenir fakat istendiği gibi çalışmaz yahut eksik çalışır. en zor hata türüdür.
    - mantık hatası: 0a bölme, 0’ın 0. kuvveti vs. gibi irrasyonel hesaplamalar yapma
    - istisnai hatalar: mimariden yahut donanımdan kaynaklanabilecek hatalar. m2’de derlenen kodun m1’de derlenmemesi, gibi.
- some important people
    - james gosling - javanın yaratıcısı
    - guido van rossum - pythonının yaratıcısı
    - bjarne stroustrup - cpp yaratıcısı
    - dennis ritchie - c yaratıcısı
    - linus torvalds - linux yaratıcısı
- Turing completeness:
- 5 Problems Any Programmer Should Be Able To Solve in less than 1 hour:
    - Problem 1 Write three functions that compute the sum of the numbers in a given list using a for-loop, a while-loop, and recursion.
    - Problem 2 Write a function that combines two lists by alternatingly taking elements. For example: given the two lists [a, b, c] and [1, 2, 3], the function should return [a, 1, b, 2, c, 3].
    - Problem 3 Write a function that computes the list of the first 100 Fibonacci numbers. By definition, the first two numbers in the Fibonacci sequence are 0 and 1, and each subsequent number is the sum of the previous two. As an example, here are the first 10 Fibonnaci numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, and 34.
    - Problem 4 Write a function that given a list of non negative integers, arranges them such that they form the largest possible number. For example, given [50, 2, 1, 9], the largest formed number is 95021. Update: Apparently this problem got a lot of people talking (although not as much as Problem 5 below.) You can click here to read my solution.
    - Problem 5 Write a program that outputs all possibilities to put + or - or nothing between the numbers 1, 2, ..., 9 (in this order) such that the result is always 100. For example: 1 + 2 + 34 – 5 + 67 – 8 + 9 = 100.
- 9 eylül 1947’de Harvard’da çalışan bir grubun bilgisayarına bir böcek giriyor. bunu cıkarma islemine debugging deniyor.
    
    ![Screenshot from 2023-03-18 18-17-55.png](cs%20notes%201c0a671ddbf049b49066ac3ea1ad16a5/Screenshot_from_2023-03-18_18-17-55.png)
    
    aslında bu efsane dogru degil cünkü bug kelimesi hailhazırda WWII’den beri kullanımdaydi. hatta 1896’daki bir kitaba kadar gidiyor (new katchecism of electricity). hatta bundan da önce shakespeare hamletin `bugs and goblins in my life` cümlesinde bu kelimeyi sorun, problem anlamında kullanıyor. kısaltılmamıs hali bugbear: anything causing seemingly needless or excessive fear or anxiety. 
    
- dosyalar genelde 2 sınıfa ayrılır
    - text (metin) dosyaları: açtığında okunabilir şeyler gelen dosyalardır.
    
    ```python
    f = open(dosya_adı, 'r')
    ```
    
    - binary (ikili) dosyalar: genelde açılamayan, açıldığında anlamsız karakterlerin oldugu dosya tipleridir. resim müzik video dosyaları vs.
    
    ```python
    f = open(dosya_adı, 'rb')
    # comes from binary
    ```
    
    GNU/Linux dağıtımlarında newline `\n` işareti ile gösterilirken bu windows’ta `\r\n` ile gösterilir. dosyaları ‘r’ ile açarken python satır sonlarını OS’deki yukarıdaki farklı kullanımlarına göre değiştirir. binary dosyalarda bu değişiklikler dosyayı tümden okunmaz kılabilir, o yüzden ‘rb’ ile açmaya dikkat.
    

 aslında text dosyaları da temelde ikili sistemi kullanır.

- dosya uzantıları ile dosya biçimleri arasında doğrudan bir bağlantı yoktur. O yüzden dosya uzantıları, dosya biçimini anlamak açısından güvenilir bir yöntem değildir. Bir resim dosyasının sonuna hangi uzantıyı getirirseniz getirin, o dosya bir resim dosyasıdır. Yani mesela bir resim dosyasının uzantısı yanlışlıkla veya bilerek .doc olarak değiştirilmişse, o dosya bir word dosyası haline gelmez.
- 8 bitle 256 farklı sayı gönderebiliriz. gönderebileceğimiz en yüksek sayı ise 255’tir. 256 sayısını göndermek istiyosak 9 bite ihtiyacımız vardır.
- 8 bitin 8’ini de kullanmak yerine bir biti boşta tutup kalan 7 bitle işlem yapabiliriz. bu boştaki biti bazı kontrolleri yapmak için kullanalım. mesela bir binary’de tek sayıda 1 varsa o sayı tektir. çift sayıda 1 varsa o sayı çifttir. sadece tek sayıları göndermek istediğimizi düşünürsek gelen sayıda eğer tek sayıda 1 varsa onun kontrol bitini yani sekizinci bitini 0 yaparak eşliğini bozmayalım. eğer çift sayıda 1 varsa kontrol bitini 1 yaparak tek sayıya çevirelim. buna `parity check`, kontrol bitine de `parity bit` denir.
- bilgisayar devrelerden oluşur. üzerinde devre yoksa o devrenin değeri 0 iken akım varken ortalama +5 volttur. 0 - 0 ile, 5volt ise 1 ile gösterilir.Yani devreden elektrik geçtiğinde o devrenin değeri 1, elektrik geçmediğinde ise 0 olmuş oluyor.
- what is *character encoding?* character encoding is the process where letters that are used in the alphabet is first translated into their ascii value in form of integer, than into binary and then into electrical signals.
- ascii tablosunda 0-127 arası toplam 128 sayı vardır. dolayısıyla ascii 7bitlik bir sistemdir. ilk 32 karakter non-printable yani çoğunlukla kaçış karakterleridir (escaping sequences).
- ascide her karakter 1 byte iken non-english karakterler (ş, ç, ğ vs.) 2 byte’tır.
- unicode dünyada alfabelerindeki tüm karakterlerin değişmez bir biçimde standartlaştırma çabasıdır. ascii ile ortak çalışır. ascii’den çok daha fazla non-english karakterin kodlamasına izin verir (ascii 128, unicode ~1000000). Unicode sisteminde her karakter tek ve benzersiz bir ‘kod konumuna’ (code point) karşılık gelir. mesela ‘a’ harfinin ascii karsılıgı 97 iken unicode karsılıgı u+0061’dir.
- britanyalı matematikçi alan turing teorik bir bilgisayar tasarlayıp adına `universal turing machine` dedi. bu makine üzerlerinde 0-1 yazan bantlardan olusuyodu. bunlarla tasıma, okuma ve yazma islemi yapılabiliyordu. fakat bu makinenin en büyük eksigi sonsuzu hesaplayamamasıydı, buna `halting problem` deniyor. bu olaydan `turing completeness` denilen şey doğdu. eğer bir programlama dili universal turing machine’i simüle edebiliyorsa *turing complete* denir o dil icin. tüm modern diller böyledir. bu yüzden bir dilde yazdıgımız bi seyi baska bi dilde de yazabiliyoruz.
- recursive factorial:

```python
def recursive_fac(n):
	if (n == 1)
		return n
	return (n * recursive_fac(n-1))

print(recursive_fac(4)) # 24
```

- fibonacci terimi eurocentric bi terimdir. 1202’de yayınladıgı meshur matematik kitabi *liber abaci*’de hindu-arap matematikcilerin halihazırda yıllardır kullanmakta oldugu matematiksel formülleri yazmıstır.  bunlardan bazıları hint ve arap sayıları, onluk sistem ve bizatihi fibonacci formülünün kendisidir. bu sayı dizisini sanksrit matematikçi Pingala bulmustur. 1-1-2-3-5 … sayı dizisini fibonaccinin adıyla ilk defa yazıya geciren 19yy’da edouard lucas diye bi fransız tarihci olmustur.
- vimde bir dosya templatei oluşturmak için:
    1. ~/.vim/templates oluştur, bunun içinde skeleton.cpp (artık hangi uzantı istiyosan) oluştur
    2. bunun içini template nası olsun istiyosan öyle doldur
    3. ~/.vimrc içine `autocmd BufNewFile *.cpp 0r ~/.vim/templates/skeleton.cpp` ekle
    4. artık vimle her açışında template’li hali gelecek
- derlemeli ve yorumlamalı diller arasındaki fark: C ve CPP gibi derlemeli dillerde kod önce derleyici tarafından binary koduna dönüştürülür daha sonra bu makine kodu bilgisayarın işlemcisi tarafından executable bir dosya haline getilir. python vs JS gibi yorumlamalı dillerde ise interpreter her satırı direkt çevirir ve çalıştırır. son zamanlarda ise farklı derleme türleri ortaya çıkmıştır JIT (just in time) ve AOT (ahead of time) compilation gibi. JIT derleme ve yorumlama tekniklerini karıştırarak kullanır, optimizasyon verimliliğine göre bazı kısımları derler bazılarını direkt çalıştırır. compile diller daha yüksek performans verirken yorumlamalılar daha hızlı ve esnek çalışır.
- programlama dillerinin kendileri de esasında birer programdır, o yüzden bir başka dilde yazılmak zorundadırlar.
- gcc flagleri: gcc’yi tek başına çağırdığımızda normalde [1] preprocessing [2] compilation [3] assembly [4] linking adımlarını otomatik olarak yapıyor.
    - `gcc -c` :  dersen linking adımını atlar ve .o uzantılı dosya oluşturur. normalde linking işlemi bu .o’ları program olan a.out’a çeviriyordu.
    - `gcc -g` : dersen programı debug modunda derler
    - `gcc -o` : program dosyasını isimlendirmemize yarar
    - `gcc -O2` : it will improve performance
    - `gcc -pedantic` : it is not requested but is a good one to check ISO C compliance
- normalde bilgisayarlar seri işlem yapması için tasarlanmıştır ama paralel programming denen metot sayesinde bilgisayar aynı anda birden fazla işlemler yapabilmektedir. macar matematikçi john von neumann elektronik bilgisayarların gereksinimlerini resmiyete dökmüştür. bir bilgisayar 4 temel şeye ihtiyaç duyar
    1. memory
    2. control unit
    3. arithmetic logic unit
    4. input/output

paralel programlamada bunlar aynıdır sadece kontrol üniteleri bir değil birden fazladır

- ./myProgram & diyerek bir prosesin arka planda çalışmasını sağlayabilirsin
- teorik olarak random sayı üretmek imkansızdır. bilgisayarlarda üretilen her sayı %100 rastgele olamıyor. buna pratikte bazı çözümler getirmeye çalışmışlar. çok ilginç bir çözüm yolu ise şöyle: **`lavarand`** denilen bir sistemle lav lambalarının tamamen rastgele oldugu farz edilen hareketlerini sensörlerle takip ederek bundan random sayılar üretilir.
- farklı case türleri:
    - snake_case:
        - Example: `this_is_snake_case`
    - dot.case:
        - Example: `this.is.dot.case`
    - path/case:
        - Example: `this/is/path/case`
    - param-case (kebab-case):
        - Example: `this-is-param-case`
    - PascalCase:
        - Example: `ThisIsPascalCase`
    - Header-Case (Train-Case):
        - Example: `This-Is-Header-Case`
    - Title Case:
        - Example: `This Is Title Case`
    - camelCase:
        - Example: `thisIsCamelCase`
    - Sentence case:
        - Example: `This is sentence case.`
    - CONSTANT_CASE:
        - Example: `THIS_IS_CONSTANT_CASE`
-