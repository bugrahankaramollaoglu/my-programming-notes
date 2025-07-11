# 3 - get_next_line

**`RESOURCES`**

- [ ]  [https://www.codequoi.com/en/handling-a-file-by-its-descriptor-in-c/](https://www.codequoi.com/en/handling-a-file-by-its-descriptor-in-c/)
- [ ]  https://github.com/n1kito/Get_next_line readme’deki videolar
- [ ]  [https://www.codequoi.com/en/local-global-static-variables-in-c/](https://www.codequoi.com/en/local-global-static-variables-in-c/)

---

- get_next_line() projesinde bir dosyadan her seferinde bir satır okuyan bir gnl() fonksiyonu yazmamız isteniyor. gnl() her çalıştığında bir satır okuyacak, döngüde çalıştırdığımızda tüm bir dosyayı okuyabileceğiz. bunun için bir buffer char stringi kullanacağız. bu char stringin boyutu dinamik olacak yani 1 de 5 de 20 de verebileceğiz. satırları okurken okuyuşunda (çalışışında) bu verdiğimiz boyut kadar okuyacak.
- normalde bir dosyadan satır satır okuyan fgets(), getline(only linux) gibi fonksiyonlar vardır. bu projede biz kendi fonksiyonumuzu yazacağız.
- gnl bonusunda ek olarak tek bir fd’den değil birden çok fd’den okuma yapabilmeyi sağlıyoruz, bunu da fd’yi tutan değişkeni int değil int array yaparak yapiyoruz. array bitene kadar bütün fd’leri gnl’ye tabi tutuyoruz.

**`STUDY LIST IN GET_NEXT_LINE`**

- [ ]  static değişkenler nedir
- [ ]  file descriptor olayı
    - [ ]  read()
    - [ ]  write()
    - [ ]  open() fonksiyonları
- [ ]  struct yapısı
- [ ]  I/O in c
- [ ]  kütüphane yaratma
- [ ]  EOF nedir
- her satırın sonunda null işareti vardırson satır hariç tüm satırlarda ek olarak \n de vardır

```c
123123123 \n \0
1231 \n \0
123123123123 \n \0
123123 \0 
```

- karakterler 1 byte iken non-unicode'lar 2 byte'tır

```c
printf("bugra"); // 5 byte
printf("buğra"); // 6 bytec
```

- arabellek bir cihazda verilerin topluca yazılmadan evvel biriktirildikleri bellektir. amaç ilgili belleğin o anda bşaka bir işle uğraşırken o işin bitmesini beklemeden emir vererek hız kazanmaktır. önbellekten farklı olarak er ya da geç ilgili belleğe yazılır. gnl()’de kullandığımız buffer arabellek olarak kullanılmaktadır.
- `static değişkenler`: In computer programming, a static variable is a variable that has been allocated "statically", meaning that its lifetime (or "extent") is the entire run of the program. statik tanımladıgın bir fonksiyonu sadece o dosyada (bugra.c) kullanabilirsin. başka bir dosyada (cemre.c) o fonksiyonu çağırırsan hata alırsın aynı klasörün içinde olsalar dahi. bir başka özellik olarak static variables have a property of preserving their value even after they are out of their scope! Hence, static variables preserve their previous value in their previous scope and are not initialized again in the new scope. A static int variable remains in memory while the program is running. A normal or auto variable is destroyed when a function call where the variable was declared is over. for instance

```c
int fun() {
    int i = 5;
    i++;
    return i;
}

int fun2() {
	static int i = 5;
	i++;
	return i;
}

int main() 
{
    printf("%d\n", fun()); // 6
    printf("%d\n", fun()); // 6
    printf("%d\n", fun()); // 6
		printf("%d\n", fun2()); // 6
		printf("%d\n", fun2()); // 7
		printf("%d\n", fun2()); // 8
}
```

- global ve statik değişkenler ilklendirilmezlerse otomatik olarak 0 değeri atanır. normal değişkenlere ise çöp değer atanır:

```c
int x;

int main()
{
    int y;
    static int z;
    printf("x: %d\n", x); // 0
    printf("y: %d\n", y); // 21452
    printf("z: %d\n", z); // 0
}
```

- **`read()`** fonksiyonu nasıl çalışır?

```c
ssize_t read(int fd, void *buf, size_t nbyte);
```

read fonksiyonu fd id’li dosyadan nbyte kadar okuyup buf’a yazdırır. read() fonksiyonu 3 şey döndürebilir

- 0 —> EOF gelmiştir
- -1 —> hata vermiştir
- 1+ —> başarıyla okuduğu byte sayısını döndürür

mesela read() fonksiyonuyla “bugrahan\nkara” stringini fd id’li asd.txt dosyasına okuyalım. buffer’ımız da 5 byte olsun. read fonksiyonu önce **`bugra`** okur, asd’ye yazdırır, sonra 5 döndürür. read fonksiyonu aynı file descriptor’ı kullandigin sürece nerede kaldığını unutmadığı için tekrar baştan değil kaldığı yerden başlar okumaya. daha sonra **`han\nk`** okur, dosyaya yazdırır ve yine 5 döndürür. gördüğün gibi alt satıra geçse bile buffer size bitmediği sürece alt satırdan okumaya devam ediyor. şuan elinde 3 byte kaldı (ara) (sondaki null okunmuyor). normalde 5 byte döndürse de elinde olanı döndürmek zorunda olduğu için stringin sonuna geldiğinde 3 döndürür. işte bu yüzden read( ) fonksiyonu bir dosyanın sonuna geldiğinde 0 döndürür çünkü okuyacak bir şey kalmamıştır.

- EOF nedir? it means end of file. It's a sign that the end of a file is reached, and that there will be no data anymore. UNIX sistemlerde input almanı sonlandırmanı yarayan şeye denir. linux ve mac’te **`ctrl+d`,** windows’ta **`ctrl+z`**'dir.
- possible reasons for segmentation fault (occurs when a program attempts to access a memory location that it is not allowed to access, or attempts to access a memory location in a way that is not allowed)
    - loop segfault:
        - in a loop, you forgot to increment it
        - in a loop, you said = instead of ==
    - Accessing the next link in a linked-list without checking the current one is NULL or not
    - something has not been malloced
- bus error (occurs when your processor cannot even attempt the memory access requested, like trying to access an address that does not satisfy its alignment requirements.)

---