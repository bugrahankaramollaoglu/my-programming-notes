# 1 - libft notları

`kaynaklar`

- [ ]  [https://stackoverflow.com/questions/5233514/where-to-find-stdio-h-functions-implementations](https://stackoverflow.com/questions/5233514/where-to-find-stdio-h-functions-implementations) 
kütüphane fonksiyonlarının kaynak kodları
- [ ]  [https://makefiletutorial.com/](https://makefiletutorial.com/)
makefile tutorial
- [ ]  [https://www.geeksforgeeks.org/data-structures/linked-list/](https://www.geeksforgeeks.org/data-structures/linked-list/)
    
    linked lists
    
- [ ]  [https://en.cppreference.com/w/c/string/byte](https://en.cppreference.com/w/c/string/byte)
c cpp
- [ ]  [şadi evren c listesi](https://www.youtube.com/watch?v=gHmaZ2zeLu8&list=PL4eNZvHTpYhnACSWVmRBEr1MviDZ26b5E)

---

**`STUDY LIST IN LIBFT`**

- [ ]  c’de linked lists
    - [ ]  baştan eleman ekleme
    - [ ]  ortadan ekleme
    - [ ]  sondan eleman ekleme
    - [ ]  listenin boyutunu alma
- [ ]  c’de file descriptor olayı, file handling
- [ ]  c’de standart kütüphane fonksiyonları (glibc)
- [ ]  c’de kütüphane yaratma
- [ ]  struct ve typedef yapısı
- [ ]  void pointer ve genel olarak pointerlar, pointer aritmetiği
- [ ]  fonksiyon pointerları nedir
- [ ]  size_t, unsigned nedir, farkı nedir
- [ ]  unsigned char nedir nasıl olur
- [ ]  makefile nedir ne işe yarar **`all $(NAME) clean .phony re`** vs.
- [ ]  bir değişkeni cast etme —> (char *)s;
- [ ]  fonksiyonlar **`man`** ve **`man 2`** page’leri kullanma
- [ ]  leak vs segfaultlar nasıl kontrol ediliyor, valgrind kullanımı

---

### libft fonksiyonları ne işe yarıyor

```markdown
ft_atoi : ascii türündeki str'yi integer'a çevirir
int ft_atoi(const char *str)

ft_bzero : s'ye baştan n kadar null koyar
oid ft_bzero(oid *s, size_t n)

ft_calloc : count adet size boyutunda nesne için yer ayırır ve ayırdıgı yeri nulla dolduru
oid *ft_calloc(size_t count, size_t size)

ft_isalnum : parametresi harf ya da rakamsa 1, değilse 0 döndürür
int ft_isalnum(int c)

ft_isalpha : parametresi harf ise 1, değilse 0 döndürür
int ft_isalpha(int c)

ft_isascii . parametresi ascii ise 1, değilse 0 döndürür
int ft_isascii(int c)

ft_isdigit : parametresi rakamsa 1, değilse 0 döndürür
int ft_isdigit(int c)

ft_isprint : parametresi printable (0-31 aralığında) ise 1, değilse 0 döndürür
int ft_isprint(int c)

ft_itoa : integer'ı char stringe çevirir
char *ft_itoa(int n)

ft_memchr : s'de c'yi buldugu zaman c dahil s'nin kalanını döndürür
void *ft_memchr(const void *s, int c, size_t n)

ft_memcmp : s1 ve s2'nin ilk n karakterini karşılaştırır, fark çıkarsa ascii farkını döndürür
int ft_memcmp(const void *s1, const void *s2, size_t n)

ft_memcpy : src'den dst'e n kadar kopyalar. aynı hafıza alanındaysa it may though overlap
void *ft_memcpy(void *dst, const void *src, int n)

ft_memmove : src'den dst'e len kadar kopyalar, aynı hafıza alanındaysa sondan kopyalar, sorun olma
oid *ft_memmove(void *dst, const void *src, size_t len)

ft_memset : b'nin ilk len karakterine c yazar
void *ft_memset(void *b, int c, size_t len)

ft_putchar_fd : dosyaya karakter yazdırır
void ft_putchar_fd(char c, int fd)

ft_putendl_fd : dosyaya string yazdırır, sonuna \n koyar
void ft_putendl_fd(char const *s, int fd)

ft_putnbr_fd : dosyaya sayı yazdırır
void ft_putnbr_fd(int n, int fd)

ft_putstr_fd : dosyaya string yazdırır
void ft_putstr_fd(char *s, int fd)

ft_tolower : büyükse küçük yapar
int ft_tolower(int c)

ft_toupper : küçükse büyük yapar
int ft_toupper(int c)

ft_split : s'yi c'lerden ayırıp 2D bir arraye atar, onu döndürür
char ft_split(char const *s, char c)

ft_strchr : s'de c'yi bulursa c dahil kalanını döndürür
char *ft_strchr(const char *s, int c)

ft_strrchr : s'de sondan geriye c'yi arar bulursa c dahil kalanı döndürür
char *ft_strrchr(const char *s, int c)

ft_strdup : s1'e önce yer ayırıp onu bir temp'e kopyalar, sonra tempi sonra döndürür
char *ft_strdup(const char *s1)

ft_striteri : s'nin tüm elemanlarını (f) fonksiyonuna tâbi tutar ama bunu string üzerinde yapar
void ft_striteri(char *s, void (*f)(unsigned int, char *))

ft_strmapi : s'nin tüm elemanlarını (f) fonksiyonuna tâbi tutar ama bunu buffer üzerinden yapar
char *ft_strmapi(char const *s, char (*f)(unsigned int, char))

ft_strjoin : s1 ve s2 stringlerini uç uca ekler
char *ft_strjoin(char const *s1, char const *s2)

ft_strlcat : src'yi dest'in sonuna atar ama destSize-1 kadar yer ayırır, null'a kesinlikle 1 byte bırakı
size_t ft_strlcat(char *dest, const char *src, size_t destSize)

ft_strlcpy : src'yi dest'e kopyalar ama maksimum destSize kadar yer ayırır
size_t ft_strlcpy(char *dest, const char *src, size_t destSize)

ft_strlen : s'nin uzunluğunu hesaplar
size_t ft_strlen(const char *s)

ft_strncmp : s1 ve s2'nin ilk n karakterini karşılaştırır, fark bulursa farkı döndürür
int ft_strncmp(const char *s1, const char *s2, size_t n)

ft_strnstr : haystack içinde ilk len karakterde needle arar, 
bulursa needle dahil kalanı döndürür. strchr'den farkı char değil string arar
char *ft_strnstr(const char *haystack, const char *needle, size_t len)

ft_strtrim : s1'in başından ve sonundan set ve türevlerine denk gelirse siler
char *ft_strtrim(char const *s1, const char *set)

ft_substr : str'nin start. indisinden itibaren len karakter kadar yazdırır
char *ft_substr(const char *str, unsigned int start, size_t len)

ft_lstnew : listeye yeni eleman ekler
t_list *ft_lstnew(oid *content)

ft_lstsize : listenin eleman sayısını verir
int ft_lstsize(t_list *lst)

ft_lstlast : listenin son elemanını verir
t_list *ft_lstlast(t_list *lst)

ft_lstadd_front : listeye baştan eleman ekler
void ft_lstadd_front(t_listalst, t_list *new)

ft_lstadd_back : listeye sondan eleman ekler
void ft_lstadd_back(t_listalst, t_list *new)

ft_lstdelone : listeden bir eleman siler yerini de free() ile serbest bırakır
void ft_lstdelone(t_list *lst, void (*del)(void *))

ft_lstclear : listeden bir dizi eleman siler
void ft_lstclear(t_listlst, void (*del)(void *))

ft_lstiter : listenin tüm elemanlarını (f) fonksiyonuna tâbi tutar ve döndürür
void ft_lstiter(t_list *lst, void (*f)(void *))

listenin tüm elemanlarını önce buffera atar, onu (f) fonksiyonuna tutar ve döndürür
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
```

- 42nin ilk projesi olan libft’de glibc kütüphanesindeki klasik bazi fonksiyonlari (60’a yakın) C dilinde kendimiz tekrar yaziyoruz. bunun için libft isimli bir kütüphane yaratip fonksiyonları bu kütüphanede biriktirmemiz gerekiyor. C’de kendi kütüphanemizi yazmak için yapmamız gerekenler
    - bir klasörde .h uzantılı bir dosya oluşturuyoruz. içeriği
    
    ```c
    #ifndef MY_LIBRARY_H
    #define MY_LIBRARY_H
    
    # include <libraries_you_want_to_include.h>
    
    /* add prototypes of the functions you'll use within this library 
    
    int ft_strlen(char *str);
    void ft_error(int errno);
    char *strrev(char *str);
    
    */
    
    #endif
    ```
    
    - daha sonra .c uzantılı dosyalarda #include “my_library.h” diyerek kullanabilirsin
    - .c’lerde başında static koymadığın tüm fonksiyonların prototiplerini .h’a dahil etmek zorundasın.
    - bu kütüphaneyi kullanmak için my_library.h kullandıgın tüm dosyaları **`cc main.c deneme1.c deneme2.c`** diyerek beraber derlemelisin (ya da makefile kullanmalısın)

### POINTERS

- bilgisayarda bir değişken tanımladığın zaman bu değişkenin bilgisayarın beyninde 2 hali vardır: [1] sağ değer [2] sol değer (L/R-value). sol değer bu değişkenin tutulduğu adres, sağ değer ise değişkenin türü neyse o türden değeridir. mesela

```c
int a = 30;
```

- kod yazarken kullandığımız değişkenler bilgisayarda RAM denen geçici hafızada tutulur. bu RAM milyonlarca küçük hücreden oluşuyor gibi düşünülebilir. bu hücrelerin her biri 8, 32, 64… bit olabilir. yani her bir hücre maksimum 32 ya da 64 bit veri tutuyor. atadığımız verileri unutmamak için bilgisayar bilgileri bu hücrelere kaydeder. mesela standart mimaride bir **`int`** 4 byte yani 32 bittir. kod yazarken bir**`int a = 13;`** tanımladıgımız vakit bilgisayar 32 tane art arda küçük hücreyi bu bilgiyi saklamaya ayırır. daha sonra bu a değişkenine bir pointer atadığımız zaman bu pointer değişkeni ram’deki bu 32 bitlik blogun hexadecimal formatta sayısal karşılığını gösterir hale gelir. yani pointerlar tanımladığımız değişkenlerin, fonksiyonların, structların vs. ram’de saklandığı hücrelerin adresleridir.

```c
int myVal = 500;
int *myPtr = &myVal;
```

```c
printf("%p\n", myPtr); // 0x1243252 verir
```

- pointer adresleri hexadecimal türündedir ve pointer tanımlamalarında değişkenlerin pointer olduklarını göstermek için başlarına * koyarız.  * operatörünün iki görevi vardır: [1] pointer tanımlarken kullanırız [2] tanımladığımız pointerın başında kullanılırsa pointerın tuttuğu değeri alırız. buna dereferencing denir.

```c
int a = 30;
int *aPtr = &a;         // birinci görev adres alır
printf("%d\n", *aPtr);  // ikinci görev değer alır (30)
```

- bir değişkenin adresini almak istediğimiz zaman & operatörünü kullanacağız. & operatörü başına geldiği şeyin hafızadaki adresine ulaşmak için kullanılır. mesela 0x10a2500 bir adres olabilir. pointer adresleri printf( ) ile yazdırılırken %p ile yazdırılır:

```c
int main()
{
    int a = 14;

    // & ile adres yazdırmanın birinci yolu
    int *aPtr = &a;    
    printf("%p\n", aPtr);  // 0x7ffee7d4c72c

    // ikinci yolu
    printf("%p\n", &a);    // 0x7ffee7d4c72c

		// değişkenin adresine ulaşmaya çalışırken adresin adresine ulaşmadıgından emin ol
		printf("%p\n", &aPtr); // pointerın tutuldugu adres gelir, a'nın değil

    // dereferencing
    int a_value = *aPtr;
    printf("%d\n", a_value); // 14
}
```

- bit comes from binary digits.
- & operatörü * operatörünün karşıtıdır. birbirlerini götürürler

```c
int main()
{
    int a = 23;
    int *aPtr = &a;
    printf("%d\n", *&*&*aPtr);
}
```

- örnek:

```c
int main(void)
{
	int a = 500;
	int *ap = &a;
	printf("%d\n", *ap); // 500
	*ap = 300;
	printf("%d\n", *ap); // 300
}
```

- örnek:

```c
int main()
{
    int a[6];
		a[0] = 10;
    a[1] = 20;
    a[2] = 30;
    a[3] = 40;             // şu an a[] = {10, 20, 30, 40};
	printf("%d\n", *a + 3);  // 13 verir. *a ifadesi a'nın ilk elemanını gösterir (10) ve +3 ekledik.
	printf("%d\n", *(a+3));  // 40 verir. a'nın 3 eleman ötelenmiş adresteki değerini alır. 
}
```

- bir pointerın gösterdiği adresteki değeri 1 arttırmak istiyosan

```c
int main()
{
	  int a = 10;
	  int *aPtr = &a;
	  (*aPtr)++;             // birinci yol
	  *aPtr += 1;            // ikinci yol
	  *aPtr = *aPtr + 1;     // ücüncü yol
	  printf("%d\n", *aPtr); // 13
	  printf("%d\n", a);     // 13 -- ikisi aynı sey
}
```

ama şöyle olsaydı aynı sey olmazdı: 

```c
// (*aPtr)++ yerine
// *aPtr++ deseydik
printf("%d\n", *aPtr); // 32424234
```

ifadesi artık dereference için kullanılamazdı. her cagrılısında random deger verirdi cünkü direkt *aPtr++ yazarsan aPtr’nin adresini tuttugu degeri 1 arttirmaz, direkt aPtr’nin adresini arttırır ve hafızada o +1 değerli adreste o an ne varsa onu yazdırmaya calısır. bunun altta yatan sebebi de ++ operatörünün önceliğinin ( )’den düşük olmasıdır.

- iki pointer arası adres atayabilirsin:

```c
int a=10, b=20;
int *aPtr=&a, *bPtr=&b;
aPtr = bPtr;
printf("%d\n", *aPtr); // 20
```

- birden fazla pointer türü vardır
    - int pointer: integer adresi tutan pointerlar
    
    ```c
    int a = 10;
    int *aPtr = &a;
    ```
    
    int pointerlar aynı zamanda array olarak da kullanılabilirler { } operatörüyle: 
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    int	main(void)
    {
    	int	*arr;
    
    	arr = malloc(sizeof(int) * 5);
    	if (!arr)
    		return (0);
    	for (int i = 0; i < 5; i++)
    		arr[i] = i;
    }
    ```
    
    işin kötü tarafı pointerlarla tanımladıgın bir arrayi tek seferde ilklendiremiyorsun: 
    
    ```c
    int ar3[] = {10,20,300};
    printf("%d\n", ar3[2]); // bu çalışır ve 300 verir
    
    int *ar = {10, 20, 300};
    printf("%d\n", ar[2]); // hata verir
    
    int *ar2 = malloc(sizeof(int) * 3);
    ar2 = {10,20,300};
    printf("%d\n", ar2[2]); // yine hata verir
    
    ```
    
    ```c
    // birinci yol
    int *arr = malloc(sizeof(int) * 3);
    int arr2[] = {10,20,300};
    memcpy(arr, arr2, sizeof(arr2));
    
    // ikinci yol
    int *arr = malloc(sizeof(int) * 3);
    int arr2[] = {10,20,300};
    for (int i = 0; i < 3; i++)
    	arr[i] = arr2[i];
    
    // üçüncü yol
    int *arr = malloc(sizeof(int) * 3);
    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 300;
    
    ```
    
    - char pointer: char array’leri oluşturmak için kullanılır
    
    ```c
    char *a = "bugra";
    ```
    
    char pointerlar arrayde her biri char türünde olan hafıza bloğunun başlangıç adreslerini tutarlar. yani c’de **`string`** diye bir şey yok, her elemanı charlardan oluşan char dizileri - **`s[]`** ya da **`*s`** vacr. birincisi bir char array, ikincisi char pointer yaratır. kullanımları benzerdir. C’de string yaratmanın bazı yolları 
    
    ```c
    // 1) string literal kullanarak
    char *s = "bugra";
    
    // 2) karakter dizisi + null kullanarak (null önemli)
    // bir ayrıntı burada *s kullanamiyosun çünkü that's not how to initialize ptr arrays
    char s[] = {'b','u','g','r','a','\0'};     // hata vermez
    char *s = {'b', 'u', 'g', 'r', 'a', '\0'}; // hata verir (malloclasan da verir)
    // ama alt alta yapabilirsin
    char *s = malloc(5);
    s[0] = 'a';
    s[1] = 'l';
    s[2] = 'i';
    s[3] = '\0'; // hata vermez
     
    // 3) strcpy kullanarak
    char str1[] = "Hello, World!";
    char str2[13];
    strcpy(str2, str1);
    
    // 4) [] kullanarak
    char s[] = "bugrahan";
    // eğer ilk başta ilklendirmek istemiyosan boyut vermek zorundasın. 
    // ilklendirmek yarattıktan sonra değer vermek demektir (initialization).
    char s[5];
    s = "ali";
    
    // 5) sprintf kullanarak sayıyı str çevirme
    char str[50];
    int num = 123;
    sprintf(str, "The value of num is %d", num);
    printf("%s\n", str); 
    ```
    
    - void pointer (aka generic pointer): belli bir veri tipi olmayan pointer, her şeyle kullanılabilir.
    
    ```c
    	int main() {
        int num = 42;
        void *ptr = &num;
        
        printf("num = %d\n", *(int *)ptr);
        return 0;
    }
    ```
    
    peki void pointerlara neden ihtiyac duyuyoruz? bildigimiz gibi bir pointer yalnızca kendi veri tipindeki bir baska degiskenin adresine point edebilir. söyle diyemeyiz: 
    
    ```c
    char a = 'a';
    int *ap = &a;
    ```
    
    void pointerı dereference etmeye kalkarsan cast etmelisin 
    
    ```c
    int main(void)
    {
    	int a = 600;
    	void *ap = &a;
    	printf("%d\n", *(int *)ap); // 600
    	printf("%d\n", *ap);        // hata verir
    }
    ```
    
    mesela malloc/calloc kullanırken void pointer return etmiş oluyoruz 
    
    ```c
    int *arr = malloc(4 * 10);
    ```
    
    ayrıca void pointerların atanmadan tipleri olmadıgı icin boyutları da kesin degildir o yüzden void pointerlarla pointer aritmetigi yapamazsın.
    
    - null pointer: null atanmış pointer
    
    ```c
    int *ptr = NULL;
    ```
    
    null is defined as: `(void *)0` . burada 0’ı void pointerla castliyoruz.
    
    ```c
    int main()
    {
    	printf("%lu", sizeof(NULL));
    	return 0;
    }
    ```
    
    fakat NULL pointerı dereference etmeye calısmak seg verir: 
    
    ```c
    int main()
    {
    	int *ap = NULL;
    	printf("%p\n", ap);  // (nil)
    	printf("%d\n", *ap); // SEGMENTATION
    }
    ```
    
    - wild pointer: ilklendirilmemiş pointerlardır. haliyle garbage value tutarlar. kullanımı risklidir
    
    ```c
    int main()
    {
    	int *p; // declare an uninitialized pointer
    	// *p = 5; // eğer bu olmazsa 0, olursa 5 yazdırır.
    
    	printf("%d\n", *p); // try to access the value of the pointer
    	return 0;
    }
    ```
    
    - dangling pointer: A dangling pointer is a pointer in computer programming that points to a memory location that has already been deallocated or freed. In other words, the pointer points to a location in memory that no longer holds the intended data, or the memory block it was pointing to has been released back to the system.
    
    ```c
    int main()
    {
    	int *p = (int *)malloc(sizeof(int)); // yer ayiriyoruz
    	*p = 42; // değer atiyoruz
    	free(p); // freeliyoruz
    	printf("%d", *p); // ulasmaya calısıyoruz fakat freeledik. *p artık bir dangling pointer
    }
    ```
    
    - complex pointer: kompleks bir veri tipini gösteren pointer türüdür. mesela bir struct ya da struct dizisi.
    
    ```c
    struct Kişi
    {
    	char isim[50];
    	int yas;
    };
    
    int main()
    {
    	struct Kişi kişiler[3] = {{"bugra", 10}, {"cemre", 20}, {"ugur", 30}};
    	struct Kişi *structPtr = kişiler;	 // create a complex pointer that points to the kişiler array
    	printf("%s is %d yo.\n", structPtr->isim, structPtr->yas); // bugra is 10 yo.
    	structPtr++;
    	printf("%s is %d yo.\n", structPtr->isim, structPtr->yas); // cemre is 20 yo.
    	structPtr++;
    	printf("%s is %d yo.\n", structPtr->isim, structPtr->yas); // ugur is 30 yo.
    }
    ```
    
    - double-pointer: in C, a double pointer (or a pointer to a pointer or 2D pointer) is a variable that stores the address of another pointer variable. It is denoted by the symbol **`**`**. Double pointers are often used when we want to modify the value of a pointer variable from within a function, or when we want to create a dynamically allocated two-dimensional array.
    
    ```c
    void fun(int **aa)
    {
    	**aa = 123;
    }
    
    int main()
    {
    	int a = 500;
    	int *ap = &a;
    	int **app = &ap;
    	printf("%d\n", *ap);    // 500
    	fun(app);
    	printf("%d\n", **app);  // 123
    }
    ```
    
- bir char dizisi tanımladıktan sonra (**`char *arr`**) artık o arrayin adı (**`arr`**) pointer’ının sembolü yerine geçer. örnek:

```c
int	main(void)
{
	char *a = "bugra";
	printf("%c\n", *(a));     // b
	printf("%c\n", *(a + 3)); // r
	printf("%c\n", *a + 2);   // d
} 
```

bu blogu pointer aritmetiğiyle modifiye edebilirsin: 

```c
int main()
{
    char *str = "bugra";
    str++;
    str++;
    printf("%s", str);  
}
```

- **`[]`** esasında bir pointer operatörüdür. arrayler’de [ ]’ler adresteki değere gitmek için kullanılır ve array indeksleri 0’la başlar.

```c
array[] = {3, 5, -10, 20, 150};
a[3] // 20;
```

[ ] içine yazdığın sayı kadar diziye öteleme işlemi uygular. mesela arr[3] demek *(arr + 3) demektir. o yüzden şu ikisi aynı şeydir: 

```c
char *a = "bugrahan";
printf("%c\n", a[2]); // g
printf("%c\n", 2[a]); // g
```

bir array çok boyutlu (yani matris) de olabilir: 

```c
array[][] = {{1, 2, 3}, {10, 20, 30}, {40, 50, 60}};
array[2][0] // 40
```

- `call by reference` vs. `call by value`:

```c
void fun1(int a)
{
	a++;
}

void fun2(int *a)
{
	(*a)++;
}

int main()
{
	int num = 10;
	fun1(num);
	fun1(num);
	fun1(num);
	printf("%d\n", num); // yine 10 verdi, 13 değil. bunun sebebi
	// call by reference değil value uygulamıs olmamız. fun1() fonksiyonunda
	// parametrenin adresindeki değeriyle değil kopyasıyla islem yapiyor.
	fun2(&num);
	fun2(&num);
	fun2(&num); // bu fonksiyon ise arttırır çünkü call by reference.
	printf("%d\n", num); // 13
}
```

bunun sebebi fun1()’de fonksiyon parametre olarak değişkenin kopyasını gönderiyoruz haliyle fonksiyonda yalnızca bu kopya değer arttırılıyor, adresindeki değerine bir şey yapmıyoruz. *n ve &n ile kullandığımzda ise adresteki değeri arttirdiği için fonksiyon scopu bitse de değişken arttırılmış oluyor.

- gcc ile derledikten sonra default olarak a.out dosyası oluşur (windows’ta a.exe). kendin isim vermek istiyorsan → gcc deneme.c -o run dersen run ismini verir a.out’a. bunu calistirmak icin de ./run demelisin.

### CASTING

- iki tip cast etme vardır
    - implicit: when data type is converted automatically by the C program:
    
    ```c
    int a = 98;
    printf("%c", a); // b 
    ```
    
    %c dediğimiz için otomatik olarak derleyici veri tipini char’a uyarladı ve char karşılığını verdi
    
    - explicit (aka typecasting): kendimiz değiştiriyoruz:
    
    ```c
    int a = 98;
    printf("%c", (char)a);
    ```
    
- bir fonksiyonda void olarak gelen parametreyi kullanabilmek için typecast etmelisin:

```c
int myFun(void *src, char *dst)
{
	src = (char *)src;
}
```

### STRUCTURES

- C structures are special, large variables which contain several named variables inside. The most basic example of structures are points, which are a single entity that contains two variables - x and y. Let's define a structure:

```c
struct		myStruct
{
	int		age;
	char	*name;
	float	salary;
};

int	main(void)
{
	struct myStruct	ben;

	ben.age = 10;
	ben.name = "bugra";
	ben.salary = 128.500;
	printf("%d\n", ben.age);      // 10
	printf("%s\n", ben.name);     // bugra
	printf("%.3f\n", ben.salary); // 128.500
}
```

```c
ben.name = "bugra";
strcpy(ben.name, "bugra");
```

- Typedefs allow us to define types with a different name - which can come in handy when dealing with structs and pointers. In this case, we'd want to get rid of the long definition of a point structure. typedef’li kullanırsan her seferinde **`struct myStruct ben;`** yerine **`ms ben;`** demen yeterli olur:

```c
typedef struct myStruct
{
	int		age;
	char	*name;
	float	salary;
} ms;

int main() {
	ms ben;
	ben.age = ---;
	ben.name = ---;
	ben.salary = ---;
}
```

- hem **`->`** hem **`.`** operatörü structın değerlerini atamak ya da almak için kullanılır ama aralarındaki fark şudur: eğer struct yapısını pointer şeklinde kurduysan -> kullanmalısın, normal kurduysan . kullanmalısın. structın içindeki elemanların pointer olmasıyla/olmamasıyla değil structı instantiaze ederken pointer mı kullandın normal mi yarattinla alakasi var:

```c
struct Node
{
    int age;
    char *name;
};

// -> kullanımı
int main()
{
    struct Node *ben = malloc(sizeof(struct Node));
    ben->age = 21;
    ben->name = "bugrahan";
    printf("%d\n", ben->age);
    printf("%s\n", ben->name);
} 

// . kullanımı
int main() {
    struct Node ben;
    ben.age = 21;
    ben.name = "bugrahan";
    printf("%d\n", ben.age);
    printf("%s\n", ben.name);
}
```

### DYNAMIC MEMORY ALLOCATION

- Dynamic allocation of memory is a very important subject in C. It allows building complex data structures such as linked lists. Allocating memory dynamically helps us to store data without initially knowing the size of the data in the time we wrote the program. To allocate a chunk of memory dynamically, we need to have a pointer ready to store the location of the newly allocated memory. We can access memory that was allocated to us using that same pointer, and we can use that pointer to free the memory again, once we have finished using it. örneğin şöyle bi yapımız olsun:

```c
typedef struct
{
    char *name;
    int age;
} person;

/* to allocate a new person in the myperson argument,
    we use the following syntax : */

int main()
{
    person *myperson = (person *)malloc(sizeof(person));
    myperson->name = "bugra";
    myperson->age = 21;
    printf("%s is %d years old.\n", myperson->name, myperson->age);
    free(myperson);
}
```

This tells the compiler that we want to dynamically allocate just enough memory to hold a person struct in memory and then return a pointer of type person to the newly allocated data. The memory allocation function malloc() reserves the specified memory space. In this case, this is the size of person in bytes. The reason we write (person *) before the call to malloc() is that malloc() returns a "void pointer," which is a pointer that doesn't have a type.Writing (person *) in front of it is called typecasting, and changes the type of the pointer returned from malloc() to be person.  we can assess its elements with -> operator.

- örnek2:

```c
str2 = (char *)malloc(sizeof(char) * str.len);
if (!str2)
	return 0;
```

yani malloc() fonksiyonu **`yeri_ayrilacak_degisken = (return_türü)malloc(ne_kadar_yer);`** olarak kullanılıyor. return_türü ifadesini yazmak zorunda değilsin. eski nesil c derleyicilerinde malloc char* döndürüyordu, o yüzden bir daha castlemek gerekiyordu, mallocun soluna cast yazma adeti oradan geliyor. ama daha sonraları malloc() void pointer döndürecek şekilde yeniden yazıldı ve buna gerek kalmadı ama hala by convention kullanılıyor.

- c yazarken herr malloc() kullanımı sonrasında 2 şeyi kontrol etmelisin
    - yer açılamamışsa return etmelisin
    
    ```c
    str = malloc(----);
    if (!str)
    	return 0;
    ```
    
    - açtığın şeyi free()’lemelisin
    
    ```c
    {
    	str = malloc(----);
    	----
    	----
    	----
    	free(str);
    	return 0;
    }
    ```
    
- malloc’u ve malloc kontrolünü tek satırda halledebilirsin:

```c
if (!(str = malloc(sizeof(char) * 10)));
	return 0;
```

- malloc’tan önceki kısmı yazmasan da olur

```c
// ikisi aynı şeydir
char *a = (char *)malloc(10);
char *a = malloc(10);
```

### MAKEFILE

- libft’de çok sayıda .c kullandığımız için make ile derliyoruz. make işletim sistemlerinde kaynak kodları tek seferde ve çoklu derlemeye yarayan bir metot. bu metodun unix/mac’te en çok kullanılan örneği ise Makefile. Cmake, Ninja vs. gibi farklı teknikler de mevcut.
- libft projesi çıktı olarak bir a.out dosyası değil arşiv dosyası istiyor. bir arşiv dosyası birden fazla dosyanın tek bir dosyada birleştirilmiş halidir, mesela 3 tane obje dosyasını

```cpp
ar rcs myArc.a file.o file1.o file2.o
```

şeklinde bir arşiv dosyasında birleştirebilirsin. libft’de de bütün .c dosyalarının obje hallerini libft.a’da birleştiriyoruz ve daha sonra kullanmak istersek **`gcc libft.a main.c`** şeklinde kullanıyoruz.

- libft’de kullandığımız makefile:

```makefile
# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile                                           :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: bkaramol <bkaramol@42istanbul.42.fr>          +#+  +:+       +#+      #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2022/07/05 04:01:36 by bkaramol          #+#    #+#              #
#    Updated: 2022/07/16 19:59:39 by bkaramol         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

# 	makefile tekniği çok sayıda kodu kolayca derleyip debug etmeye yarar.
# 	yani tek tek gcc *.c yazmamıza gerek kalmıyor. gcc'nin çalışma mantığı
# 		1) preprocessing (standart çıktı) [gcc -E]
# 			*	yorumları siler
# 			*	makroları açar
# 			*	.h uzantılı kütüphaneleri import eder
# 				bunun için direkt olarak kütüphaneyi kopyalar
# 				koda yapıştırıp çalıştırır
# 		2) compiling (derleme) [gcc -S]
# 			*	assembly koduna çevirir
# 			*	böylelikle asd.s (assembly uzantısı) oluşur
# 		3) assembly (bir araya getirme) [gcc -c]
# 			*	assembly kodu makina diline (0-1) çevrilir
# 			*	böylece .o uzantılı object dosyaları oluşur
# 				bu dosyalar makine diline en yakın aşamadır
# 		4) linking (bağlama)
# 			*	nesne kodları çalıştırılabilir bir dosyaya linklenir
# 			*	bu işlemin sonucunda nihai çalıştırılabilir dosya
# 				elde edilir (.exe ya da .out veya uzantısız)

# extension aramaya vsc'de ext:s,c,o vs. yazarsan o uzantıyla ilgili
# paketler gelir
# değişkenleri yazarken $() içine yazıyoruz
# make ... demek ... komutunu çalıştır demek
# direkt make yazarsan ilk komutu çalıştırır

# burada kaynak kodlarımızı listeliyoruz
SRCS			=	ft_atoi.c ft_bzero.c ft_calloc.c ft_isalnum.c ft_isalpha.c ft_isascii.c \
					ft_isdigit.c ft_isprint.c ft_itoa.c ft_memchr.c ft_memcmp.c ft_memcpy.c \
					ft_memmove.c ft_memset.c ft_putchar_fd.c ft_putendl_fd.c ft_putnbr_fd.c \
					ft_putstr_fd.c ft_split.c ft_strchr.c ft_strdup.c ft_striteri.c ft_strjoin.c \
					ft_strlcat.c ft_strlcpy.c ft_strlen.c ft_strmapi.c ft_strncmp.c ft_strnstr.c \
					ft_strrchr.c ft_strtrim.c ft_substr.c ft_tolower.c ft_toupper.c

# bu komut ile .c uzantılıları .o uzantıya çeviriyoruz
# .o(bject) dosyası ne demek? makine dili ile C dili arasındaki levelde bir dosya
# türüdür. derleyici, ingilizce kelimelerle yazılan kodu 0-1 diline çevirmeden önce
# bu dosyalara dönüştürür
OBJS			= $(SRCS:.c=.o)

# bonusları ekliyoruz
BONUS			=	ft_lstadd_back.c ft_lstadd_front.c ft_lstclear.c \
					ft_lstdelone.c ft_lstiter.c ft_lstlast.c \
					ft_lstmap.c ft_lstnew.c ft_lstsize.c
					
# bonusları .o'ya dönüştürüyoruz
BONUS_OBJS		= $(BONUS:.c=.o)

# değişkenler ekliyoruz
CC				= gcc

# make fclean dediğimizde rm -f komutunu kullanacak
RM				= rm -f

# otomatik olarak bu flaglerle derlemesini istiyoruz
CFLAGS			= -Wall -Wextra -Werror -I.

NAME			= libft.a

# iki noktadan önce yazdıkların kuraldır
# yanına yazdıkların kuralın bağımlı olacağı şeydir (dependencies)
# kuralın kendisini işlemeden bu yanına yazdığın komutları çalıştırır
# altına indented yazdıkların da o kuralı gerçekleştirecek komutlardır
# kural: bağımlılıklar
#	 komutlar
# komutlar sonucu kural oluşur, kuralın oluşabilmesi için nesneye ihtiyaç var
# makefile soldan sağa ve yukarıdan aşağıya çalışır. sıralamalar önemlidir

# all -> tüm kuralları çalıştıran kök kural
# burada neden direkt ar rcs komutunu all'ın altında yazmadık?
# çünkü biz en sonda $name isimli bir dosya oluşsun istiyoruz ki relink olmasın
# yani her make dendiginde makefile tekrar tekrar çalışmasın. bunun için ana kuralın
# çıktısı isminde bir dosya olmalı, bunu da all'ı dolaylı yazarak sağlıyoruz
# bir makefile'ın relink yapmamasını sağlayan iki şey var
# bir üreteceği dosya adında bir dosyanın hali hazırda var olması
# iki bu dosyanın içeriğinin değişmemiş olması
all:			$(NAME)

# başlarındaki $ onların değişken olduğunu söylüyor
# ar means archive. yoksa oluşturuyor.
# r --> replace the content in the archive
# c --> create a new archive
# s --> Write an object-file index into the archive
# NAME'e bağımlılık olarak OBJS vermeseydik dosyalarda yapılan
# güncellemeler sonrası tekrar makeleyemezdik, libft.a'yı silmemiz gerekirdi
$(NAME): $(OBJS)
				ar rcs $(NAME) $(OBJS)

# make clean: derleme sonrası oluşan ara dosyaları siler
clean:
				$(RM) $(OBJS) $(BONUS_OBJS)

# make fclean: derleme sonrası oluşan tüm dosyaları siler (fullclean)
fclean:	clean
				$(RM) $(NAME)

# make re: kütüphaneyi yeniden çalıştırır. önce fclean ile
# her şeyi siler sonra all ile yeniden yapar
re:			fclean all

bonus:	$(OBJS) $(BONUS_OBJS)
				ar rcs $(NAME) $(OBJS) $(BONUS_OBJS)

# C clean kuralını çalıştırmak istesin. aynı adda bir başka klasör ya da dosya varsa
# ona gitmesin kural olan clean'i anlasın diye bunu yazıyoruz. mesela clean diye bi dosyan
# olsun. make clean dediğinde .o noktalarını silme işlemi değil clean'ı derleme işlemi yapacaktır
# eğer .phony'ye clean ismini dahil etmezsen. .gitignore gibi düşünebilirsin
.PHONY:			all clean fclean re bonus
```

derledikten sonra her .c’nin .o’su + olarak da libft.a çıkacaktır. birden fazla dosyanın kullanıldığı bir dosyayı kısaca derlemek için **`dosya.c libft.a`** diyebilirsin. burada derleme işlemini yaparken cc ya da gcc değil ar rcs yani arşiv oluşturma metodunu kullanıyoruz çünkü libt’de main( ) fonksiyonu yok o yüzden derleyip executable program oluşturmaya çalışmak hata verir. 

### LINKED LIST

- linked list yani bağlı listeler bir veri yapısı türüdür. içerlerinde farklı türden verileri tutmaya yararlar. peki listeler nasıl çalışıyor? listeler arrayler gibi hafızada sıralı hücrelerde değil dağınık hücrelerde tutuluyor. her hücre hem bir veriyi hem sonraki hücrenin bilgisini saklıyor.
    
    
    - each element of a list contains
        - A Data Item (we can store integer, strings, or any type of data).
        - Pointer (Or Reference) to the next node (connects one node to another) or An address of another node
        
    
    ![Screenshot from 2022-12-13 19-53-57.png](1%20-%20libft%20notlar%C4%B1%2013817f06ff7543c3b95c2efb36a1d0d5/Screenshot_from_2022-12-13_19-53-57.png)
    
    listelerin avantajı kolaylıkla veri eklenip çıkartılması. hatta ileri düzey listelerde birden fazla listeyi birbirine bağlayabiliyorlar. dezavanyaji ise access time’ı biraz uzun çünkü location (indis) kesin değil arraylerin aksine. o yüzden arraylerde spesifik bir elemana ulaşmak hem daha kolay hem daha kısa sürüyor.
    
- liste türleri
    - singly linked list: her eleman bir sonrakini gösteriyor son eleman null’u gösteriyor. libft bonusunda bu tip listeleri kullanıyoruz. işlem olaraksa baştan ekleme sondan çıkarma vs. gibi klasik liste problemleri çözmemiz isteniyor.
    
    ```c
    // SLL structımız. birincisi data, ikincisi bir sonraki node'u işaret eden pointer
    struct			Node
    {
    	int			data;
    	struct Node	*next;
    };
    
    // listeye yeni node ekleyecek fonksiyon
    void	push(struct Node **head, int new_data)
    {
    	struct Node	*new_node;
    
    	// yeni node için yer ayiriyor
    	new_node = malloc(sizeof(struct Node));
    	// yeni node'un datasını parametre olarak verilecek sey yapiyor
    	new_node->data = new_data;
    	// yeni_node'un nextini listenin o anki head'i yani başlangıcı yapiyor cünkü yeni node baştan eklenecek
    	new_node->next = (*head);
    	// update the head pointer to point to the new node
    	(*head) = new_node;
    }
    
    void	print_list(struct Node *node)
    {
    	while (node)
    	{
    		printf("[%d]", node->data);
    		node = node->next;
    	}
    }
    
    int	main(void)
    {
    	struct Node	*head;
    
    	head = NULL;
    	push(&head, 10);
    	push(&head, 15);
    	push(&head, 20);
    	print_list(head);
    }
    ```
    
    - doubly linked list: her eleman bir sonrakini ve bir öncekini gösteriyor son eleman null’u ve bir öncekini gösteriyor.
    
    ```c
    struct Node {
        int data;
        struct Node* prev;
        struct Node* next;
    };
    
    // Function to add a new node to the front of the list
    void push(struct Node** head_ref, int new_data) {
        // Allocate memory for the new node
        struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    
        // Set the data and pointers for the new node
        new_node->data = new_data;
        new_node->prev = NULL;
        new_node->next = (*head_ref);
    
        // Update the previous pointer of the current head node
        if ((*head_ref) != NULL) {
            (*head_ref)->prev = new_node;
        }
    
        // Update the head pointer to point to the new node
        (*head_ref) = new_node;
    }
    ```
    
    - circular linked list: her eleman bir sonrakini gösteriyor son eleman ilk elemanı gösteriyor.

---

- **`memchr`** vs. **`strchr`** farkı: memchr() fonksiyonu strchr()’ye göre fazladan bir uzunluk parametresi alır ve aramasını o parametre kadar yapar. bunun sebebi strchr’ye kesin olarak string göndermemiz, memchr’ye ise herhangi bir tipte veri gönderebilmemiz. stringlerin sonunda null oldugu kesindir, o yüzden null görene kadar koşuluyla overflow riskini aşabiliriz ama mem’lerde string verilecegi kesin olmadıgından bir arama limiti dışarıdan verilmelidir.
- **`strcpy`** vs. **`memcpy`** farkı: strcpy’de sadece string kopyalayabilirsin. memcpy ise void pointer kullandıgından direkt hafıza alanını kopyaladığı için üzerindeki datanın tipinin bir önemi yoktur. strcpy null görene kadar kopyaladığı için bir byte limiti verme zorunluluğu yoktur. memcpy’de ise sadece string değil int de kopyalayabiliriz ama onun sonunda null yok. bu durumda memcpy’ye kopyalanacak byte sayısı önceden verilmelidir. bir üsttekiyle aynı olay.
- **`memmove`** vs. **`memcpy`** farkı: With memmove, the destination cannot overlap the source at all. With memcpy it can.
    
    ![Screenshot from 2022-12-24 02-37-44.png](1%20-%20libft%20notlar%C4%B1%2013817f06ff7543c3b95c2efb36a1d0d5/Screenshot_from_2022-12-24_02-37-44.png)
    
    Unless you know for sure that `src` and `dst` don't overlap, call `memmove` as it will always lead to correct results and is usually as fast as that is possible for the copy case you require. 
    
    ```c
    void memmove ( void * dst, const void * src, size_t count ) {
        if ((uintptr_t)src < (uintptr_t)dst) {
            // Copy from back to front
    
        } else if ((uintptr_t)dst < (uintptr_t)src) {
            // Copy from front to back
        }
    }
    
    void mempy ( void * dst, const void * src, size_t count ) {
        if ((uintptr_t)src != (uintptr_t)dst) {
            // Copy in any way you want
        }
    }
    ```
    
    If you know for sure that `src` and `dst` don't overlap, call `memcpy` as it won't matter which one you call for the result, both will work correctly in that case, but `memmove` will never be faster than `memcpy` and if you are unlucky, it may even be slower, so you can only win calling `memcpy`. 
    
    ```c
    int main(void)
    {
        char s1[] = "123456789abcd";
        char *s2, *s3;
        s2 = s1;
        s3 = s1;
    
        printf("initially s1:  %s\n", s1); // "123456789abcd"
        memcpy(s2 + 5, s2, 7);
        printf("memcopied: s2: %s\n", s2); // "123451234567d"
        memmove(s3 + 5, s3, 7);
        printf("memmoved s3:   %s\n", s3); // "123451234512d"
        return 0;
    }
    ```
    
    diğer bir deyişle: şöyle bir kodumuz olsun 
    
    ```dart
    char str[] = "bugrahan";
    memcpy(&str[3], &str[4], 4); // it might blow up
    ```
    
    çünkü dest, src’den sonra çakışıyor. memmove burada sorun çıkarmaz. aralarındaki temel fark memmove’un bir buffer yani geçici bellek kullanmasıdır bu nedenle üst üste binme riski yoktur. mesela 
    
    ```c
    int main (void)
    {
        char string [] = "stackoverflow";
        char *first, *second;
        first = string;
        second = string;
    
        puts(string);
        memcpy(first+5, first, 5);
        puts(first);
        memmove(second+5, second, 5);
        puts(second);
    }
    ```
    
    fakat kod şöyle olsaydı 
    
    ```dart
    int main (void)
    {
        char string [] = "stackoverflow";
        char *third, *fourth;
        third = string;
        fourth = string;
    
        puts(string);
        memcpy(third+5, third, 7);
        puts(third);
        memmove(fourth+5, fourth, 7);
        puts(fourth);
    }
    ```
    
    olarak gelir. çünkü memcpy sırasıyla şöyle yapar: 
    
    ```c
    1.  stackoverflow
    2.  stacksverflow
    3.  stacksterflow
    4.  stackstarflow
    5.  stackstacflow
    6.  stackstacklow
    7.  stackstacksow
    8.  stackstackstw
    ```
    

### **FILE DESCRIPTORS**

- In C, you can perform four major operations on files, either text or binary:
    1. Creating a new file
    2. Opening an existing file
    3. Closing a file
    4. Reading from and writing information to a file
- A file descriptor is a positive number that uniquely identifies an open file in a computer's operating system. The descriptor is identified by a unique non-negative integer, such as 0, 12, or 567. At least one file descriptor exists for every open file on the system. File descriptors were first used in Unix, and are used by modern operating systems including Linux, macOS, and BSD. In Microsoft Windows, file descriptors are known as file handles. ilk 3 FD default olarak şunlardır:
    - 0 - standard input (stdin): The default data stream for input, for example in a command pipeline. In the terminal, this defaults to keyboard input from the user.
    - 1 - standard output (stdout): The default data stream for output, for example when a command prints text. In the terminal, this defaults to the user's screen.
    
    ```c
    int	main(void)
    {
    	write(1, "ali\n", 4);
    }
    ```
    
    - 2 - standard error: The default data stream for output that relates to an error occurring. In the terminal, this defaults to the user's screen.
- dosyalarla ilgili yaptığın işlemlerin çoğu **`fcntl.h`** kütüphanesini kullanır.
- bir dosya açmak istediğinde çekirdek önce
    - o dosyaya erişim iznini kontrol eder. varsa
    - global file table’da bir entry yaratır
    - programa açması için dosyanın konumunu gönderir
- bazı I/O fonksiyonları:
    - **`int open(char *path, int flags)`** open fonksiyonu eğer varsa path isimli dosyayı açar, yoksa flagler yardımıyla oluşturur. return olarak açtığı dosyanın fd’sini döndürür dolayısıyla bir dosyanın file descriptorini almaya yarar.
    
    ```c
    int main() {
    	int my_fd = open("abc.txt", O_RDWR);
    }
    ```
    
    - **`ssize_t read(int fd, char* buf, size_t sz)`** Read data upto count bytes from a file whose file descriptor is fd and store the results in buf pointer. It returns the number of bytes read. In case of any error, it returns -1.
    
    ```c
    int main()
    {
        int fd = open("asd.txt", O_RDWR);
        char *c = (char *)malloc(1000);
        int chk = read(fd, c, 1000);
        printf("%s\n", c);
    }  // content of asd.txt
    ```
    
    open() ile asd.txt dosyasının fd’sini öğrendik. bunu daha sonra read() fonksiyonunda kullanarak asd.txt’ten c stringine okuma yapmada kullandık.
    
    - **`ssize_t write(int fd, const char* buf, size_t sz)`** write fonksiyonu buf char stringinden fd id’li dosyaya sz byte kadar okuma yapar. Normally, write returns sz, but as with read, it might return less. bunlara short read/write denir.
    
    ```c
    void	ft_putchar_fd(char c,  int fd)
    {
    	write(fd, &c, 1);
    }
    
    void ft_putstr_fd(char *s, int fd)
    {
    	write(fd, s, strlen(s));
    }
    
    int main()
    {
        int x = open("bugra.txt", O_CREAT | O_RDWR);
        ft_putchar_fd('s', x);
        ft_putchar_fd('\n', x);
    		ft_putstr_fd("bugra kara", x);
    }
    ```
    
    burada bugra.txt dosyasına s charını yazdırdık. eğer x yerine 0, 1, 2 kullansaydık terminale yazdırırdı. her ne kadar 0 input, 1 output 2 error yazdırma için kullanılıyor diye bilsek de 
    
    ```c
    #include <unistd.h>
    
    int main()
    {
    	write(0, "Hello, world!\n", 14); // Hello, world!
    	write(1, "Hello, world!\n", 14); // Hello, world!
    	write(2, "Hello, world!\n", 14); // Hello, world!
    	return 0;
    }
    ```
    
    her üç şekilde de ekrana yazdiriyor ama yine de her birini doğru fd ile kullanmak daha doğru.
    
    - **`int close(int fd)`**fd id’li dosyayı kapatır.
    
    ```c
    int main()
    {
    	close(fd);
    }
    ```
    
    - **`int creat(char *filename, mode_t mode):`** filename konumunda mode izinleriyle dosya yaratır. it returns the file descriptor that points to that file in the file table entry. In case of any error, it returns -1.
    
    ```c
    int new_file = creat("asd.txt",0600);
    ```
    
    bazı flagler: 
    
    | O_RDONLY | read only |
    | --- | --- |
    | O_WRONLY | write only |
    | O_RDWR | read and write |
    | O_CREAT | create file if it doesn’t exist |
    | O_EXCL | prevent creation if it already exists |
    | __O_LARGEFILE | used for opening large files(>1GB) |
    | O_TRUNC | Truncate the contents of the file, if the file already exists |
- **`file descriptor`** vs. **`file pointer`** farkı: A file descriptor is a low-level integer "handle" used to identify an opened file (or socket, or whatever) at the kernel level, in Linux and other Unix-like systems. You pass "naked" file descriptors to actual Unix calls, such as read(), write() and so on. A FILE pointer is a C standard library-level construct, used to represent a file. The FILE wraps the file descriptor, and adds buffering and other features to make I/O easier. You pass FILE pointers to standard C functions such as fread() and fwrite(). /

---