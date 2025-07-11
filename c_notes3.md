# deitel - how to program c notları

- ram: random access memory
- cpu: diğer bölümlerin işbölümünü ayarlayıp düzenler. input ünitesine hangi verilerin ram'e yazılacağını ve output ünitesini hangi verilerin hafızadan okunacagını söyler.
- bytes hieararchy (each x1024):
    - kilobyte
    - megabyte
    - gigabyte
    - terabyte
    - petabyte
    - exabyte
    - zettabye
- ascii: american standard code for information interchange
- A database is a collection of data organized for easy access and manipulation. The most popular model is the relational database, in which data is stored in simple tables. A table includes records and fields. For example, a table of students might include first name, last name, major, year, student ID number and grade point average fields. The data for each student is a record, and the individual pieces of information in each record are the fields.
- programlama dilleri genel hatlarıyla 3e ayrılabilir
    - machine languages
    - assembly languages
    - high-level languages
- C kendinden önceki iki dilden ilham aldı, BCPL ve B. Bell laboratuarlarında çalışan Denis ritchie tarafından 72de C yazıldı. farklı versiyonları var like C11 (2011), c99 (1999) vs. c++ was developed by Bjarne Stroustrup
- microsoft'un 3 temel OOP dili var
    - Visual Basic (inspired from Basic)
    - Visual C++ (inspired from C++)
    - Visual C# (inspired from C# and Java)
- swift 2014'te yaratıldı.
- bir C kodu nasıl çalışır
    - programcı editörde kodu yazar ve bilgisayar önce onu diske kaydeder
    - preprocessor program processes the code
    - derleyici .o uzantılı obje dosyalarını oluşturur .c'lerin ve diske kaydeder
    - linker obje kodlarını kütüphenelere bağlar, creates an excutable file ve diske kaydeder
    - loader programı (executable file) hafızaya kaydeder
    - cpu bu hafızadaki programı çalıştırır
- standart bir linux sisteminde derleme komutu gcc (gnu c compiler)'dır.
- escape characters
    - \n --> newline
    - \a --> alarm: produces sound or visible alert
    - \t --> tab
    - \\ --> inserts a backslash (\)
    - \" --> double quote
- casings
    - thisIsCalledCamelCasing
    - this_is_called_snake_casing
    - this-is-called-kebab-casing
    - ThisIsCalledPascalCasing
- tek argümanli printf() olacaksa onun yerine puts() tavsiye edilir. puts() ayrıca sonuna newline ekler.
- Function printf always begins printing where the cursor is positioned, and this may be anywhere on a line of the screen.
- % (mod) sadece integerlarla kullanılabilir
- A float has 7 decimal digits of precision and occupies 32 bits . A double is a 64-bit IEEE 754 double-precision floating-point number. 1 bit for the sign, 11 bits for the exponent, and 52 bits for the value. A double has 15 decimal digits of precision and occupies a total of 64 bits. Double is more precise than float and can store 64 bits, double of the number of bits float can store. Double is more precise and for storing large numbers, we prefer double over float.
- Defining a function inside another function is a syntax error.
- return 0'daki 0 programın başarıyla calıstıgını gostererek bitiriyor.
- stack yapıları bulaşık kulesi gibidir üstten alınır üste koyulur. bu özelliğiyle LIFO (last item in first item out) olarak bilinir. function call stack yapısı fonksiyonların çağrılması/return etmesinde kullanılır.
- In many programming languages, there are two ways to pass arguments—pass-by-value and pass-by-reference. When arguments are passed by value, a copy of the argument’s value is made and passed to the called function. Changes to the copy do not affect an original variable’s value in the caller. When an argument is passed by reference, the caller allows the called function to modify the original variable’s value. Pass-by-value should be used whenever the called function does not need to modify the value of the caller’s original variable. This prevents the accidental side effects (variable modifications) that so greatly hinder the development of correct and reliable software sys- tems. Pass-by-reference should be used only with trusted called functions that need to modify the original variable. In C, all arguments are passed by value.
- Function rand actually generates pseudorandom numbers. Calling rand repeatedly produces a sequence of numbers that appears to be random. However, the sequence repeats itself each time the program is executed. Once a program has been thoroughly debugged, it can be conditioned to produce a different sequence of random numbers for each execu- tion. This is called randomizing and is accomplished with the standard library function srand. Function srand takes an unsigned int argument and seeds function rand to pro- duce a different sequence of random numbers for each execution of the program.
- Keywords extern and static are used in the declarations of identifiers for variables and functions of static storage duration. Identifiers of static storage duration exist from the time at which the program begins execution until the program terminates. For static variables, storage is allocated and initialized only once, before the program begins execution. For func- tions, the name of the function exists when the program begins execution. However, even though the variables and the function names exist from the start of program execution, this does not mean that these identifiers can be accessed throughout the program. Storage du- ration and scope (where a name can be used) are separate issues, as we’ll see in Section 5.13. There are several types of identifiers with static storage duration: external identifiers (such as global variables and function names) and local variables declared with the storage- class specifier static. Global variables and function names are of storage class extern by default. Global variables are created by placing variable declarations outside any function definition, and they retain their values throughout the execution of the program. Global variables and functions can be referenced by any function that follows their declarations or definitions in the file. This is one reason for using function prototypes—when we include stdio.h in a program that calls printf, the function prototype is placed at the start of our file to make the name printf known to the rest of the file.

### arrays

- an array is a group of contiguous memory locations that are of the same data type.
- array hafızada yer tuttugundan dolayı `int array[3]` diyerek initialize etmemiz gerekiyor ki bilgisayar `sizeof(int)*3` kadar yer ayırsın.
- arrayleri de ; diyip bırakırsan garbage value atanır otomatik olarak.
- int n[10] = {0} diyerek ilk elemanı 0'a initialize etmek kalan elemanları da 0'a initialize eder. array'i initialize etmemek genellikle hatadır.
- int n[] = {1, 2, 3,} diyerek 3 elemanlı bir array de oluşturabilirsin
- #define SIZE 5 diyerek symbolic constant değişken tanımlamış olursun. bundan sonraki her SIZE kullandığında C onu 5 olarak anlayacaktır. bunun faydası daha sonra array'in size'ını değiştirmek istediğinde direkt en üstte tek bir satırı (SIZE 5) değiştirmen yeterli oluyor, diğer türlü diğer bütün 5leri silip yeni değer yazmak zorundasın.
- örnek:

```c
#include <stdio.h>
#define SIZE 10
int main()
{
	int n[SIZE] = {1, 2, 3, 50, 60, 40, 23, 24, 300, 10};
	int sum = 0;
	for (int i = 0; i < SIZE; ++i)
		sum += n[i];
	printf("sum of n array is: %d", sum);
}
```

- stringler yani "abcd" gibi veri tipleri esasında veri tipi char olan arraylerden başka bir şey değildir. şöyle deklare edilirler:

```c
char str[] = "bugra";
```

bu ifade b u g r ve a char'larını str arrayinin sırasıyla 0. 1. 2. 3. ve 4. indislerine atar sonuna da \0 koyar. yani aslında şöyledir: 

```c
**char str[] = {'b', 'u', 'g', 'r', 'a', '\0'};**
```

- scanf() ile string'lerin kullanımı:

```c
int main()
{
	printf("enter a num:");
	char *num = malloc(10); // ya da
//char num[10];
	scanf("%5s", num);
	printf("your num is: %s\n", num);
}
```

- statik lokal değişkenler hafızada yer tutar ve normal tanımlanan değişkenlerden farklıdır. mesela

```c
int fun()
{
	int nb = 3;
	nb++;
	return nb;
}

int main()
{
	printf("%d ", fun());
	printf("%d ", fun());
	printf("%d ", fun());
}
```

- bir array tanımladıktan sonra hafızada
    - array
    - &array
    - &array[0]

ifadeleri aynı anlama gelir pointer aritmetiği yapmadığın sürece (aynı hafıza adresine sahiptirler)

- difference between **`pass by value`** and **`pass by reference`**: in a pass by value, the parameter value copies to another variable while, in a pass by reference, the actual parameter passes to the function. yani referensıyla gönderdiğinde adresini gönderiyosun, değeriyle gönderdiğinde kopyasını gönderiyosun. o yüzden pbr asıl değişkeni değiştirirken pbv değiştirmiyor.

```c
// pass by value
void fun(int nb)
	nb += 10;

int main()
{
	int a = 5;
	fun(a);
	fun(a);
	printf("a: %d\n", a); >>> 5 DEĞER DEĞİŞMEDİ
}

// pass by reference
void fun(int *nb)
	*nb += 10;

int main()
{
	int a = 5;
	fun(&a);
	fun(&a);
	printf("a: %d\n", a); >>> 25 DEĞER DEĞİŞTİ
}
```

örnek2: pbv vs. pbr farkını gördüğümüz bir başka güzel örnek de swap() işlemidir: 

```c
// PASS BY VALUE
int swap(int a, int b) {
	int tmp;
	temp = a;
	a = b;
	b = a;
}
swap(x, y);  >>> swap işlemi uygulanmaz

// PASS BY REFERENCE
int swap(int *a, int *b) {
	int tmp;
	tmp = *a;
	*a = *b;
	*b = tmp;
}
swap(&x, &y); >>> swap işlemi gerçekleşir
```

- adding const to something, in our case before an array means that this array cannot be modified later on. değiştirmeye çalışmak compile error verir.
- we'll discuss two searching methods in arrays:
    - linear search: teker teker arama
    - binary search: devamlı yarıya bölerek aranan şeyin mevcut oldugu yarıda aramaya devam etme
- arrays can be multi-dimensional. for instance 3-by-4 array has 3 rows and 4 columns.
    
    ![mesela myArr[3][2] demek 3. satırın 2. sütununa denk gelen eleman demektir.](deitel%20-%20how%20to%20program%20c%20notlar%C4%B1%207089d02d07ce4378b28c6a662c3c657f/image1.jpg)
    
    mesela myArr[3][2] demek 3. satırın 2. sütununa denk gelen eleman demektir.
    
- how to initialize a multidimensional array?

```c
int a[2][2] = {{1,2}, {3, 6}};
```

- For each array you’ve defined so far, you’ve specified its size at compilation time. But what if you cannot determine an array’s size until execution time? In the past, to handle this, you had to use dynamic memory allocation. For cases in which an array’s size is not known at compilation time, C has variable-length arrays (VLAs)—that is, arrays whose lengths are defined in terms of expressions evaluated at execution time.
- printf outputs a string by reading characters from the beginning of the string in memory and continuing until it encounters the string’s '\0'. If the '\0' is missing, printf continues reading from memory until it encounters some later '\0' in memory. This can lead to strange results or cause a program to crash.
- The C11 standard’s optional Annex K provides new, more secure, versions of many string-processing and input/output functions. When reading a string into a character array function scanf_s performs additional checks to ensure that it does not write beyond the end of the array.

### pointers

- pointer are basically variables whose values are pointer addresses.Normally, a variable directly con- tains a specific value. A pointer, however, contains an address of a variable that contains a specific value.

```c
int a = 10;
int *ap = &a;
printf("%p\n", ap);  >>> 0x7ffec7d4fd6c
printf("%d\n", *ap); >>> 10
```

adres alma operatörü & ile yapılır. başına geldiği değişkenin hafızada tutuldugu adresi çeker.

değer alma operatörü * ile yapılır. başına geldiği pointerın işaret ettiği değişkenin değerini çeker.

- pointer yaratırken initialize etmelisin.
    - ya bi adrese
    - ya 0'a
    - ya NULL'a
- bir array oluşturduktan sonra o arrayin ismi artık &array[0] ile aynı şey haline gelir:

```c
int ar[] = {1,2,3};
int *arPtr = &ar;
// artık -> ar = *arPtr = &ar[0]
```

![](deitel%20-%20how%20to%20program%20c%20notlar%C4%B1%207089d02d07ce4378b28c6a662c3c657f/image2.png)

- In conventional arithmetic, 3000 + 2 yields the value 3002. This is normally not the case with pointer arithmetic. When an integer is added to or subtracted from a pointer, the pointer is not incremented or decremented simply by that integer, but by that integer times the size of the object to which the pointer refers. neden çünkü ramde bir değişken depolanırken bitlere o değişkenin tipinin boyutu kadar yer ayırıyor. mesela bir **`int ar[] = {10,20,30};`** değişkeni olsun. bu değişkenin tutulduğu adres değerinin başlangıcı yani ar[0] da 0x12050 numaralı adreste olsun. bu durumda ar[1] 0x12054, ar[2] 0x12058 nolu adreste tutulur çünkü int 4’er 4’er artar.
- fonksiyon prototiplerinde kullanacagin const kelimesi sayesinde o parametrenin fonksiyon içinde modifiye edilememesini sağlayabilirsin. böylelikle değiştirilmeye çalışıldığında derleyiciye bağlı olarak hata ya da uyarı mesajı döndürecektir. There are four ways to pass a pointer to a function:
    - a non-constant pointer to non-constant data In this case, the data can be modified through the dereferenced pointer, and the pointer can be modified to point to other data items.
    
    ```c
    char str[] = "asfasd";
    char *sPtr = &str;
    int func(char *sPtr);
    ```
    
    - a constant pointer to nonconstant data : it always points to the same memory location, and the data at that location can be modified through the pointer.
    
    ```c
    char str[] = "bugra";
    const char *strPtr = &str;
    ```
    
    - a non-constant pointer to constant data : A non-constant pointer to constant data can be modified to point to any data item of the appropriate type, but the data to which it points cannot be modified. Such a pointer might be used to receive an array argument to a function that will process each element without modifying that element:
    - a constant pointer to constant data.
- bir arrayin eleman sayısını bulmanın yolu

```c
int len = sizeof(arr) / sizeof(arr[0]);
```

- a pointer can only be assigned to another pointer only if they share the data type. exception to this rule is void pointers (void *). a void pointer can be assigned to any integer of any type. however, they cannot be dereferenced like normal pointers. Consider this: The compiler knows that a point- er to int refers to 4 bytes of memory on a machine with 4-byte integers, but a pointer to void simply contains a memory location for an unknown data type—the precise number of bytes to which the pointer refers is not known by the compiler.
- arrayler ve pointerlar zaman zaman birbirlerinin yerine kullanılabilirler. mesela int a[] yerine int *a da diyebilirsin. örnek:

```c
int ar[] = {10, 20, 30};
int *arPtr = &ar;
// arPtr şuan 10'u gösteriyor.
&arPtr[2] = *(arPtr + 2) = arPtr + 2 = 30;
```

- arraylerle pointerları kullanmanın bir yolu 2D string arrayler oluşturmaktır

```c
char *a[2] = {"bugra", "kara"};
```

burada her bir eleman aslında string değil char arrayin adresini tutar.

- a pointer to function contains the *address* of the function in memory. daha önce bir arrayin isminin arrayin ilk elemanın adresi oldugunu görmüstük. benzer bir şekilde fonksiyon ismi de hafızada fonksiyonun tutuldugu yerin ilk adresini verir. mesela

```c
int (*fun)(int a, int b);
```

int return eden, 2 int'i parametre olarak alan bir fonksiyonun adresini gösteriyor. parantezler şart çünkü pointer oldugunu söylüyor.