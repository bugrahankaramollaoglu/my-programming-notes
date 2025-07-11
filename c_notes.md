# c programming, just the FAQs

- sonuç ne olur?

```c
i = (a, b);
```

- C’de bir array l-value olamaz. yani direkt içine bir şey atayamazsın

```c
int ar[5], ar2[5];
ar = ar2; // yanlış
```

bunun yerine bir while iterator yaratıp teker teker ar2’nin elemanlarını ar’ın elemanlarına eşitlemeliyiz.

```c
int ar[5] = {10, 20, 30, 40, 50};
int ar2[5];

for (int i = 0; i < 5; i++) {
	ar2[i] = ar[i];
}
```

gelgelelim yalın arraylerin aksine struct içerisindeki arrayleri kopyalayabiliriz 

```c
typedef struct mySturct {
	int a;
	char b[20];
	char c[30];
} ms;

NAME ms, ms2;
/* ms ve ms2'yi değiştirdik */
ms = ms2;
```

- LEFT_VALUE bir sayı, harf ya da constant değişken olamaz

```c
4 = a; // yanlış
CONST_VAR = 200; // yanlış
's' = 'a'; // yanlış
```

- sayilar tiplerine göre değer alırlar ne verirsen ver. mesela

```c
int x = 15/4;
```

- değişkenler scope’larına göre 3’e ayrılır
    - extern: herhangi bir fonksiyon dışında tanımlanan değişkenlerdir. programdaki tüm kod bloklarında kullanılabilirler. such variables’ lifetimes range  from before `main()` is called until the program exits.
    - static: herhangi bir fonksiyon içinde tanımlanmayan statik bir değişkenin skopu o dosyanın tüm kod bloklarıdır. fakat statik değişken eğer bir fonksiyon içerisinde tanımlanmışsa geçerlilik alanı o local block alanı dahilindedir.
    - auto: bir fonksiyon içinde tanımlanmış auto bir değişkenin geçerlilik alanı o local block alanıdır.
- değişkenler yaşam sürelerien göre hafızada farklı yerlerde depolanırlar. statik ve global değişkenler RAM’de `data-segment` denilen kısımda saklanırlar. bu kısım bu tür değişkenler için özel olarak tahsis edilmiştir. bu kısım da ikiye ayrılır, birincisi ilklendirilmiş ikincisi ise ilklendirilmemiş değişkenleri tutmak için. fonksiyonların içinde tanımlanmış değişkenlerin ömürleri ise (statik tanımlanmamış) { } arasıdır. bunlar hafızanın 2. kısmı olan `stack` denilen yerde tutulurlar. `int a = 30` dediğinde bu stackte saklanır. stack’in belli bir boyutu vardır ve gittikçe birikir. eğer bu sınırı taşarsa stack overflow denilen olay meydana gelir. hafızanın üçüncü ve son kısmı ise `heap` denilen yerdir. stack gibi bu da gittikçe büyür fakat stackten farkı programcı açık bir şekilde malloc/calloc kullandığı zaman artmasıdır.
- normalde bir değişkeni ilklendirmezsen garbage value atanır içine. bunun iki istisnası vardır: `global` ve `statik` değişkenler. bunlar değer verilmediğinde otomatik olarak 0 alırlar.
- virtual memory is a technique that allows ram to use more memory than it has. it is like credit system. bunu da hdd’yi ram gibi göstererek yapıyor.
- çok sık kullanacağın bir değişkeni `register` ile tanımlarsan o değişkene daha çabuk erişirsin çünkü onu stack’te değil register’larda saklar. her değişkeni register ile kullanamazsın, boyutu ≤ int olmalı. ayrıca register değişken hafızada saklanmadığından & operatörü ile adresine erişemezsin.
- `declare` vs. `define` a variable:

```c
int a;       // this is declaration
int b = 30; // this is definition
```

- makrolarla değişkenin yanında fonksiyon da tanımlanabilir

```c
#define MY_AGE 30
#define CUBE(n) (n*n*n)

int main()
{
	int x = 5;
	int z = CUBE(++x);
	printf("%d", z);
}
```

- __LINE__ o anki satırı verir. debug için kullanılabilir

```c
int main() 
{
	printf("%d\n", __LINE__); >>> 3
}
```

__FILE__ o anki dosyanın ismini verir 

```c
int main()
{
	printf("%s\n", __FILE__); >>> main.c
}
```

__DATE__ makrosu da o anki tarihi verir

- `strcpy` vs. `memcpy` farkı: strcpy’de sadece string kopyalayabilirsin. memcpy ise void pointer kullandıgından direkt hafıza alanını kopyaladığı için üzerindeki datanın tipinin bir önemi yoktur. strcpy null görene kadar kopyaladığı için bir byte limiti verme zorunluluğu yoktur. memcpy’de ise sadece string değil int de kopyalayabiliriz ama onun sonunda null yok. bu durumda memcpy’ye kopyalanacak byte sayısı önceden verilmelidir.
- trailing spaces silme

```c
void trailing_trim(char *str)
{
	int len = strlen(str) - 1;
	while (*str)
		str++;
	while ((*str) == ' ' || (*str) == '\0')
		str--;
	*(++str) = '\0';
}
```

- ansi standartına göre bir derleyici en az 12 boyutlu pointer atayabilecek güçte olmalı
- bir pointera bir sayı eklediğimizde ne olur? mesela elimizde

```c
int main()
{
	int arr[] = {10, 20, 30, 40};
	int *ar = arr;
	ar += 2;
	printf("%d\n", ar[0]); // 30
}
```

şeklinde bir kod var. burada ar’ın başlangıç adresi 0x12F500 olsun. burada `ar += 2` ifadesi bu adrese 2 ekler ve adres artik 502 olur dersek yanlış olur. asıl olan şey bu adresin pointerın bir elemanının boyutu * arttırılan sayı **kadar hafızada ileriye ötelenmisidir. yani başlangıçtaki adres sizeof(int) * 2 byte kadar sağa ötelenmiştir. bu yüzden pointer aritmetiği void pointerlarla kullanılamaz çünkü elemanının boyutu belli değil. kullanmak istersen önce char pointera çevirip kullanıp sonra tekrar void pointera dönüştürebilirsin.

- null `0` da olabilir `(void *)0` da.
- pointer to function nedir: elimizde `pf` isminde bi tane pointerımız ve `strcmp` fonksiyonumuz olsun.

```c
int *pf;
int strcmp(const char *str, const char *str)
```

 biz bu pointerı strcmp fonksiyonuna point etmek istiyoruz. bu durumda yapmamız gereken şey şudur: 

```c
int (*pf)(const char *, const char *)
```

yani fonksiyonun ismini silip parantez içinde pointerın ismini yazıyoruz. parantezler burada mühim çünkü eğer parantez koymazsak ve

```c
int *pf(const char *, const char *) // YANLIŞ
```

yazarsak bu şu anlama gelir: 

```c
(int *) pf(const char *, const char *) 
```

ki bu da `int *` döndüren bir fonksiyon anlamına gelir. this is not what we want.

daha sonra fonksiyon declaration’ınını yaptıktan sonra strcmp’nin adresini pf’ye atiyoruz 

```c
pf = strcmp;
```

daha sonra pointerı kullanabiliriz. örnek: 

```c
int main()
{
	int strcmp(const char *, const char *);
	int (*pf)(const char *, const char *);
	pf = strcmp; // ya da pf = &strcmp
	printf("%d\n", pf("bugra", "bugrc"));
}
```

burada bir püf nokta parametrelere isim vermemektir.

- C’de VLA (variable-length-arrays) olayı yoktur. o yüzden bir arrayin boyutu yalnızca derleme zamanında belirlenebilir, çalışma zamanında belirlenemez. eğer belirlenebilseydi programlar çok daha yavaş çalışır, stack yapısı çok daha karmaşık olur, fonksiyon çağırmak çok daha az verimli olurdu.

```c
int i = 10;
int arr[i]; // C'de bu yanlıştır
```

- `calloc` ve `malloc` arasında 2 fark vardır
    - mallocun aksine calloc ayırdığı yeri 0’la doldurur
    - calloc returns an array of objects, malloc returns one object.
- stack is where all the functions’ local variables are stored. heap are where variables defined with malloc, calloc and realloc are stored. fetching memory from heap is much slower than fetching from stack. unlike stack, variables do not get deallocated automatically, so you must use free() later on. stack however doesn’t require this. this is why we don’t have to call free after we declare a normal variable but we do when we use malloc. recursive çağrılar da heap’te gerçekleşir.
- if you free a pointer, what you actually mean is that you freed the pointed-to memory on ram, not the pointer itself.
- `NULL` vs. `NUL` farkı: NULL stddef kütüphanesinde tanımlı NULL pointer gösteren bir makrodur. NUL ise ASCII tablosunun ilk elemanının ismidir. sayısal olarak 0’a eşittir. NULL can be defined as `(void *)0`, NUL as `\0`. both can be simply defined as `0`. NULL is meant to be used as a pointer, NUL as a character. mind the difference.
- ayırdığın yerin boyutunu öğrenmenin C’de bir yolu yoktur. somewhy free( ) knows it but it is a very complicated formula.
- eğer bir fonksiyonu yalnızca o dosyada kullanacaksan statik tanımlaman daha mantıklı olur.
- program normalde main( ) bittikten sonra biter. fakat C’de olan `atexit()` fonksiyonu sayesinde main bittikten sonra en son yapılıp her şeyin bitmesini istediğin işlemleri gerçekleştirebiliyoruz.

```c
void	print_bye(void)
{
	printf("atexit1\n");
	return ;
}

int main() {
	printf("hello\n");
	atexit(print_bye);
}
```

- `return()` vs. `exit()` farkı: ikisi birbirinden farklıdır. exit komple programdan çıkarken return o anki fonksiyon blogundan cıkıs yapar. fakat main’de çağrılan return ve exit aynı anlama gelir.
- adresler genelde 0x000000 ile 0xFFFFFFF arasındadır.
- in C, a string is actually a special sort of array whose type is char data type and ends with NUL \0. even deeper than that, there is no actually a data type as char. it is just a different version of its integer equivalent. in C++ however, char is a distinct data type.