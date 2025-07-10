# makefile notları

- [ ]  [https://makefiletutorial.com/#static-pattern-rules](https://makefiletutorial.com/#static-pattern-rules)
- [ ]  [https://noahloomans.com/tutorials/makefile/](https://noahloomans.com/tutorials/makefile/)
- [ ]  [https://www.gnu.org/software/make/manual/make.html](https://www.gnu.org/software/make/manual/make.html)

---

- Makefile birden çok dosyayı kolayca derlememizi sağlayan Make tekniklerinden en çok bilinenidir. genelde c/cpp için kullanılır. GNU Make olarak geçer ve Linux&Mac’te kullanılır. muadilleri CMake, SCons, Bazel ve Ninja’dır. python ve js gibi diller derlenmedikleri için makefile kullanmazlar.
- Makefile isimli bir dosyaya derleme komutları yazılarak yapılır. make uygulaması çalıştırıldığında, bulunulan dizinde sırasıyla GNUmakefile, makefile ve Makefile dosyalarını arar. yani bu üç isimden birini de kullanabilirsin. yani makefile ve Makefile isimli iki dosyan varsa önce makefile kontrol eder varsa onu çalıştırır. ayrıca -f seçeneği ile Makefile olarak kullanacağınız dosyayı da belirlememiz mümkün (make -f <dosya>)
- **`make -v`** bilgisayarındaki make sürümünü gösterir
- **`make -n**`  derleme işlemi yapmadan derleme sonucunu gösterir
- mesela bir klasörde

```makefile
- folders/
	* deneme.c
	* deneme2.c
	* deneme.h
```

dosyaların var. bunları derlemek ve tek bir output dosyasına yazdırmak için 

```makefile
	gcc -o deneme deneme.c deneme2.c -I.
```

demen gerekirdi. bunları make ile çok daha kolay bir yolla derleyebiliriz: 

```makefile
all: deneme.c deneme2.c
	gcc -Wall -Werror -Wextra -o deneme deneme.c deneme2.c
# ${CC} ${CFLAGS} -o ${NAME} ${SRCS}
```

bu makefile’ı biraz daha geliştirelim: 

- The variables set with`:=` are always set unconditionally. Variables set with `?=` are only set if it hasn’t been set already.
- makefile büyük ölçüde kurallardan oluşur.

```makefile
all: name
	gcc name -o my_name
```

Makefile’da commandları yazarken **`tab`** ile indentlemelisin aksi taktirde çalışmazlar. aslında bunun da bir work-around’ı var. o da .RECIPEPREFIX’i değiştirerek: 

```makefile
.RECIPEPREFIX = >
all:
>@echo Hello, world
```

- makefile hello world yazdırma

```makefile
hello:
	@echo Hello, World
```

- bağımlılk (dependency) nedir?

```makefile
ilk_kural : ilk_bagimlilik
	ilk_komut
ikinci_kural : ikinci_bagimlilik
	ikinci_komut
ücüncü_kural :
	ücüncü_komut
```

- örnek:

```makefile
# makefile'da commentler # ile başlar
hello:
	echo "Hello, World"
	echo "This line will always print, because the file hello does not exist."
```

- relink: her make dediğinde kodun yeniden makelenmisidir, hatalıdır. mesela bir tane deneme.c dosyamız olsun ve şöyle bi makefile

```makefile
deneme:
	cc deneme.c -o deneme
```

fakat bu sefer de deneme.c’nin içeriğini değiştirdikten sonra make dersek makefile tekrar çalışmaz çünkü ona göre zaten deneme isimli bir dosya mevcut. bunu `deneme` kuralına bir bağımlılık atayarak çözebiliriz: 

```makefile
deneme: *deneme.c*
	cc deneme.c -o deneme
```

bunu bir başka örnekte de görelim. mesela şöyle bi makefile’ımız var 

```c
NAME = result
CC = gcc
FLAGS = -Wall -Werror -Wextra
SOURCES = a.c b.c main.c
OBJECTS = $(SOURCES:.c=.o)

all: $(NAME)

$(NAME): $(OBJECTS)
	$(CC) $(FLAGS) $(OBJECTS) -o $(NAME)

clean:
	rm -rf $(OBJECTS) $(NAME)

PHONY = all clean re fclean
```

```c
NAME = result
CC = gcc
FLAGS = -Wall -Werror -Wextra
SOURCES = a.c b.c main.c
OBJECTS = $(SOURCES:.c=.o)

all: $(OBJECTS)
	$(CC) $(FLAGS) $(OBJECTS) -o $(NAME)

clean:
	rm -rf $(OBJECTS) $(NAME)

PHONY = all clean re fclean
```

- `make clean` komutu dosya silmek için kullanılan kurala verilen isimdir. başka bir isim de verebilirsin

```makefile
clean:
	rm -rf *.o *.c *.cpp
```

- makefile’da yalnızca string değişkenler tanımlayabilirsin. **`:=`** ya da **`=`** kullanılır

```markdown
files := file1 file2

deneme: ${files}
	@echo these are variables: ${files}
 	@touch deneme

file1:
	@touch file1
file2:
	@touch file2
clean:
	rm -rf file1 file2 deneme
```

- **`:=`** ve **`=`** farkı:

```bash
# := ile bir kere tanımlarsan daha sonra değişmez
NAME := program
NAME := dosya
all:
    @echo $(NAME)  # program kaldı

# = ile değişir
NAME = program
NAME = dosya
all:
    @echo $(NAME)  # dosya oldu
```

- tanımladığın değişkenlere variable expansion uygulamak istiyosan **`${}`** ya da **`$()`** işaretini kullanmalısın:

```makefile
a := hi

deneme:
	@echo ${a}
	@echo $(a) # recommended bc also works with nmake (windows make)
	@echo $a   # works too but not recommended
```

- sadece **`make`** dersen makefile’da gördüğü top-to-bottom ilk kuralı çalıştıracaktır. bu ilk kurala genelde **`all`** ismi verilir

```makefile
all: one two three
one:
	touch one
two:
	touch two
three:
	touch three
```

- double :: → double colon kullanımı bir kuralı birden fazla kez tanımlayabilmene yarar

```makefile
all: greet

greet:: 
	@echo "hello"

greet::
	@echo "hello again"
```

- kuralların altına yazdığın komutlar çalıştıklarında onları çalıştıran satır da ekrana yazdırılır.  bunu engellemek için başlarına @ koyabilirsin

```makefile
all:
	@echo "only this message will be printed"
	echo "but this is different, isn't it?"
```

- makefile komutlarında linux komutlarını kullanabilmek istiyosan `arasına` yazmalısın.

```makefile
all:
	@echo `pwd` 
```

kuralların her bir satırı ayrı ayrı çalıştırılan shell komutları gibidir. o yüzden birinci komut satırında tanımladığın bir değişken bir alttakinde geçerli olmaz:  

```makefile
hi:
	export myAge=30
	@echo "myAge=[$myAge]"
```

çalışmaz. fakat aynı satırda olmak şartıyla başka komutlar da ekleyebilirsin:

```makefile
all: 
	cd ..
	@echo `pwd` # this won't work bc it is on different lines. however

	cd ..; @echo `pwd` # this, will work
```

- default shell `/bin/sh` dizinidir. bash’e değiştirmek istiyosan şunu ekle

```makefile
SHELL=/bin/bash
```

- uzun satırları `\` ile bölebilirsin

```makefile
some_file: 
	echo This line is too long, so \
		it is broken up into multiple lines
```