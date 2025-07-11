# 2 - ft_printf notları

### `kaynaklar`

- [https://csnotes.medium.com/ft-printf-tutorial-42project-f09b6dc1cd0e](https://csnotes.medium.com/ft-printf-tutorial-42project-f09b6dc1cd0e)
- [https://medium.com/@zhang.yine/ft-printf-d95747b7aa5a](https://medium.com/@zhang.yine/ft-printf-d95747b7aa5a)
- [https://cplusplus.com/reference/cstdio/printf/](https://cplusplus.com/reference/cstdio/printf/)
- https://github.com/settleformore/ft_printf
- this pdf

[secrets_of_printf.pdf](2%20-%20ft_printf%20notlar%C4%B1%2035ef6204b5b04e3fb116670fe48f5f29/secrets_of_printf.pdf)

---

- printf() fonksiyonu C’de terminale çıktı bastırmaya yariyor. en çok kullanılan fonksiyonlardan biridir. printf, fprintf, sprintf, snprintf, vprintf, vfprintf, vsprintf, vsnprintf gibi bir çok türevi vardır. bu projede amaç kendi printf'imizi yazmak. fakat sadece
    1. %c (char) 
    2. %s (string) 
    3. %d (integer) 
    4. %i (integer) 
    5. %p (pointer) 
    6. %u (unsigned integer)
    7. %x ve %X (küçük büyük hexadecimal) yazdırıyoruz.

**`STUDY LIST IN FT_PRINTF`**

- [ ]  man 2 printf
- [ ]  bağlı listeler
- [ ]  pointerlar (genel)
- [ ]  kütüphane nası oluşturulur
- [ ]  makefile
- [ ]  variadic fonksiyonlar (crux of the project)
- [ ]  veri tipleri (char integer vs.)
- [ ]  printf() conversion specifier’ları (%c %s %p vs.)
- [ ]  unsigned, hexadecimal vs. nedir
- [ ]  const nedir ne işe yarar , diff btw constant char vs. char
- [ ]  makrolar nedir nası tanımlanır
- [ ]  printf(), read() vs. return değerleri

**`TO DO LIST IN FT_PRINTF`**

- [ ]  kütüphane yarat
- [ ]  makefile yarat
- [ ]  öncelikle **`int ft_printf(const char *s, ...)`** fonksiyonuyla başla
- [ ]  printf’in % görmediği müddetçe char yazdırsın (ft_printf(”bugra kara” gibi). %görürse %’den  sonra bir char arasın. bu char’ın ne olduguna göre farklı işlemler yapacağın bir check() fonksiyonu yaz. eğer
    - [ ]  %c ya da %% ise putchar ile
    - [ ]  %s ise putstr ile
    - [ ]  %u,d ya da %i ise putnbr ile yazdir.
    - [ ]  kalanlara özel fonksiyon yaz
- [ ]  tüm bunları yaparken va_arg() yapısını kullanmalısın
- [ ]  testerlardan geçmeli

**LINKED LISTS**

- Linked lists are a way to store data with structures so that the programmer can automatically create a new place to store data whenever necessary. Specifically, the programmer writes a struct definition that contains variables holding information about something and that has a pointer to a struct of its same type (it has to be a pointer--otherwise, every time an element was created, it would create a new element, infinitely). Each of these individual structs or classes in the list is commonly known as a node or element of the list.
- A linked list is a set of dynamically allocated nodes, arranged in such a way that each node contains one value and one pointer. The pointer always points to the next member of the list. If the pointer is NULL, then it is the last node in the list. A linked list is held using a local pointer variable which points to the first item of the list. If that pointer is also NULL, then the list is considered to be empty. lets define a linked list:

```c
typedef struct node
{
    int val;
    struct node *next;
} my_node;

int main()
{
    /* This will be the unchanging first node */
    struct node *root;

    /* Now root points to a node struct */
    root = (struct node *)malloc(sizeof(struct node));
    if (!root)
        return 0;

    /* The node root points to has its next pointer equal to a null pointer set */
    root->next = NULL;

    /* By using the -> operator, you can modify what the node, a pointer, (root in this case) points to. */
    root->x = 5;

    /* Now we can use the nodes. Let's create a local variable which points to the first item of the list (called head): */
    my_node *head = NULL;

    head = (my_node *)malloc(sizeof(my_node));

    if (!head)
        return 0;

    head->val = 1;
    head->next = NULL;
}
```

**POINTERS**

- pointer nedir? değişkenler ve fonksiyonlar bilgisayarda geçici hafızada yani RAM’de saklanır. RAM birçok küçük hücreden oluşan bir dikdörtgen gibi düşünülebilir. bu hücrelerin her biri 1 byte yere sahip olsun. bu hücrelerin her birininde hexadecimal formatta bir sayısal numarası var. 0x00000’dan başlayip 0xFFFFFF gidiyor gibi düşünülebilir. bir integer değişkeni tanımladığımızda (ya da ilklendirdiğimizda) bu integer değişken (genelde) 4 byte olduğu için 4 adet kutucuğa ihtiyacı var saklanabilmesi için.

```c
int a = 42;
```

mesela tanımladıgım a degiskeni 0x15000, 0x15001, 0x15002, 0x15003 kutucuklarını almış olsun. pointer kavramı burada devreye giriyor. pointerlar en basit haliyle yine o değişken gibi aynı ram üzerinde bir başka yerde yer tutan (8 byte) ve içerisinde değer olarak gösterdiği değişkenin hafızadaki adresinin başlangıcını tutan değişkenlerdir. mesela bu değişkeni gösteren bir pointer tanımlarsak 

```c
int a = 42;
int *aPtr = &a;
```

artik aPtr pointeri hafızada a’nin adresinin başlangıcını tutuyor. buna kısaca genelde anin adresini tutuyor denir. 

- Bir integer pointer şöyle tanımlanır:
    
    ```c
    int *pointer_name = &variable;
    ```
    
- pointerların sembolü %p'dir. printf'le yazarken öyle kullanılır printf("%p", xptr) → 0012F88…
- asagidaki kod a'nın degerini degistiremez:

```c
void inc(int a)
{
    a++;
}

int main()
{
    int x = 5;
    inc(x);
    inc(x);
    inc(x);
    printf("%d\n", x);
} 
```

degissin istiyosan 2 sey yapabilirsin

ya pointer kullanacaksın ki adres üzerinde dogrudan degisiklik yapilsin

```c
void inc(int *a)
{
    (*a)++;
}

int main()
{
    int x = 5;
    inc(&x);
    inc(&x);
    inc(&x);
    printf("%d\n", x);
}
```

ya da local bir degisken return etmelisin

```c
int inc(int a)
{
    return (++a); // çalışıyor
    return (a+1); // çalışıyor
    return (a++); // çalışmıyor
}

int main()
{
    int x = 5;
    x = inc(x);
    x = inc(x);
    x = inc(x);
    printf("%d\n", x); // 8
} 
```

- 42de global degisken tanımlamak yasaktır. fakat bunun yerine struct{ } içerisinde tanimlayabilirsin:

```c
typedef struct myS
{
	int a;
	int b;
} t_env;

void fun(t_env *env)
{
	env->a = 40;
	env->b = 85;
}

// and then using these variables like

int main()
{
	t_env env;
	fun(&env);
	printf("%d\n", env.a); // 40
	printf("%d\n", env.b); // 85
}
```

- conversions
    - c - char
    - d or i - signed decimal integer
    - e or E - scientific notation
    - f - floating point
    - o - signed octal
    - s - string of characters
    - u - unsigned decimal integer
    - x - unsigned hexadecimal integer
        
        X - unsigned hexadecimal integer (capital 10AD2F)
        Hexadecimal is a numbering system with base 16. It can be used to represent large numbers with fewer digits. In this system there are 16 symbols or possible digit values from 0 to 9, followed by six alphabetic characters -- A, B, C, D, E and F. These characters are used to represent [decimal](https://www.tutorialspoint.com/automata_theory/chomsky_normal_form.htm) values from 10 to 15 in single [bits](https://www.techtarget.com/whatis/definition/bit-binary-digit).
        
    - p - pointer address
    - % - character
    - e - exponential float-point number

**MACROLAR**

- macrolar **`#define`** yapısıyla tanımlanır. değişken tanımlama gibi düşünebilirsin

```c
#define AGE 46

int main()
{
    printf("%d\n", AGE); // 46
}
```

örnek:

```c
#define MAX(x, y) (x > y ? x : y)

int main()
{
    int x = 5;
    int y = 10;
    int a = MAX(x, y);
    printf("%d\n", a); // 10
}
```

**VARIADIC FUNCTIONS**

- bir fonksiyonun sayisi belirsiz argüman alabilmesini sağlamak için va_list yapısını kullanıyoruz. argüman sayısını bilmediğimizi göstermek için de son parametresini `...` yapiyoruz. variadic fonksiyonları kullanırken `stdarg.h` kütüphanesini import etmeyi unutma.
- variadic fonksiyonların 4 macrosu var
    - **`va_list ap:`** parametreleri işlemeye başlamadan önce va_list tipinde bir değişken ilklendirmemiz gerekiyor. adı ap olsun. bu ap her bir parametreyi tutacak olan değişken.
    - **`va_start(ap, var):`** birinci argümanı `ap`, ikinci argümanı fonksiyona verdiğimiz, `...`'den bir önceki parametrenin ismi olan bu fonksiyon sinirsiz parametreleri işleme sürecine başlamadan önce kullanılmalı
    - **`va_arg(ap, data_type):`** birinci argümanı `ap`, ikinci argümanı aldığı parametrenin türü olan bu fonksiyon parametreleri teker teker işleyip bir sonraki parametreye geçmeye yariyor. mesela int fun(int a, ...) dedin ve buna fun(5, 1, 2, 3, 4, 5); verdin. va_arg()’ı her çağırdığında önce 1 sonra 2 sonra 3. parametreye geçecektir ve return değeri o parametre olacaktır.
    - **`va_end(ap):`** parametre işleme eylemini bitirmeye ve ayirdigi hafizayi freelemeye yariyor. aslında yazmasan da oluyor ama idk.
- variadic fonksiyonları kullanarak bir sayısı belirsiz parametrelerin toplandığı ve bu toplamı döndüren bir toplama fonksiyonu yazalim:

```c
// variadic fonksiyon oldugunu belirmek için son parametresi ...
int toplama(int sayi, ...)
{
    // va_list tipinde bir başlangıç noktası yaratiyoruz
    // bu değişken ...'e gelecek ilk parametreyi tutacak
    va_list arg;

    int i = 0;
    int toplam = 0;

    // va_start(baslangic_noktasi, ...'den bir önceki parametre) ile başlatıyoruz.
    // buna last-named-parameter şartı deniyor
    va_start(arg, sayi);

    while (i < sayi)
    {
        // va_arg(baslangic_noktasi, parametrenin_türü) fonksiyonu,
        // parametreleri işlemeye, iow, birer parametre atlamaya yariyor
        toplam += va_arg(arg, int);
        i++;
    }
    i = 0;

    // va_end(baslangic_noktasi) ile de bitiriyoruz parametre işleme olayını
    va_end(arg);

    return toplam;
}

int main()
{
    printf("%d\n", toplama(5, 1, 2, 3, 4, 5)); // 15
}
```

- parametrelerini yazdiran bi fonksiyon yazalim:

```c
void kounter(int num, ...)
{
    va_list ap;
    int kount = 0;
    int i = 0;
    va_start(ap, num);
    while (i < num)
    {
        printf("[%d]", va_arg(ap, int));
        i++;
    }
    va_end(ap);
}

int main()
{
    kounter(3, 10, 20, 30);
    putchar('\n');
} 
```

ya da verilen stringleri birlestiren fonksiyon 

```c
char *concatenate(int count, ...)
{
	va_list args;
	va_start(args, count);
	size_t total_length = 0;
	for (int i = 0; i < count; i++)
	{
		char *arg = va_arg(args, char *);
		total_length += strlen(arg);
	}
	va_end(args);

	char *result = malloc(total_length + 1);
	if (result == NULL)
	{
		return NULL;
	}

	va_start(args, count);
	size_t position = 0;
	for (int i = 0; i < count; i++)
	{
		char *arg = va_arg(args, char *);
		size_t length = strlen(arg);
		memcpy(result + position, arg, length);
		position += length;
	}
	va_end(args);

	result[total_length] = '\0';
	return result;
}

int main()
{
	printf("%s\n", concatenate(3, "bugra", "kara", "molla"));
}
```

- printf() bir şeyi ekrana yazdırsa da arka planda return olarak yazdırdığı şeyin size_t cinsinden uzunluğunu döndürüyor (null’u saymıyor). ft_printf de öyle yapmalı.

```c
int main()
{
    char a[] = "bugra";
    printf("%d\n", printf("%s\n", a));
} 
```

- non-unicode karakterler bir değil iki byte olarak hesaplanıyor:

```c
int	main(void)
{
	printf("%d\n", printf("buğra")); // buğra 6
	printf("%d\n", printf("bugra")); // bugra 5
}
```

- örnek

```c
int	main(void)
{
	printf("%%hello"); >>> %hello
}
```

- **`printf(”%c”, 300)`** yazarsan ascide 256 eleman var, başa sarıp 44'ün karsılıgını yazdırır

```c
printf("%c\n", 300); // ,
```

- **`printf(”%d”, "str")`** dersen random sayı döndürür

```c
printf("%d\n", "bugra"); 
```

- **`puts()`** vs. **`printf(`**) difference:  ikisi de ekrana bir şeyler yazdırmaya yariyor fakat aralarındaki en mühim fark puts sadece string yazdiriyor, bir de sonuna otomatik olarak \n koyuyor, printf koymuyor.
- örnek

```c
int	main(void)
{
	printf("%5.2f", 100.12345);
} >>> 100.12
```

- %f’ye .precision vermezsen 6 precision ile yazdirir
- %[flag][min width][precision][length modifier][conversion specifier]
- printf()’te % ile conversion arasına yazdığın sayı width belirtir:

```c
printf("%20d\n", 10); // 10
```

- # işareti 0x koymaya yarıyor

```c
printf("%#x", 15) // 0xf
```

- + işareti gelen sayıyı işaretiyle yazdırır

```c
printf("%+d", 150); // +150
printf("%+d", -59); // -59
```

- `unsigned` vs. `normal` integer: normal bir integer -2147483648 ile 2147483647 arasındadır. negatif de pozitif de olabilir. unsigned tipinde bir integer ise sadece 0 ve 4294967295 aralığında pozitif değerler alabilir. çok mantıklı çünkü ikisi de aynı byte (4) ve *unsigned integer* eksileri hesaba katmadığı için pozitif tarafta çok daha fazla geniş bir range’e ulaşabiliyor.
- pointerların başındaki 0x ifadesi hexadecimal oldugunu anlatmak icin konur. asıl adres 0x’ten sonraki kısımdır. 0 burada parser’a sayinin bir constant oldugunu, x de hexadecimal oldugunu soyler. tıpkı 42 sayisinin octal oldugunu anlatmak icin 042 sekilnde yazilmasi gibi.
- printfte makefile yazarken libtool kullanımı yasak, onun yerine ar komutunu kullanmamız gerekiyor. ar komutu object dosyalarını istediğimiz isimle ziplememize yariyor. The r option tells ar to add the object file to the archive or replace an existing object file with the same name. The c option tells ar to create the archive file if it does not exist. The s option tells ar to write an index into the archive, which speeds up subsequent searches of the archive.

---