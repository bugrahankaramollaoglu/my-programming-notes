# random C/C++ notes

- array elemanlarını istediğin sırayla ilklendirebilirsin

```c
int main() {
  int arr[5] = {[3] = 4, [2] = 3};
  print(arr);
}
```

you can also use this technique within ranges  

```c
 int main() {
  int arr[10] = {[0 ... 3] = 4, [6] = 3};
  print(arr);
} 
```

- scanf tricks:

```c
#include <stdio.h>
#include <unistd.h>

int main()
{
    // inputta \n alana kadar okumaya devam eder
    scanf("%[^\n]\n", a);

    // inputta , alana kadar okumaya devam eder
    scanf("%[^,],", a);

    // sadece abcd harflerini alir. baska girersen orada keser scanf'i
    scanf("%[abcd]s", str);

    // abcde harici her sey alir abcd girersen keser input almayi
    scanf("%[^abcd]s", str);

    // \n yazana kadar her şeyi alır (enterlasan da bitmez)
    scanf("%[^\n]s", str);

    // val'i terminalde n kadar sağa öteleyerek yazdırır
    int n = 30;
    int val = 1000;
    printf("%*d", n, val);
}
```

- oturumu kapatan c komutu

```c
#include <windows.h>

int main() {
  system("shutdown -l -f -t 00");
}
```

- pointerla tanımlanmış iki stringi kopyalamanın en kısa yolu

```c
while (*dst++ = *src++);
```

- integer’i char’a çevirmek için sprintf kullanabilirsin

```c
int main() {
  char buffer[21];
  int number = 12345;
  sprintf(buffer, "%i", number);
  printf("%s", buffer); >>> 12345
  printf("%d", number);   >>> 12345
}
```

- interesting usage of inline blocks

```c
int main() {
    printf("%d\n", ({ int n; scanf("%d", &n); n*n; }));
}
```

- C’de a[2] ile 2[a] aynı şeydir. çünkü ikisi de *(a + 2) demektir

```c
int main()
{
    char *s = "bugra";
    printf("%c", 3[s]); // same as printf("%c", s[3]);
} // r
```

- tek/çift kontrolü yaparken % yerine & kullanabilirsin

```c
int main()
{
    int x = 51;
    if (x & 1)
        printf("odd");
    else
        printf("even");
    return 0;
}
```

- aynı şekilde çarpma işlemi için de << / >> kullanabilirsin

```c
int main()
{
    int x = 51;
    printf("%d\n", x << 1); // 2yle çarpmanın kolay yolu
    printf("%d", x >> 1);   // 2ye bölmenin kolay yolu
}
```

- meşhur swap() işleminde aslında temp’e ihtiyacımız yok:

```c
int main()
{
    int x = 10;
    int y = 34;

    x ^= y;
    y ^= x;
    x ^= y;
}
```

swap etmenin bir başka yolu da asm( ) fonksiyonudur:  

- You know that the maximum size of array inside main function is 10^6 right? But if you declare it globally, you can even declare it upto 10^7.
    
    ```c
    void swap(int *a, int *b){
        asm("" : "=r" (*a), "=r" (*b) : "1" (*a), "0" (*b));
    }
    
    swap(&a, &b);
    ```
    
- sayının en sağındaki basamağa **least significant digit,** en sol basamağındaki sayıya da **most significant digit** denir. most significant digit bulma metodu:

```c
double x= log10(num); 
x= floor(x);
```

- 69’da bell laboratuvarlarinda assembler dilinde UNIX geliştirildi.
- 72’de dennis ritchie C’yi geliştirdi. bu dil B dilinin devamıydı. daha sonra 73’te UNIX C’de tekrar yazildi. unix kodu 10bin küsür satırdır.
- ANSI C, standard C ya da C89 olarak da bilinir.
- C11’le gets() ailesi çıkartılmıştır.
- basamak sayısı hesaplayan fonksiyon:

```c
#include <math.h>

int main()
{
    int x = 1035;
    int dig = floor(log10(x)) + 1;
}
```

- is_power_of_2 hesaplayan fonksiyon:

```c
int is_power_of_2(int x)
{
    return x && (!(x & (x - 1)));
}
```

- /*  */ alternatifi

```c
#if 0
your code
#endif
```

- strrev alternatifi

```c
char* reverse( char* s) 
    { 
    	size_t n = strlen(s); 
     
    	size_t i = 0; 
     
        char* rev = (char*) malloc( n * sizeof(char) ); 
      
         for(i=0; i < n; i++) 
          { 
             rev[i] = s[n-i]; 
           } 
        
        return rev; 
    }
```

- nice

```c
int main()
{
    int x = 10;
    int y = 3;
    if (x = 2) // this is punch line. this assignment actually works 
    {
        y = x * 20;
    }
    printf("x is %d\n", x); >>> 2
    printf("y is %d", y);   >>> 40
}
```

- nice2

```c
int main()
{
    char a[100] = "bugra"; // this won't work
    char *a = "bugra";     // this will work
    a = "cemre123";
    printf("%s", a);
}
```

- double ve float farkı : double’ın precision’ı float’tan iki kat daha fazla. float has 7 decimal digits of precision whereas double has 15. specifiers. `"%f"` is the (or at least one) correct format for a double. There *is* no format for a `float`, because if you attempt to pass a `float` to `printf`, it'll be promoted to `double` before `printf` receives it. double 8 byte, float 4 byte’tır. double’ın 64 bitinin dağılımı
    
    ![Screenshot from 2022-12-08 20-07-47.png](random%20C%20C++%20notes%209e3890b180bb40ccb900c7fd72a43e3a/Screenshot_from_2022-12-08_20-07-47.png)
    

| `Void` | None | None |
| --- | --- | --- |
| `_Bool` | 0 to 1 | %d |
| `Char` | –128 to 127 | %c |
| `unsigned char` | 0 to 255 | %u |
| `short int` | –32,768 to 32,767 | %d |
| `unsigned short int` | 0 to 65,535 | %u |
| `int` | –2,147,483,648 to 2,147,483,647 | %d |
| `unsigned int` | 0 to 4,294,967,295 | %u |
| `long int` | –2,147,483,648 to 2,147,483,647 | %ld |
| `unsigned long int` | 0 to 4,294,967,295 | %lu |
| `long long` | –9,223,372,036,854,775,808 to
9,223,372,036,854,775,807 | %lld |
| `unsigned long long` | 0 to 18,446,744,073,709,551,615 | %llu |
| `float` | 1.2×10–38 to 3.4×1038 | %e, %f, %g |
| `double` | 2.3×10–308 to 1.7×10308 | %e, %f, %g |
| `long double` | 3.4×10–4932 to 1.1×104932 | %e, %f, %g |

printf()’te double ya da float kullanırken %f ya da %lf kullanmanın pek bir önemi yok çünkü float’ı otomatik olarak double’a çeviriyor. fakat scanf()’te durum böyle değil. float vereceksen %f, double vereceksen %lf yazman gerekiyor.

- %d ve %i farkı : %d specifies signed decimal integer while %i specifies integer. printf()’le kullanırken hiçbir farkları yok. double ve float’ta oldugu gibi farkları scanf’te ortaya çıkıyor. %d’nin aksine %i’yi input alırken sadece decimal integer için değil octal vehexadecimal sayılarla da kullanabiliyorsun. octal’ın başına 0 hex’in başına 0x koyarsan %i bunları anlıyor ve decimale çevirip öyle yazdiriyor.

```c
int main()
{
    int a = 0, b = 0;
    printf("enter value of a :");
    scanf("%d", &a);
    printf("enter value of b :");
    scanf("%i", &b);
    printf("value of \"a\" using %%d is= %d\n", a);
    printf("value of \"b\" using %%i is= %i\n", b);
}
```

- print() ile %d yazdırmak için “%%d” yazmalısın
- switch() kullanımı

```c
int main()
{
    int num;
    printf("enter 1 2 or 3 to see its power to the third: ");
    scanf("%d", &num);
    switch (num)
    {
    case 1:
        printf("you chose %d.\n", num);
        printf("1's power to the third is: %d\n", 1);
        break;
    case 2:
        printf("you chose %d.\n", num);
        printf("2's power to the third is: %d\n", 2 * 2 * 2);
        break;
    case 3:
        printf("you chose %d.\n", num);
        printf("3's power to the third is: %d\n", 3*3*3);
        break;
    default:
        printf("yanlis girdin\n");
        break;
    }
}
```

- struct kullanıım

```c
struct Person
{
    char isim[20];
    char soyisim[300];
    int maas;
    int yaş;
};

int main()
{

    struct Person ben = {"buğra", "kara", 1000, 20};
		printf("ismi %s, soyismi %s, maaşı %d, yaşı %d", 
					ben.isim, ben.soyisim, ben.maas, ben.yaş);	
}
```

- `unsigned int` ve `size_t` farkı:  unsigned int de size_t de nonNegatif sayılarla kullanılabilir fakat aralarındaki fark şudur: size_t çok daha kapsamlıdır. unsigned char/short/int/long/long long olabilir. genelde uzunluk ve boyut belirtirken size_t kullanılması tavsiye edilir. strlen() ve sizeof() da size_t döndürür. size_t esasında yukarıdaki durumlarda kullanılan bir `alias`’tır. boyutu 8 byte’tır. `uint64_t` de 8byte unsigned integer’ın sembolüdür.`ssize_t` is used for functions whose return value could either be a valid size, or a negative value to indicate an error.
It is guaranteed to be able to store values at least in the range `[-1, SSIZE_MAX]` (`SSIZE_MAX` is system-dependent). So you should use `size_t` whenever you mean to return a size in bytes, and `ssize_t` whenever you would return either a size in bytes or a (negative) error value. printf() ile conversion’ı **`%zu`**’dur.
- call by value/reference farkı: call by value demek bir fonksiyona parametre olarak bir değişkenin değerini, call by reference demek ise parametre olarak adresini göndermek demektir. ilkinde değişkenin değeri değişmezken ikincisinde değişir

```c
// call by value
int myFun(int a);

// call by reference
int myFun(int *a);
```

- kaynak kodları windows’ta .obj’e , unix’te .o uzantıya çevrilir.
- `const char` ve `char const` farkı: The difference is that `const char *str` is a pointer to a const char, while `char * const` str is a constant pointer to a char. The first, the value being pointed to can't be changed but the pointer can be. The second, the value being pointed at can change but the pointer can't (similar to a reference). There is also a const char * const which is a constant pointer to a constant char (so nothing about it can be changed). Note: The following two forms are equivalent: const char * and char const * The exact reason for this is described in the C++ standard, but it's important to note and avoid the confusion. I know several coding standards that prefer: char const over const char (with or without pointer) so that the placement of the const element is the same as with a pointer const.
- fonksiyonların pointer göndermesi:
- -> operator in C:
- what’d be the output?

```c
int main() {
	printf("%d", write(1, "x", 1));
} >>> x 1

int main() {
	printf("%d", write(1, "abcd", 4));
} >>> x 4

```

- malloc’u kullanmanın farklı yolu

```c
char *a;

a = (char *)malloc(sizeof(char) * 256);
if(!a)
	return 0;

// ya da direkt
if (!(a = (char *)malloc(sizeof(char) * 256);
```

- Local variable value are allocated on the stack, which is cleaned once you exit the function. o yüzden asagidaki kod a'nın degerini degistiremez:

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
} >>> 5
```

degissin istiyosan 2 sey yapabilirsin

1. ya pointer kullanacaksın ki adres üzerinde dogrudan degisiklik yapilsin

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
} >>> 8
```

1. ya da local bir degisken return etmelisin

```c
int inc(int a)
{
    return (++a); // çalışıyor
    return (a+1); // çalışıyor
    return (a++); // arttırmıyor
}

int main()
{
    int x = 5;
    x = inc(x);
    x = inc(x);
    x = inc(x);
    printf("%d\n", x);
} >>> 8
```

- c kodlarında, eğer bir fonksiyonun üstüne

```c
/**
  * Komutları depolamak için kullanılacak yığınları ve dizeyi başlatır
  *
  * @param a İlk yığın.
  * @param b Sıralanan sayıları saklamak için kullanılacak yığın.
  * @param p bir karaktere bir işaretçiye işaretçi.
  * @param av Programa iletilen argümanlar.
  */
void	init(t_stack *a, t_stack *b, char **p, char **av)
```

şeklinde yazarsan, fonksiyonun üzerine geldiğinde yorum satırlarını highlight ederek gösterir

- örnek:

```c
#include <stdio.h>
int main() {
	if (!NULL)
		printf("this will work");
	else
		printf("no, this will work");
}
```

- örnek:

```c
int main()
{
    int i;
    static int count;
    for (i = NULL; i <= 5;)
    {
        count++;
        i += 2;
    }
    printf("i: %d\n", i);
    printf("count: %d\n", count);
}
```

- sonuç ne olur?

```c
int main()
{
    char *str;
    strcpy(str, "bugra");
    printf("%s", str);
    return 0;
}
```

aynı şekilde bu da segfault verir 

```c
int main()
{
	char *a = "bugrahan";
	char *b = "12345678";
	strcpy(a, b);
	printf("a: %s\n", a);
	printf("b: %s\n", b);
}
```

```c
char a[] = "bugrahan";
char *b = "12345678";
```

- bir arrayin eleman sayısını öğrenme:

```c
int a = sizeof(arr) / sizeof(arr[0]);
```

- what is the size of void pointer?
Size of any type of pointer in c is independent of data type which is pointer is pointing i.e. size of all type of pointer (near) in c is two byte either it is char pointer, double pointer, function pointer or null pointer. Void pointer is not exception of this rule and size of void pointer is also two byte.h
- pointerlarda öncelik sırası `(), [] (left to right)` > `* (right to left)` > `casting`'dir. mesela `char (*aPtr)[3]` olsun. burada öncelik sıralaması
    - aPtr
    - *
    - [3]
    - char’dır.
    
    char (*aPtr)[3] means: ptr is a pointer to the 1D array of size 3 whose content is of char data type. 
    
    float (*ptr)(int) means: ptr is a pointer to a function who takes a float and returns an int.
    
- What is difference between uninitialized pointer and null pointer?
An uninitialized pointer is a pointer which points unknown memory location while null pointer is pointer which points a null value or base address of segment.

```c
int *p;   //Uninitialized pointer
int *q= (int *)0;  //Null pointer
```

- what is memory leak?
Memory is allocated on demand—using malloc() or one of its variants—and memory is freed when it’s no longer needed. A memory leak occurs when memory is allocated but not freed when it is no longer needed. Leaks can obviously be caused by a malloc() without a corresponding free(), but leaks can also be inadvertently caused if a pointer to dynamically allocated memory is deleted, lost, or overwritten. Buffer overruns—caused by writing past the end of a block of allocated memory—frequently corrupt memory. Memory leakage is by no means unique to embedded systems, but it becomes an issue partly because targets don't have much memory in the first place and partly because they often run for long periods of time without rebooting, allowing the leaks to become a large puddle. Regardless of the root cause, memory management errors can have unexpected, even devastating effects on application and system behavior. With dwindling available memory, processes and entire systems can grind to a halt, while corrupted memory often leads to spurious crashes.
memory leak’e bakmanın 5 yolu
    1. memwatch
    2. valgrind
    3. memleax
    4. Collecting core dump
    5. linux tools

[https://www.golinuxcloud.com/how-to-find-memory-leaks/](https://www.golinuxcloud.com/how-to-find-memory-leaks/)

- how to write hello without using **`;` ?**

```c
// birinci cözüm
int main()
{
    if (printf("Hello world\n"))
    {}
}

// ikinci cözüm
int main()
{
    while (!printf("Hello world\n"))
    {}
}

// ücüncü cözüm
int main()
{
    switch (printf("Hello world\n"))
    {}
}
```

- temp kullanmadan iki integer’i swap etme:

```c
int main()
{
    int a = 5;
    int b = 12;

		// solution1
    a = a + b;
    b = a - b;
    a = a - b;

		// solution2
		a=a^b;
    b=a^b;
    a=b^a;
    printf("a:%d b:%d\n", a, b);
}
```

- pointer türleri
    - dangling pointer: If any pointer is pointing the memory address of any variable but after some variable has deleted from that memory location while pointer is still pointing such memory location. Such pointer is known as dangling pointer and this problem is known as dangling pointer problem.
    - wild pointer: pointer which has not been initialized. mesela
    
    ```c
    int main() {
    	int *ptr;
    	printf("%u\n", ptr);
    	printf("%d\n", *ptr);
    }
    ```
    
    - void pointer:
    - null pointer:
    - int pointer:
    - char pointer:
    - far pointer: The pointer which can point or access whole the residence memory of RAM i.e. which can access all 16 segments is known as far pointer.
- what lies behind **`int a = 7`** ?
    
    Memory representation of:
    
    **`signed int a=7;`**         (In Turbo c compiler)
    
    **`signed short int a=7`** (Both turbo c and Linux gcc compiler)
    
    Binary equivalent of data 7 in 16 bit is: 00000000 00000111
    
    Data bit: 0000000 00000111 (Take first 15 bit form right side)
    
    Sign bit: 0 (Take leftmost one bit)
    
    First
     eight bit of data bit from right side i.e. 00000111 will store in the 
    leftmost byte from right to left side and rest seven bit of data bit 
    i.e. 0000000 will store in rightmost byte from right to left side as 
    shown in the following figure:
    
    ![24.jpeg](random%20C%20C++%20notes%209e3890b180bb40ccb900c7fd72a43e3a/24.jpeg)
    
- C'de python'daki gibi 2 ** 3 diyerek 2'nin 3. kuvvetini alamıyosun. bunun icin math.h import edip pow() fonksiyonunu kullanabilirsin
- there are 2 kinds of loops in C:
    - counter controlled loops (definite) (i < 5)
    - sentinel controlled loops (indefinite) (-1 to quit)
- C, 0 hariç her sayıyı true kabul eder
- leak yer ayrılmış bir char stringini free’lemediginde oluyor. segfault ise erişim iznin olmayan bir yere erişmeye çalıştığında. leak’leri şöyle kontrol ediyosun

```c
system("leaks a.out");
```

     segfault’u ise lldb ile yapabilirsin  

```c
lldb ./a.out ve sonrasında r'ye basarak bakabilirsin
```

- parametre & argüman farkı: parametres are just placeholders for functions. they also indicate the type of the data. where they differ from arguments is that they do not have an actual value. for instance:

```c
int myFun(int param1, char *param2); // these are parameters
myFun(10, "bugra"); // these these are arguments
```

- şu ifade yanlıştır

```c
while (s1[i])
	s2[i++] = s1[i++];
```

```c
while (s1[i])
	s2[i++] = s1[i];
```

- örnek

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char    *str;
    int     i;
    str = malloc(sizeof(char) * 5);
    str = "ahmet";
    free(str);
}

/* İkinci yaptığın Ahmet eşitlemesi ayrı bir hafızada 
readonly bir stringe işaret ediyor yani mallocla ayırdığın 
alandan başka bir yeri işaret ediyor orası da haliyle 
free edilebilen bir yer değil. ahmet'i str'ye verdiğimizde
str'nin adresini kaybetmiş oluruz bu da memory leak'e sebep olur. */
```

- örnek:

```c
int main()
{
    int a = 2;
    printf("%ld\n", sizeof(a)); >>> 4
}
int main()
{
    int a = 2;
    printf("%ld\n", sizeof(sizeof(a))); >>> 8
}
```

- array boyutunu hesaplarken sık yapılan bir yanlış:

```c
void myFun(int *a)
{
	int size = sizeof(a) / sizeof(a[0]);
}
```

```c
sizeof(int *) / sizeof(a[0])
```

- restrain from using global variables unnecessarily. here’s why: [wiki.c2.com/?GlobalVariablesAreBad](http://wiki.c2.com/?GlobalVariablesAreBad)
- sadece dinamik yer ayırdığın bir değişkeni freeleyebilirsin:

```c
char *a = "bugra";
free(a); // saçma çünkü bugra su an read-only bir yerde saklanıyor, freeleyemezsin

char *b = malloc(10);
free(b); // freeleyebilirsin çünkü dynamically-allocated
```

- ; kullanmadan nasıl hello world yazdırırız?

```c
int main(void)
{
	if(printf("hello world")) {
	}
}
```

- what is memory leak?  Memory leak occurs when programmers create a memory in heap and forget to delete it. a function example with leak:

```c
void f()
{
    int *ptr = (int*)malloc(sizeof(int));
  
    /* Do some work */
  
    return; /* Return without freeing ptr*/
}
```

- what are static functions? What is their use? In C, functions are global by default. The “static” keyword before a function name makes it static. Unlike global functions in C, access to static functions is restricted to the file where they are declared. Therefore, when we want to restrict access to functions, we make them static. Another reason for making functions static can be reuse of the same function name in other files. yani değişkenlerin başına static koyma sebebimiz değeri kaybolmasın diye, fonksiyonların başına static koyma sebebimiz sadece o dosyada geçerli olsun diyedir.
- **`i++`** vs. **`++i`**: birincisine post ikincisine pre increment denir. birinci örnek printf’le kullanıldıgında önce i’nin o anki değerini (5) verir sonra printf bittikten sonra arttırır. ikincisi ise önce arttırır sonra printf’le yazdırır. örnek:

```c
int main()
{
    int i = 5;
    printf("%d\n", i++); >>> 5 
    printf("%d\n", i);   >>> 6 
    printf("%d\n", ++i); >>> 7
    printf("%d\n", i);   >>> 7
}
```

- what is l-value? l-value means LEFTn value. it refers to an expression that can be used on left side of assignment operator. For example in expression “a = 3”, a is l-value and 3 is r-value. 3 constant oldugu icin asla l-value olamaz. yani asla bir değeri 3’e *atayamazsın.* iki çeşit l-value vardır
    - nonmodifiable like const variables
    - modifiable
- kendi sizeof()’umuzu yazalım:

```c
#define ft_sizeof(type) (char *)(&type + 1) - (char *)(&type)
int main()
{
    int a = 32;
    printf("%ld\n", ft_sizeof(a)); >>> 4
    printf("%ld\n", sizeof(a));    >>> 4
}
```

- loop kullanmadan 1-n yazdırma? (rekürsif)

```c
void print_it(int n)
{
	if (n > 0)
	{
		print_it(n-1);
		printf("%d ", n);
	}
}
```

- ikisi aynı şeydir

```c
int main()
{
	char a[] = "bugra";
	printf("%p\n", a);  // 0x7fff7c069692
	printf("%p\n", &a); // 0x7fff7c069692
}
```

- difference between **`*p++`**, **`++*p`** and **`*++p`:**

```c
int main()
{
    int arr[] = {10, 20};
    int *p = arr;
    ++*p;   // arr = {11, 20} | *p = 11. same as ++(*p)
    *p++;   // arr = {10, 20} | *p = 20. same as *(p++)
    *++p;   // arr = {10, 20} | *p = 20. same as *(++p)
}
```

- pointer’ların boyutu tuttukları değerle ilgili değildir:

```c
// program to show that array and pointers are different
int main()
{
	int arr[] = { 10, 20, 30, 40, 50, 60 };
	int *ptr = arr;

	printf("Size of arr[] %ld\n", sizeof(arr)); // "6x4'ten 24"

	// sizeof a pointer is printed which is same for all
	// type of pointers (char *, void *, etc)
	printf("Size of ptr %ld", sizeof(ptr)); // "8"
}
```

- sizeof all pointer types are same: 8.

```c
sizeof(int)    // 4
sizeof(int *)  // 8
sizeof(char **) // 8
```

- sonuç ne olur?

```c
int main() {
    void *vPtr;
    vPtr = (void *)0; 
    printf("%lu", sizeof(vPtr));
}
```

- C’de değişken isimleri _ ile başlayabilir:

```c
int main()
{
    int _ = 34;
    printf("%d\n", _);
}
```

- sonuç ne olur?

```c
int main()
{
    printf("%d\n", 8);
    printf("%d\n", 090);
    printf("%d\n", 00200);
    printf("%d\n", 0007000);
}
```

- bir sayıyı floata çevirmek için sonuna f ya da F koymalısın:

```c
1.425F ya da 1.623f
```

- % operatörü yalnızca integerlar üzerinde çalışır. float long vs. ile çalışmaz. onlar için math.h’da fmodf( ) ve fmodl( ) vardır.
- sonuç ne olur?

```c
int main()
{
    int a = 1, 2, 3;
    printf("%d", a);
}
```

ama şöyle olursa 

```c
int main()
{
    int a;
    a = 1, 2, 3;
    printf("%d", a);
}
```

- sonuç ne olur?

```c
int main()
{
    int a = (3, 6, 20);
    printf("%d\n", a);
}
```

- sonuç ne olur?

```c
	int main()
	{
	    int i = 3;
	    printf("%d", (++i)++);
	}
```

- sonuç ne olur?

```c
int foo(int* a, int* b)
{
    int sum = *a + *b;
    *b = *a;
    return *a = sum - *b;
}
int main()
{
    int i = 0, j = 1, k = 2, l;
    l = i++ || foo(&j, &k);
    printf("%d %d %d %d", i, j, k, l);
    return 0;
}
```

- sonuç ne olur?

```c
int main()
{
    int i = 5, j = 10, k = 15;
    printf("%d ", k /= i + j);
}
```

- sonuç ne olur?

```c
int main() {
	for (int i = 1; i < 10; i++) {
		printf("%d", i);
	}
	printf("\n");
	for (int i = 1; i < 10; ++i) {
		printf("%d", i);
	}
}
```

- sonuç ne olur?

```c
int main()
{
    printf("%ld", sizeof(printf("GeeksQuiz")));
}
```

```c
int main()
{
    int i = 12;
    int j = sizeof(i++);
    printf("%d  %d", i, j);
    return 0;
}
```

- sonuç ne olur?

```c
int main()
{
    int a = 1;
    int b = 1;
    int c = a || --b;
    int d = a-- && --b;
    printf(a); >>> 0
		printf(b); >>> 0
		printf(c); >>> 1
		printf(d); >>> 0
}
```

- sonuç ne olur?

```c
int main() 
{ 
  int a = 10, b = 20, c = 30; 
  if (c > b > a) 
    printf("TRUE"); 
  else
    printf("FALSE"); 
  return 0; 
}
```

- sonuç ne olur?

```c
int main()
{
    char *s[] = {"bugra", "kara", "molla"};
    char **p;
    p = s;
    printf("%s\n", ++*p); // ugra
    printf("%s\n", *p++); // ugra
    printf("%s\n", ++*p); // ara

    return 0;
}
```

- sonuç ne olur?

```c
#define VAL 32
int main()
{
    char arr[] = "bugrahan";
    *(arr + 0) &= ~VAL; 
    *(arr + 5) &= ~VAL;  
    printf("%s", arr);
}
```

- sonuç ne olur?

```c
int main()
{
    printf("%d", 1 << 2 + 3 << 4);
    return 0;
}
```

- swap işlemi için bit operatörleri kullanılırsa temp’e gerek kalmaz:

```c
x = x ^ y;
y = x ^ y;
x = x ^ y;
```

- sonuç ne olur?

```c
int main()
{
    int x = 10;
    int y = (x++, x++, x++);
    printf("x:%d y:%d\n", x, y);
    return 0;
}
```

- sonuç ne olur?

```c
void fun(void)
    printf("bugra");
void fun2(void)
    printf(" kara");
int main()
{
    fun(), fun2();
}
```

- girdiğin sayıyı binary çeviren program:

```c
int main()
{
    unsigned int num;
    int i;
    printf("enter a positive num: ");
    scanf("%u", &num);
    for (i = 0; i < 8; i++)
    {
        printf("%d", (num << i & 1 << 7) ? 1 : 0);
    }
}
```

- sonuç ne olur?

```c
int main()
{
 int var;  /*Suppose address of var is 2000 */
 
 void *ptr = &var;
 *ptr = 5;
 printf("var=%d and *ptr=%d",var,*ptr);
}
```

- kodun sadece belli bi parçasını çalıştırma:

```c
int main() {
    #ifndef BUGRA
    printf("enabled\n");
    #endif
    printf("hello\n");
}
```

- sonuç ne olur?

```c
int main() {
	int i;
	i++;
	printf("%d", i);
}
```

- bir sayıyı 2’yle çarpmakla << 1 aynı anlama gelir.

```c
int main() {
	int i = 5;
	printf("%d\n", i*2);  >>> 10
	printf("%d\n", i<<1); >>> 10
}
```

- gömülü sistemlerde klasik int, char, long vs. veri tiplerini kullanmak çok tehlikelidir. sebebi de mimariden mimariye bu veri tiplerinin boyutlarının değişkenlik göstermeleridir. mesela 32bit bi bilgisayarda bir int 32bit yer kaplar. 64 bitte ise 64 bit. Örneğin iki adet gömülü sistemin haberleştiğini düşünün. Birinde(X) int 32 bit olsun diğerinde(Y) ise 64 bit olsun. X’den Y’ye olan haberleşmede aynı kodları kullanmak istediğimizde Y’de daha az değer okumaya başlarız. Aynı sayıda değer okumaya kalkarsak da yanlış değer okuruz. Keza X’de bir struct’ı olduğu gibi sd carda yazarsak, ve Y’de o sd cardı aynı struct ile okumaya kalkarsak, eğer struct; int, float gibi platform safe olmayan değişkenler içerirse verileri yanlış okuruz. onun yerin **`stdint.h`** elemanları kullanılır. bunlardan bazıları **`uint32_t, int16_t, int8_t`** gibi veri tipleridir. bildiğimiz int’in karşılığı **`int32_t`** veri tipidir.

| uint8_t | unsigned char |
| --- | --- |
| uint16_t | unsigned short |
| uint32_t | unsigned int |
- bir değişkenin değerinin değiştirilmemesini istiyosan başına **`const`** koymalısın:

```c
int main()
{
	const int a = 10;
	a = 20;
	printf("a:%d\n", a);
}
```

değeri değişmesin istiyosak bunu kullanıyoruz. aynı şekilde *hafızadaki yeri* değişmesin istiyosak da **`static`** keywordünü kullanmalıyız. static olan bir değişkenin yeri bellekte değişmediğinden, o değişken son değerini her zaman korur. Misal şu bilgi de her yerde var; bir c dosyasında global olarak tanımlanmış statik bir değişken yalnız o dosyada kullanılabilir. Neden? Çünkü derleyici her dosyayı bir obje olarak derler. Sonra da objeler linker tarafından birleştirilir. Bir objede bir değişkenin yeri sabit tutuluyorsa o bellek alanı, sinemada rezerve edilen koltuğa benzer. Başkasına satmazlar ikisi de bir arada kullanılabilir.

ayrıca hız açısından bir değişkene daha çabuk erişmek istiyosan onu **`volatile`** ile register’a kaydedebilirsin 

```c
volatile int a = 100;
```

**`extern`** ön ekiyle ise başka dosyalardaki değişkenleri kullanabilirsin fakat header olayi daha mantıklı.

- some clean code rules
    - hungarian notation: naming the variables descriptive enough so the reader can get them without much trouble like intCounterOfArray, str_stacks_name etc. hem değişkenin tipi hem de görevi hakkında bilgi verir.
    - 
- bir koddaki leakleri satır bilgisiyle veren [program](https://www.codeproject.com/Articles/19361/Memory-Leak-Detection-in-C):

[leak_detector_c.zip](random%20C%20C++%20notes%209e3890b180bb40ccb900c7fd72a43e3a/leak_detector_c.zip)

- #include nasıl çalışır? derleyici konumlarını ezbere bildiği .h uzantılı kütüphaneleri direkt olarak include edebilir. diğerlerini konum belirterek include etmene izin verir:

```c
#include "../libft/libft.h"
```

# ile başlayan komutlar preprocessor komutları diye geçer ve yalnızca derleme zamanında çalışır. Yani biz selam.c fonksiyonunda selam.h’ı include edince derleyici derleme esnasında gider _selam.c diye geçici bir dosya oluşturur, selam.h’da ne var ne yoksa gider selam.c’nin tepesine koyarak toplam içeriği _selam.c’de saklar.

- **`fun( )`** vs. **`fun(void)`**: ikisi çoğu zaman aynı şey sanılsa da esasında aralarında bi fark vardır. fun( ) fonksiyonu parametre olarak ne gönderirsen gönder işleme almaz. fakat fun(void) fonksiyonu eğer herhangi bir parametre gönderirsen hata döndürür.

```c
void fun1() {
	printf("deneme1\n");
}

void fun2(void) {
	printf("deneme2\n");
}

int main() {
	fun1(1);
	fun2(1);
}
```

- header dosyaları her zaman **`.h`** uzantılı olmak zorunda değildir. include ederken o isimle ettigin sürece istedigin isimde uzantı verebilirsin
- *done* memory leakleri kontrol etmenin 5 yolu
    1. `memwatch`**:** memwatch, C için yazılmış bir leak kontrol programıdır. şu [linkten](https://sourceforge.net/projects/memwatch/) indirilebilir. sadece .c dosyanın içinde headerı tanımlıyosun ve gcc’ni optimize ediyosun. leakleri, double free’leri, over/underflowları kontrol eder.
- [ ]  [https://www.golinuxcloud.com/how-to-find-memory-leaks/](https://www.golinuxcloud.com/how-to-find-memory-leaks/)
- **`segmentation check list`:** A common run-time error for C programs by beginners is a "segmentation violation" or "segmentation fault." When you run your program and the system reports a "segmentation violation," it means your program has attempted to access an area of memory that it is not allowed to access. In other words, it attempted to stomp on memory ground that is beyond the limits that the operating system (e.g., Unix) has allocated for your program. bu hatayı her aldığında aşağıdaki adımlarla çözmeye çalışabilirsin:
    1. scanf( ) kullanırken & operatörünü unuttuysan seg verir
    2. printf( ) ve scanf( )’lerde conversion sayılarını kontrol et. aynı sayıda %s,d,c ve değişken kullanmazsan seg verir
    3. arrayin boyutundan büyük indise ulaşmaya çalışmadığını kontrol et
    4. pointerlarla kullanılan & ve * operatörlerini karıştırmadığından emin ol
    5. tüm pointerların valid bir adrese point ettiklerinden emin ol. bunun için pointerları şöyle ilklendirmelisin: 
    
    ```c
    int var;
    int *ptr = &var;
    ```
    
    1. check every where where you used pointers, array and/or &, * operators. buna
    2.  hiçbiri olmuyosa printf(”1\n”) kullan

When your program runs, it has access to certain portions of memory. First, you have local variables in each of your functions; these are stored in the stack. Second, you may have some memory, allocated during runtime (using either malloc, in C, or new, in C++), stored on the heap (you may also hear it called the "free store"). Your program is only allowed to touch memory that belongs to it -- the memory previously mentioned. Any access outside that area will cause a segmentation fault. Segmentation faults are commonly referred to as segfaults. There are four common mistakes that lead to segmentation faults: 

- dereferencing NULL,
- dereferencing an uninitialized pointer,
- dereferencing a pointer that has been freed (or deleted, in C++) or that has gone out of scope (in the case of arrays declared in functions),
- writing off the end of an array
- and a recursive function that uses all of the stack space. On some systems, this will cause a "stack overflow" report, and on others, it will merely appear as another type of segmentation fault.

The strategy for debugging all of these problems is the same: load the core file into GDB, do a backtrace, move into the scope of your code, and list the lines of code that caused the segmentation fault. 

- valgrind kullanırken hangi satırın leak verdiğini görmek istiyosan
    1. derlerken -g flagiyle derlemelisin 
    
    ```c
    gcc -g a.c -o dosya
    ```
    
    1. valgrindi optimize etmelisin 
    
    ```c
    valgrind --tool=memcheck --leak-check=yes ./dosya
    ```
    
    bu satır bilgisini verecektir  
    
    ```c
    ==421750==  100 bytes in 1 blocks are definitely lost in loss record 1 of 1
    ==421750==  at 0x4848899: malloc (in /usr/libexec/valgrind/vgpreload_memcheck-amd64-linux.so)
    ==421750==  by 0x10915E: main (a.c:4) // here
    ```
    
    valgrind array-overflowları, double free ve ilklendirilmemiş değişken kullanımları hakkında da bilgi verir. 
    
- **`big-endian`** vs. **`little-endian`**: big-endian sistemler bitleri sağdan sola tutarken little-endian soldan sağa tutar. yani big-endian most-significant-bit’i (en soldaki bit) ilk hafıza adresinde tutarken little endian ise ilk hafıza adresinde least-significant-bit’i tutar (en sağdaki bit). bu isimler de guliverin gezilerindeki liliputların yumurtayı kırmaya başlama şekillerine göre ayrılmalarından geliyor.  aşağıdaki kod sistem little-end ise 1, big-end ise 0 verir:

```c
int main()
{
  int x = 1;
  char *y = (char*)&x;
  printf("%c\n",*y+'0');
}

// if it is little-endian, x will be hold like this:
higher memory
          ----->
    +----+----+----+----+
    |0x01|0x00|0x00|0x00|
    +----+----+----+----+
    A
    |
   &x

// if it is big-endian, x will be hold like this:
    +----+----+----+----+
    |0x00|0x00|0x00|0x01|
    +----+----+----+----+
    A
    |
   &x
```

big-little endian kontrolünün bir başka yolu:  

```c
int x = 9;
if (*(char *)&x == 0x09)
	printf("1\n");
// we cast x as a byte to get its very first 
// byte, it will return true (meaning little 
// endian) if the first byte is equal to 9.
```

- negatif indis kullanımı:

```c
#include <limits.h>	// INT_MAX
#include <stdio.h>	// printf

int main(void) {
	int x[2001];
	int *y = &x[1000];

	(void)x;
	y[-10] = 5;
	printf("%d\n", y[-10]);
}
```

- *There are two ways to write error-free programs; only the third one works – Alan J. Perlis*
- what may cause segmentation faults?
    - infinite loops
    - = instead of ==
    - forgetting break;
    - 
- sonuç ne olur?

```c
int main(void)
{
	unsigned char c = 0;
	while (c < 150)
	{
		write(1, &c, 1);
		c++;
	}
}
```

- VLA: variable-length-arguments in C: below is a usage

```c
int fun(int x, int y, int arr[x][y]); 
```

- sonuç ne olur?

```c
int main()
{
	int i = 0; 
	i = (i++);
	write(1, &i + '0', 1);

	return 0;
}
```

- sonuç ne olur?

```c
int main()
{
	const char s[20] = "hello world";
	*s = 'a';
	s[0] = 'b';
}
```

- sonuç ne olur?

```c
#define MAX(a,b) a > b ? a : b
int main()
{
	int a = 5;
	int b = 42;
	int c = 40 + MAX(a, b);
	printf("%d\n", c);
}
```

- Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live – John Woods
- :D
    
    ![Screenshot from 2023-01-13 02-27-02.png](random%20C%20C++%20notes%209e3890b180bb40ccb900c7fd72a43e3a/Screenshot_from_2023-01-13_02-27-02.png)
    
- would it work?

```c
int n;
scanf("%d", &n);
int array[n];
```

- **`int **a`** ile **`int[][]`** tam olarak aynı şey değildir. bc a 2D array is not simply a 1D array of 1D arrays, but rather like one big 1D array that has been cut into n pieces. mesela şu kod yanlıştır:

```c
int a[3][5];
int **aPtr;
aPtr = a;   // !!
```

doğrusu şudur: 

```c
int a[3][5];
int (*aPtr)[5];
aPtr = a;  // OK
```

örnek: 

```c
int func(int a, int b, int arr[3][4]) // you can erase 3, it still works
{
	for (int i = 0; i < a; i++)
	{
		for (int j = 0; j < b; j++)
			printf("[%d]", arr[i][j]);
	}
}

int main()
{
	int ar[3][4] = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}};
	func(3, 4, ar);
}
```

- strncpy( ) kullanırken sonuna null koymadıgını bilmen gerekir

```c
int main() {
	char s1[10];
	strncpy(s1, "hello", 5); // did not put \n at the end
	s1[5] = '\0';
	printf("%s\n", s1);
}
```

- normalde characterleri `' '` ile kullanirken neden write’ta bunu yapamiyoruz?

```c
// yanlıs
write(1, '-', 1);

// dogru
write(1, "-", 1);

// dogru2
char a = '-';
write(1, &a, 1);
```

- hata nerede?

```c
printf("%s", 'a');
```

- low level çalışan kurumlar genelde int yerine int32_t kullanırlar ki farklı OS ve mimarilerde int kesin 4 bit olsun
- çok eski nesil derleyicilerde ++i ifadesi i++’den daha verimli çalışıyordu
- random bir sayı üretmenin en kısa ve güzel yolu sayının pointer adresini int’le castlemektir:

```c
int main() {
	int a = (int)&a;
	printf("%d\n", a);
}
```

- bir sayıyı +1’lemenin bitwise yolu:

```c
a = 10;
a = -~a;
print(a) >> 11
```

- main( ) fonksiyonu parametre olarak sadece şunlari alabilir

```c
int main(int ac, char **av, char **env);
```

- sonunda ondalık olan tüm decimal sayılar double’dır, float değil. floatların sonunda F ya da f bulunur.
- `char[][]`, `char *[]`, `**char` bunların hepsi 2D char array oluşturur fakat benzer anlama gelir: `char[num_of_strings][size_of_each_string]`. aynı şekilde `int *a[10]` demek int pointer türünden 10 tane eleman demektir.
- 42 normunda structları **`bugra_t`** şeklinde tanımlama zorunlugu var. buradaki **`_t`** type anlamına geliyor.
- **`data->str`** ile **`(*data).str`** aynı şeydir. str pointer tanımlanmışsa **`.`** yerine **`->`** kullanılır.
- header’ların 2 kere include edilmesini önlemek için 2 yol var
    - include guard
    
    ```c
    #ifndef BUGRA_H
    #define BUGRA_H
    
    // struct
    
    #endif
    ```
    
    - pragma once
    
    ```c
    #pragma once
    
    // struct
    ```
    
- `unsigned` really is a shorthand for `unsigned int`, and so defined in standard C.
- sonuç ne olur?

```c
unsigned int a = -30;
printf("%d\n", a);
```

- C’de aynı satırda üçlü atama yapabilirsin

```c
int a;
int b;
int c;
a = b = c = 30; 
```

- sonuç ne olur?

```c
printf("%s", "bugra" "kara");
```

- valgrind ile debug ederken satır numarası da versin istiyosan `-g` ile derlemelisin
- malloc’un dönüş değeri ayırdığı adresin başlangıcıdır. o yüzden o adres başlangıcını bir pointera atadığımızda artık o pointer o adresi (daha doğrusu içerisindeki değeri) gösterir hale gelir

```c
int *ptr = malloc(sizeof(int) * 5);
```

peki aynı objeye malloc ile iki kere yer ayırırsak ne olur?  

```c
char *ss = malloc(100);
char *ss = malloc(150);
```

bu durumda memory leak alırız. sebebi ise şu: ilk mallocta 100 byte uzunlugunda bir yer acıldı, tamam. fakat bu acılan yeri henüz freeleyemeden hafızanın *başka bir yerinde* 150 byte uzunlugunda bir başka yer açıldı. artık bu ilk açtığın yerin adresini tutacak bir pointer değişken kalmadı o yüzden adresini unuttuğun bu yeri freeleyemiyosun. haliyle de memory leak oluyor.  aynı şey şunda da geçerli 

```c
int a;
a = 14;
a = 20;
```

14’e, daha doğrusu 14’ün değerinin tutulduğu hafıza bloğuna artık erişemiyoruz. 

- sonuç ne olur?

```c
i = (a, b);
```

- C’de bir array l-value olamaz. yani direkt içine bir şey atayamazsın

```c
int ar[5], ar2[5];
ar = ar2; // yanlış
```

bunun yerine bir while iterator yaratıp teker teker ar2’nin elemanlarını ar’ın elemanlarına eşitlemeliyiz. memcpy( ) de kullanılabilir. ayrıca arraylerin aksine struct elemanlarını kopyalayabiliriz 

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
	printf("%d\n", ar[0]); >>> 30
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

- eski tip derleyeci C’lerinde VLA (variable-length-arrays) olayı yoktur. o yüzden bir arrayin boyutu yalnızca derleme zamanında belirlenebilir, çalışma zamanında belirlenemez. eğer belirlenebilseydi programlar çok daha yavaş çalışır, stack yapısı çok daha karmaşık olur, fonksiyon çağırmak çok daha az verimli olurdu.

```c
int i = 10;
int arr[i]; // C'de bu yoktur
```

ama c99’dan sonra gelmiştir 

```cpp
int main()
{
	int n;
	printf("Enter the size of the array: ");
	scanf("%d", &n);

	int vla[n];

	return 0;
}
```

- `calloc` ve `malloc` arasında 2 fark vardır
    - mallocun aksine calloc ayırdığı yeri 0’la doldurur
    - calloc returns an array of objects, malloc returns one object.
- stack is where all the functions’ local variables are stored. heap are where variables defined with malloc, calloc and realloc are stored. fetching memory from heap is much slower than fetching from stack. unlike stack, variables do not get deallocated automatically, so you must use free() later on. stack however doesn’t require this. this is why we don’t have to call free after we declare a normal variable but we do when we use malloc. recursive çağrılar da heap’te gerçekleşir.
- if you free a pointer, what you actually mean is that you freed the pointed-to memory on ram, not the pointer itself.
- `NULL` vs. `NUL` farkı: NULL stddef kütüphanesinde tanımlı NULL pointer gösteren bir makrodur. NUL ise ASCII tablosunun ilk elemanının ismidir. sayısal olarak 0’a eşittir. NULL can be defined as `(void *)0`, NUL as `\0`. both can be simply defined as `0`. NULL is meant to be used as a pointer, NUL as a character. mind the difference.
- ayırdığın yerin kesin boyutunu öğrenmenin C’de bir yolu yoktur. somehow free( ) knows it but it is a very complicated formula.
- çoklu dosyalarda çalıştığın bir kodda eğer bir fonksiyonu yalnızca o dosyada kullanacaksan statik tanımlaman daha mantıklı olur.
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
- sonuç ne olur?

```c
int main()
{
    int a = 23;
    int *aPtr = &a;
    printf("%d\n", *&*&*aPtr);
}
```

- sonuç ne olur?

```c
int main(void) {
	char x = "a\n";
	write(1, &x, 1);
}
```

- prefix while’da şöyle çalışır:

```c
int main() {
	int i = 0;
	while (i++ < 10) {
		printf("%d ", i);
	}
} // >>> 1 2 3 4 5 6 7 8 9 10

int main() {
	int i = 0;
	while (++i < 10) {
		printf("%d ", i);
	}
} // >>> 1 2 3 4 5 6 7 8 9

int main() {
	int i = 0;
	while (i < 10) {
		printf("%d ", i);
		i++;
	}
} // >>> 0 1 2 3 4 5 6 7 8 9
```

- sonuç ne olur?

```c
int main() {
	int arr[] = {10, 20, 0, 30, 50};
	int i = 0;
	while (arr[i])
	{
		printf("[%d]", arr[i]);
		i++;
	}
}
```

- örnek

```c
if (!a)
```

- örnek

```c
int main() {
	char *str = "bugra";
	char str2[] = "cemre";
}
```

![Ekran Resmi 2023-02-23 ÖÖ 6.16.05.png](random%20C%20C++%20notes%209e3890b180bb40ccb900c7fd72a43e3a/Ekran_Resmi_2023-02-23_OO_6.16.05.png)

heapte bir şey depolansın istiyorsan malloc/calloc/realloc() kullanmalısın.

- `memcpy` fonksiyonu, `strcpy` fonksiyonunun aksine, sadece stringler değil, herhangi bir veri türünün bellek bölgesini kopyalayabilir.
- Pointer aritmetiği yaparken, pointer'ın türüne göre büyüklük farklıdır. Mesela bir `char` pointer'ı 1 byte, bir `int` pointer'ı ise 4 byte ilerler.
- `NULL` ve `NUL` farklı şeylerdir. `NULL`, bir pointer'ın gösterdiği bellek adresinin boş olduğunu ifade ederken, `NUL` bir karakterin (ASCII tablosunda) sıfır (0) olmasını ifade eder.
- Her malloc çağrısında ayrı bir hafıza alanı oluşturulur. Bu yüzden

```c
char *ss = malloc(100); 
char *ss = malloc(150);
```

kodu hatalıdır ve memory leak'e sebep olur.

- Bir array l-value olamaz. Bu yüzden `ar = ar2;` yanlıştır.
- Değişkenler stack ve heap'te farklı yerlerde depolanır. Global ve statik değişkenler RAM'de `data-segment` adı verilen yerde saklanırken, fonksiyonların içinde tanımlanan değişkenler stack'te saklanır.
- recursive mantıgı tam olarak nasıl calısır?
    
    ```c
    // mesela şöyle bir rec_fac fonksiyonumuz olsun
    int recursive_factorial(int n) {
    	if (n == 1)
    		return n;
    	else
    		return (n * recursive_fac(n-1);
    }
    ```
    
- sonuç ne olur?

```c
int	main(void)
{
	int	x;
	int	y;
	int	z;

	x = 5;
	y = 10;
	z = x*y + (++y);
	printf("%d\n",z);
}
```

- sonuç ne olur?

```c
int main()
{
	printf("%lu", sizeof(void));
	return 0;
}
```

- malloc’un başındaki typecast olayının sebebi:

```c
int *a = (int *)malloc(sizeof(int) * 10);
```

- malloc ayırdıgı yeri baslangıcta garbage value ile doldurur.
- bir fonksiyonun kod blogunu calıstırmadan o fonksiyonun return degerini bir degiskene atamak imkansızdır:

```c
int game()
{
	printf("bugra\n");
	return 5;
}

int main()
{
	int x = game();
}
```

- OOP pillars
    1. Polymorphism
        1. Compile Time Polymorphism
            1. Function Overloading: 
            
            ```cpp
            class Base {
              public:
                void fun(int a) {
                  std::cout << "this is " << a << std::endl;
                }
                void fun(float b) {
                  std::cout << "this is " << b << std::endl;
                }
            };
            
            int main() {
              Base base;
            
              base.fun(53);
              base.fun(2.99);
            }
            ```
            
            ii. Operator Overloading : bir operatörü kendi istediğin şekilde yeniden yazmak
            
            ```cpp
            class Deneme {
            	public:
            		int val;
            
            		Deneme() {
            			val = 5;
            		}
            		
            		void operator--() {
            			val = val - 3;
            		}
            };
            
            int main() {
            	Deneme deneme;
            	--deneme;
            	std::cout << deneme.val << std::endl;
            }
            ```
            
        2. Run Time Polymorphism
            1. Function Overriding: Function overriding in C++ is termed as the redefinition of base class function in its derived class with the same signature i.e. return type and parameters
            
            ```cpp
            class Base {
              public:
                void func() {
                  std::cout << "this is base func" << std::endl;
                }
            };
            
            class Derived : Base {
              public:
                void func() {
                  std::cout << "this is derived func" << std::endl;
                }
            };
            
            int main() {
              Derived derived;
              derived.func(); // this is derived func
            }
            ```
            
            function overriding’in farklı özellikleri daha var. mesela derived classta base classın fonksiyonunu çağırabilirsin 
            
            ```cpp
            class Base {
              public:
                void func() {
                  std::cout << "this is base func" << std::endl;
                }
            };
            
            class Derived : Base {
              public:
                void func() {
                  std::cout << "this is derived func" << std::endl;
            
            			Base::func(); // bu durumda her ikisini de yazdırır
                }
            };
            
            int main() {
              Derived derived;
              derived.func();
            }
            ```
            
            ya da Base class pointerı kullanırsan base’in fonksiyonu çalışır 
            
            ```cpp
            class Base {
              public:
                void func() {
                  std::cout << "this is base func" << std::endl;
                }
            };
            
            class Derived : public Base {
              public:
                void func() {
                  std::cout << "this is derived func" << std::endl;
                }
            };
            
            int main() {
              Derived derived;
              Base *basePtr = &derived;
            	basePtr->func(); // this is base func
            }
            ```
            
            ya da :: operatörü sayesinde derived üzerinden base fonksiyonuna erişebilirsin 
            
            ```cpp
            class Base {
              public:
                void func() {
                  std::cout << "this is base func" << std::endl;
                }
            };
            
            class Derived : public Base {
              public:
                void func() {
                  std::cout << "this is derived func" << std::endl;
                }
            };
            
            int main() {
              Derived derived;
              derived.func(); // this is derived func
            	derived.Base::func(); // this is base func
            }
            ```
            
            function overloading ile function overriding farkları
            
            - function overloading inheritance olmadan da görülebilir ama overriding olması için bir Derived classa ihtiyacımız var
            - bir fonksiyon birden fazla kez overload edilebilir ama yalnızca bir kere override edilebilir
            - overloading aynı scope’ta olur overriding farklı scopelarda
            
            ii. Virtual Function: A virtual function is a member function that is declared in the base class using the keyword virtual and is re-defined (Overridden) in the derived class 
            
            ```cpp
            class Base {
              public:
                virtual void fun() {
                  std::cout << "base fun() called" << std::endl;
                }
            };
            
            class Derived : Base {
              public:
                void fun() override {
                  std::cout << "overridden fun() called" << std::endl;
                }
            };
            
            int main() {
              Base base;
              base.fun(); // base fun() called
            
              Derived derived;
              derived.fun(); // overridden fun() called
            }
            ```
            
    2. Encapsulation: Bir varlığı bütün olarak ele almak ve varlığın yapısını dışarıyla oluşabilecek sonuçlara karşı korumayı amaçlar.Bu mekanizma hakkında genel fikir basittir. Bir nesnede dışarıdan görünmeyen bir özelliğiniz varsa ve erişimi sağlayan yöntemlerle bir araya getirirseniz, belirli bilgileri gizleyebilir ve nesnenin iç durumuna erişimi kontrol edebilirsiniz. **`public`**, **`protected`**, **`private`** bunda kullanılır. 
    3. Abstraction: Detayların, karmaşıklığın azaltılması anlamına gelmektedir.Bir nesnenin neleri içermesi gerektiğine odaklanmayı ve önemli bilgileri gösterirken istenmeyen ayrıntıları gizlemeyi amaçlar. Büyük projelerde yapılan çalışmaların hepsini bilmek gereksizdir. kullanıcıya sadece gerekli yerleri açık yapma. **`abstract class`** ve **`interface`**
    
    ```jsx
    #include <iostream>
    using namespace std;
    
    class Sum {
    private:
    	// private variables
    	int a, b, c; 
    public:
    	void sum(int x, int y)
    	{
    		a = x;
    		b = y;
    		c = a + b;
    		cout<<"Sum of the two number is : "<<c<<endl;
    	}
    };
    int main()
    {
    	Sum s;
    	s.sum(5, 4);
    	return 0;
    }
    ```
    
    1. Inheritance: Türkçe karşılığı ‘miras alma, kalıtım’dır. Inheritance; bir nesnenin özelliklerinin başka nesneler tarafından kullanılabilmesine olanak sağlar. Sınıflar arasında hiyearşik bir yapı kurabilmek için kullanılır. Inheritance bir sınıfın kendi özellikleri ve metotları yanı sıra kalıtım aldığı base(taban) sınıfın özellikleri ve metotlarına da sahip olabilmesidir.Ancak kalıtım alan sınıf herhangi bir özellik veya metoda sahip olmasa da olur. 
- sonuç ne olur?

```cpp
int main()
{
	std::string name;
	std::string surname;
	std::string nickname;
	std::cin >> name;
	std::cin >> surname;
	std::cin >> nickname;
	std::cout << "your name: " << name << std::endl;
	std::cout << "your surname: " << surname << std::endl;
	std::cout << "your nickname: " << nickname << std::endl;
}
```

- 

- sonuç ne olur?

```c
#include <stdlib.h>
int main() {
	int *ar = malloc(100);
	*ar = 325;
	system("leaks a.out");
}
```

- { } ile sayısal olmayan struct, array ve vektörleri ilklendirebilirsin, {0} ile herhangi bir veri tipini

```c
int main() {
	int a[] = {};
	int a2[10] = {};
	void *p = {}; // hata 
	int i = {}; // hata 
	
	/* ... */

	void *p = {0};
	int i = {0};
}
```

- sonuç ne olur?

```c
int foo() {
    int* a;
    int* b;
    {
        static int foo;
        a = &foo;
    }
    {
        static int foo;
        b = &foo;
    }
    // this always returns false: two static variables with the same name (foo)
    // but declared in different scope refer to different storage.
    return a == b;
}

int main() {
	int a = foo();
	printf("%d\n", a); // her çalıştırdığında 0
}
```

- bir struct’ı array olarak da tanımlayabilirsin:

```c
typedef struct {
	int age;
	float height;
} Person[3];
```

```c
int	main(void)
{
	Person people;
	people[0].age = 10;
	people[0].luckyNum = 21;
	printf("%d\n", people[0].luckyNum); // 21
	printf("%d\n", people[0].age);      // 10
	people[3].age = 20;                 // hata verir çünkü person 3 elemanlı
}
```

- sonuç ne olur?

```c
const char *s = "bugra";
s = "cemre";
s[3] = 't'; // hata verir çünkü s burada pointer
printf("%s\n", s);
```

```c
const char * const s = "bugra";
s = "cemre"; // artık bu da hata verir çünkü const s dedin
printf("%s\n", s);
```

- In general, valgrind is a more reliable tool to detect memory leaks than leaks. valgrind analyzes your program at runtime and can detect memory errors, such as memory leaks, buffer overflows, and invalid memory accesses. On the other hand, leaks is a command-line tool that analyzes a running process's memory usage and prints a list of leaked memory blocks. However, leaks can only detect memory leaks at the end of a program's execution, so it may miss some leaks that occur during the program's execution.
- sonuç ne olur?

```c
int main()
{
    char s1[] = "bugra";
    char s2[] = {'b', 'u', 'g', 'r', 'a', '\0'};
    int s1_len = sizeof(s1) / sizeof(s1[0]);
    int s2_len = sizeof(s2) / sizeof(s2[0]);
    printf("s1:%d\ts2:%d\n", s1_len, s2_len);
	}
```

- sonuç ne olur?

```c
void swap(char *str1, char *str2)
{
  char *temp = str1;
  str1 = str2;
  str2 = temp;
}  
   
int main()
{
  char *str1 = "Geeks";
  char *str2 = "Quiz";
  swap(str1, str2);
  printf("str1 is %s, str2 is %s", str1, str2);
  return 0;
}
```

doğrusu şudur 

```c
void swap(char **s1, char **s2) {
	char *temp = *s1;
	*s1 = *s2;
	*s2 = temp;
}

int main()
{
  char *str1 = "Geeks";
  char *str2 = "Quiz";
  swap(&str1, &str2);
  printf("str1 is %s, str2 is %s", str1, str2); // Quiz Geeks
}
```

- sonuç ne olur?

```c
int fun(char *str1)
{
    char *str2 = str1;
    while (*++str1) // *str1++ deseydik 10 dönerdi
        ;
    return (str1 - str2);
}

int main()
{
    char *str = "123456789";
    printf("%d", fun(str));
    return 0;
}
```

- sonuç ne olur?

```c
char c[] = "1234abcd";
char *p = c;
printf("%s", p + p[3] - p[1]);
```

- sonuç ne olur?

```c
int main()
{
    char str[] = "bugrakara";
    printf("%s", &str[5]);  // kara
    printf("%s", &5[str]);  // kara
    printf("%s", str + 5);  // kara
    printf("%c", *(str+7)); // r
    printf("%c", str[7]);   // r
    printf("%c", 7[str]);   //  r
}
```

- sonuç ne olur?

```c
char p[20]; 
char *s = "bugra"; 
int length = strlen(s); 
for (int i = 0; i < length; i++) 
    p[i] = s[length — i]; 
printf("%s", p);
```

- sonuç ne olur?

```c
void my_toUpper(char *str, int index)
{
    *(str + index) &= ~32;
}

int main()
{
    char *arr = "geeksquiz"; // eğer char arr[] olsaydı GeeksQuiz olurdu
    my_toUpper(arr, 0);
    my_toUpper(arr, 5);
    printf("%s", arr);
    return 0;
}
```

- sonuç ne olur?

```c
int main()
{
    char str[] = "%d %c";
    char arr[] = "bugrakara";
    printf(str, 0[arr], 2[arr + 3]); // 98 k
}
```

- sonuç ne olur?

```c
int main()
{
    char str[20] = "bugrakara";
    printf("%d", sizeof(str));
}
```

- sonuç ne olur?

```c
int main()
{
    char *s1 = "bugra";
    char s2[] = "bugra";
    printf("sizeof(s1) = %ld", sizeof(s1)); // 8
		printf("sizeof(s2) = %ld", sizeof(s2)); // 6
    printf("\n");
}
```

- sonuç ne olur?

```c
char str1[100];

char *fun(char str[])
{
    static int i = 0;
    if (*str)
    {
        fun(str + 1);
        str1[i] = *str;
        i++;
    }
    return str1;
}

int main()
{
    char str[] = "12345 6789 abc";
    printf("%s", fun(str));
}
```

- sonuç ne olur?

```c
void foo(char *a)
{
    if (*a && *a != ' ')
    {
        foo(a + 1);
        putchar(*a);
    }
}

int main()
{
    foo("1234 5678");
}
```

- sonuç ne olur?

```c
int main( )
{
    char s1[7] = "1234", *p;
    p = s1 + 2;
    *p = '0' ;
    printf ("%s", s1);
}
```

- sonuç ne olur?

```c
struct Node
{
    char x, y, z;
};

int main()
{
    struct Node p = {'1', '0', 'a' + 2};
    struct Node *q = &p;
    printf("%c", *((char *)q + 1)); // 0
    printf("%c", *((char *)q + 2)); // c
}
```

- sonuç ne olur?

```c
int main() {
    int x, y = 5, z = 5;    
    x = y == z;
    printf("%d", x);
}
```

- sonuç ne olur?

```c
int main()
{
    int i = 3;
    printf("%d", (++i)++);
    return 0;
}
```

- in c, functions can return any type except array and functions. we can get around this by instead returning *pointers* to arrays and functions.
- C’de staticler şunlarla kullanılabilir
    - global değişkenlerle
    
    ```c
    static int a = 30;
    ```
    
    - yerel değişkenlerle
    
    ```c
    int add(int n)
    {
    	static int m;
    };
    ```
    
    - fonksiyonlarla
    
    ```c
    static myFun() { };
    ```
    
    fakat fonksiyona parametre olarak static veremezsin 
    
    ```c
    int myFun(static int a); // ERRONEOUS
    ```
    
- gets( ) fonksiyonu bufferın size’ını bilmediği için EOF ya da \0 görene kadar hafızada ne varsa okumaya devam eder. o yüzden kullanması risklidir.
- scanf(%4s”, str) demek maksimum 4byte oku demektir.
- sonuç ne olur?

```c
void f(int *p, int *q)
{
    p = q;  // etkisiz. eğer *p = *q deseydi p 2 q 1 olurdu 
    *p = 2;
}
int i = 0, i2 = 1;
int main()
{
    f(&i, &i2);
    printf("i: %d\n", i);  // 0
    printf("i2:%d\n", i2); // 2
    return 0;
}
```

- çok basit stack-overflow örneği

```c
int main()
{
    printf("hi");
    main();
}
```

- C’de aynı header’ı birden fazla kere çağırabilirsin, hiçbir şekilde hata vermez. Hafıza sorunu da çıkmaz çünkü C sadece bir kere çağırır kütüphaneyi, bu da kütüphanede yazan #ifndef #define macroları sayesindedir.
- sonuç ne olur?

```c
int main()
{
    int var; /*Suppose address of var is 2000 */

    void *ptr = &var;
    *ptr = 5;
    printf("var=%d and *ptr=%d", var, *ptr);
}
```

- sonuç ne olur?

```c
int main()
{
    int x = 1, i = 1;
    while (x <= 500)
    {
        x = pow(2, x);
        i++;
    }
		printf("i: %d\n", i); >>> 5
} 
```

- sonuç ne olur?

```c
int main()
{
    static int i = 5;
    if (--i)
    {
        main();            // if it was after the printf(), it'd print 4 3 2 1
        printf("%d ", i);
    }
}
```

- sonuç ne olur?

```c
int main()
{
    int x = 5;
    int *const  = &x;
    ++(*ptr);
    printf("%d", x);
```

```c
int main()
{
    int x = 5;
    int const * ptr = &x;
    ++(*ptr);
    printf("%d", x);
}
```

know the difference between constant pointer and a pointer to a constant. **`int *const ptr`** —> here ptr is constant pointer. You can change the value at the location pointed by pointer p, but you can not change p to point to other location. **`int const *ptr`** —> here ptr is a pointer to a constant. You can change ptr to point other variable. But you cannot change the value pointed by ptr. Therefore first program works well because we have a constant pointer and we are not changing ptr to point to any other location. We are only incrementing value pointed by ptr.

- **`typedef`** kelimesi veri tipine alias atamak için kullanılabilir

```c
int main() {
    typedef int my_int;
    my_int a = 10;
    my_int b = 32;
}
```

- sonuç ne olur?

```c
int fun()
{
    static int num = 16;
    return num--;
}

int main()
{
    for (fun(); fun(); fun())
        printf("%d ", fun());
    return 0;
}
```

- sonuç ne olur?

```c
int main() {
	int x = 50;
	static int y = x;
}
```

- sonuç ne olur?

```c
unsigned int a = -20;
printf("%u\n", a);
```

- The key combination for EOF (End-of-File) depends on the operating system and terminal/console being used. In Unix-based systems (including Linux and macOS), the key combination for EOF is Ctrl+D. In Windows, the key combination for EOF is Ctrl+Z, followed by pressing the Enter key.
- < > ile “ “ arasındaki fark nedir?

```c
#include <lib.h> // aramaya önce derleyici ve sistem klasörlerinden başlar
#include "lib.h" // ararken o anki klasörden genele doğru gider
```

- In C, a heap is a region of memory used for dynamic memory allocation. It is managed by the programmer and allows for the allocation and deallocation of memory at runtime. The heap is distinct from the stack, which is used for storing local variables and function call frames. Unlike the stack, memory allocated on the heap persists beyond the lifetime of the function that allocated it. The heap is typically used for data structures that require dynamic resizing or for allocating large amounts of memory. Examples of data structures that are commonly implemented using the heap include linked lists, binary trees, and hash tables. In C, memory on the heap is allocated using functions such as malloc() and calloc(), and deallocated using the free() function. It is important to manage memory correctly on the heap to avoid memory leaks and other issues that can arise from improper memory management.
- bir stringe bir fonksiyon içinde yer ayırırsan daha sonra yer ayırmadan kullanabilirsin, fonksiyonda ayırdığın yer geçerli kalır:

```c
char* fun(char *st) {
	return st;
}

int main() {
	// mesela burada bugra'ya yer ayirmadik ama string literal kullandigimiz icin
	// otomatik olarak bugra + null kadar s'ye yer ayirir ve içine bugra yazdirir
	// fun() burada b'yi gösteren bir adres return eder.
	char *s = fun("bugra");
	printf("%s\n", s);
}
```

- sonuç ne olur?

```c
int main() {
	int i = 0;
	while (i < 5)
		i++;
	printf("%d\n", i); // 5
	i = 0;
	while (i++ < 5);
	printf("%d\n", i); // 6
}
```

- bir dosyayı farklı sürüm gcc’yle derlemek istiyosan

```python
gcc -std=c89 -o output deneme.c
```

- son çalıştırdığın executable başarılı mı başarısız mı öğrenmek için **`$?`** kullanabilirsin

```python
$ ./a.out
$ $?
```

- hem static değişkenler hem de global değişkenler 0’a eşitlenir ama static değişken kullanmak bir tık daha fazla yer kaplar.
- sonuç ne olur?

```c
void fun1() {
	int a;
	printf("%d\n", a);
}

void fun2() {
	int a = 42;
}

int main() {
	fun2();
	fun1();
}
```

- bir kodu farklı optimizasyon levelleriyle derlemek için

```c
cc -O1 a.c // default optimizasyon seviyesi
cc -O2 a.c
cc -O3 a.c // en yüksek
```

- sonuç ne olur?

```c
void fun()
{
	int a = 40;
	a = a++;
	printf("%d\n", a);
}

int main()
{
	fun();
}
```

- sonuç ne olur?

```c
int fun1()
{
	printf("3\n");
	return 3;
}

int fun2()
{
	printf("4\n");
	return 4;
}

int main()
{
	int a = fun1() + fun2();
	printf("%d\n", a);
}
```

- sonuç ne olur?

```c
printf("%d\n", sizeof(int));
```

- C’de bir struct yapısının boyutu nedir?

```c
struct myStruct
{
	int a;
	char *c;
	char b;
};

int main()
{
	printf("%zu\n", sizeof(struct myStruct));
}
```

- sonuç ne olur?

```c
struct try {
	void (*try)(int);
}try1;

void add(int i) {
	printf("hello world");
}

int	main(void)
{
	try1.try = add;
	try1.try(2);
	return (0);
}
```

- C dilinin RAM modeli beş parçadan oluşur
    1. Stack: tüm yerel değişkenler, argümanlar, otomatik olarak yer ayrılmış arrayler tutulur. LIFO mantıgıyla calısır. 
    2. Heap: malloc ve türevlerine burada yer açılır. 
    3. BSS: manuel olarak ilklendirilmemiş tüm global ve statik değişkenler burada tutulur
    4. Data: ilklendirilmiş tüm global ve statik değişkenler burada tutulur 
    
    ```c
    int global = 156;  //<- stored in .data
    
    void func()
    {
        int a = 1;  // stored on stack
        int b = 2;  // stored on stack
        int *c = malloc(100); // stored on heap
    }
    
    int main()
    {
      func();
        return 0;
    }
    ```
    
    1. Text: çevrilmiş makine dili kodlarının saklandığı segment 
    
    ```c
    objdump -h a.out
    ```
    
    komutuyla görebilirsin çıktıları 
    
    [çizim hali](https://excalidraw.com/#json=R7ZFFEfIwBg20FOw6plit,DLD9m0m8Lmt0EI39ELPUCQ) 🪨
    stack aşağı doğru büyür, heap yukarı doğru büyür. eğer bunlar çakışırsa `stackoverflow` olur. fonksiyonlar sonlandıkça stacke verilen alan OS’ye geri verilir böylece stack’in boyutu küçülür. 
    
- printf fonksiyonu hemen her zaman buffera atar içeriği sonra yazdırır. buffera atmasın direkt yazdırsın istiyosan /codf

```c
flush(stdout)
```

kullanabilirsin

- komut satırından aldıgın 2D argüman dizisini sayılarla öteleyebilirsin /codi

```c
int main(int ac, char **av) {
	av += 0; // av -> ./a.out
	av += 1; // av -> bugra
	av += 2; // av -> kara ...
}
// gcc a.c && ./a.out bugra kara 
```

- c’de renkli çıktı almanın yolu renk kodlarıdır

```c
#define GREEN "\033[0;32m"
# define RESET "\033[0m"

int ft_putstr(char *str)
{
	write(1, str, strlen(str));
}

int main()
{
	ft_putstr(GREEN);
	ft_putstr("bugra_yeşil\n");
	ft_putstr(RESET);
	ft_putstr("bugra_beyaz\n");
}
```

- C’de parametre olarak fonksiyon kullanma

```c
#include <stdio.h>

int is_pipe(char a) {
	if (a == '|')
		return 1;
	return 0;
}

int checker(char *str, int(*checker)(char)) {
	int i = 0;
	while (str[i++])
		if (checker(str[i]) == 1)
		{
			printf("pipe var\n");
			return 1;
		}
	printf("pipe yok\n");
	return 0;
}

int main() {
	char *a = "bugrahan";
	char *b = "kara|molla";
	checker(a, &is_pipe);
	checker(b, &is_pipe);
}
```

- bir pointeri şöyle ilklendirmek hatalıdır

```c
char *a = malloc(10);
a = "bugra";
printf("%s\n", a); // bugra
```

- 

---