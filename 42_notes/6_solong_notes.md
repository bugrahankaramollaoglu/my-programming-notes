# 6 - so_long

kaynaklar

- [**https://harm-smits.github.io/42docs/libs/minilibx](https://harm-smits.github.io/42docs/libs/minilibx)**
- [**https://github.com/berkayinam/howcanido/blob/master/So_longREADME.md](https://github.com/berkayinam/howcanido/blob/master/So_longREADME.md)** (berkay inam mlx)
- [**https://eastmanreference.com/completelistofapplescriptkeycodes**](https://eastmanreference.com/completelistofapplescriptkeycodes%5D(https://eastmanreference.com/completelistofapplescriptkeycodes))
- [**https://github.com/terryyes/mlx_example**](https://github.com/terryyes/mlx_example)
- https://github.com/keuhdall/images_example
- [**https://github.com/madebypixel02/so_long](https://github.com/madebypixel02/so_long%5D(https://github.com/madebypixel02/so_long))**
- [**https://github.com/SLucasSerrano/so_long**](https://github.com/SLucasSerrano/so_long%5D(https://github.com/SLucasSerrano/so_long))
- https://github.com/qst0/ft_libgfx
- [https://medium.com/@erenakbas6157/ecole42-so-long-detaylı-anlatım-türkçe-7f9949b3986e](https://medium.com/@erenakbas6157/ecole42-so-long-detayl%C4%B1-anlat%C4%B1m-t%C3%BCrk%C3%A7e-7f9949b3986e)

**`STUDY LIST IN SO_LONG`**

- [ ]  mlx kütüphanesi, basitçe kullanımı
- [ ]  structlar
- [ ]  davut abi so_long pdf’i
    
    [So_long_hucreler_arasında_yol_bulma.pdf](6%20-%20so_long%20e78ef89c23ac432f9491a68f8d1565ed/So_long_hucreler_arasnda_yol_bulma.pdf)
    
- [ ]  so_long’da valid_map, flood fill olayı
- [ ]  2boyutlu string nedir nasıl okunur (nested while ile)
- [ ]  
- structs in c: structlar c’de birden fazla türde değişken tutan tek bir veri yapısı gibi düşünülebilir. nasıl yaratılır?

```c
struct myStruct {
	int num;
	char myLet;
};
```

kullanmak için bu struct tipinde bir eleman yaratmalısın. daha sonra bu elemana ulaşmak için (.) operatörünü kullanıyosun: 

```c
struct myStruct {
	int myNum;
	char myLet;
};

int main() {
	struct myStruct s1;

	s1.myNum = 30;
	s1.myLet = 'a';

	printf("my num is: %d\n", s1.myNum);
	printf("my letter is: %c", s1.myLet);
}
```

eleman yaratmanın kısa yolu 

```c
struct myStruct {
	int myA;
	float myB;
} eleman1, eleman2;
```

```c
struct myStructure {
  int myNum;
  char myLetter;
  char myString[30]; // String
};

int main() {
  struct myStructure s1;

  // Assign a value to the string using the strcpy function
  strcpy(s1.myString, "Some text");

  // Print the value
  printf("My string: %s", s1.myString);

  return 0;
}
```

Just insert the values in a comma-separated list inside curly braces {}. Note that you don't have to use the strcpy() function for string values with this technique: 

```c
// Create a structure
struct myStructure {
  int myNum;
  char myLetter;
  char myString[30];
};

int main() {
  // Create a structure variable and assign values to it
  struct myStructure s1 = {13, 'B', "Some text"};

  // Print values
  printf("%d %c %s", s1.myNum, s1.myLetter, s1.myString);

  return 0;
}
```

struct elemanlarını birbirine kopyalayabilirsin: 

```c
struct myStructure s1 = {13, 'B', "Some text"};
struct myStructure s2;

s2 = s1;
// s2 is now copy of s1
```

pointerlar kullanma: 

```c
struct point {
   int x;
   int y;
};
struct point my_point = { 3, 7 };
struct point *p = &my_point;  /* p is a pointer to my_point */
(*p).x = 8;                   /* set the first member of the struct */
p->x = 8;                     /* equivalent method to set the first member of the struct */
```

struct elemanlarına ulaşmanın 2 yolu vardır

- nokta operatörü ( . )
- pointer operatörü ( → )

typedef: veri tiplerine alias atamak için typedef keywordünü kullanıyoruz. şu 2si aynı koddur 

```c
struct Distance{
  int feet;
  float inch;
};

int main() {
  struct Distance d1, d2;
}

// and

typedef struct Distance {
  int feet;
  float inch;
} distances;

int main() {
  distances d1, d2;
}
```

iç içe de struct yazabilirsin: 

```c
struct arabalar {
	int model;
	float km;
};

struct arabam {
	struct arabalar honda;
	int arabamın_modeli;
} benim_arabam;

benim_arabam.honda.model = 2005;
```

- mlx'i başka bilgisayarlarda kullanmak:
    - Linux: # include "minilibxlinux/mlx.h"
        
        gcc -framework OpenGL -framework AppKit mlx/libmlx.a a.c
        
    - Macos: # include "minilibxmacos/mlx.h"
    
    linux’ta: 
    
    1) Derleme almak için ilk önce minilibxlinux içinde iken 'make' çekin kütüphane kendisini derleyerek bir çıktı verecek: 'libmlx.a'
    
    2) Kendi projenizde derleme almak için ise ilk önce kendi c dosyalarınız sonra 'libmlx.a' dosyasının konumu ve ardından şu bayrakları ekleyin: 'lXext lX11 lm lz' 
    Örnek: gcc *.c ./minilibxlinux/libmlx.a lXext lX11 lm lz* 
    
    macte: 
    
    1) Derleme almak için ilk önce minilibxmacos içinde iken 'make' çekin kütüphane kendisini derleyerek bir çıktı verecek: 'libmlx.a'
    
    2) Kendi projenizde derleme almak için ise ilk önce kendi c dosyalarınız sonra 'libmlx.a' dosyasının konumu ve ardından şu bayrakları ekleyin: 'framework OpenGL framework AppKit' Örnek: gcc *.c ./minilibxmacos/libmlx.a framework OpenGL framework AppKit*
    

mlx komutları ne yapıyor?

- mlx_init() -> ekran ve yazılım arasında bağlantı kurar
- mlx_new_window -> ekranda yeni pencere oluşturur. size_x kadar genişlik size_y kadar yükseklik parametresi alır. title pencerenin başlığını belirler. hata durumunda null döndürür.
- mlx_clear_window -> pencereyi siyaha boyar.
- mlx_destroy_window -> pencereyi kapatır
- mlx_pixel_put -> x ve y koordinatına color rengini çizer. (0, 0) noktası ekranın sol üst köşesidir. mlx_ptr parametresi mlx_init'i, win_ptr parametresi mlx_new_window'u alır.
- mlx_string_put -> ekrana string yazdırmamızı sağlıyor.
- mlx_new_image -> bellekte yeni bir görüntü oluşturur.
- mlx_put_image_to_window -> oluşturulan görüntüyü ekrana bastırır.
- mlx_destroy_image -> verilen görüntüyü siler (img_ptr).
- mlx_loop -> program içindeki verileri görüntülemek için kullanılır. klavye ve fareden komut alabilir. veri döndürmez mlx_ptr ile çalışır.
- mlx’te kullandığımız resimler esasında char pointerları yani stringlerdir. 1 resim = char pointer. resmimizin her pikseli sol üst köşeden (ekranın 0,0 noktası) birbiri ardına yerleştirilir. ilk satır bitince alt satıra geçer ve böyle devam eder. her piksel 4 chardır. mesela 800x600 bir ekranda 800.600’den 480000 piksel vardır.  onu da 4le çarpınca char sayısını buluruz.why 4 chars for one pixel ? Simple ! The 3 first chars are representing the color of the pixel through RGB values going from 0 to 255. The 4th pixel is the alpha, yani saydamlık.
- To read from a file to a image object, you need either the XMP or PNG format. In order to read we can call the functions `mlx_xpm_file_to_image` and `mlx_png_file_to_image` accordingly. Do mind that mlx_png_file_to_image currently leaks memory. Both functions accept exactly the same parameters and their usage is identical.
- leak yer ayrılmış bir char stringini free’lemediginde oluyor. segfault ise erişim iznin olmayan bir yere erişmeye çalıştığında. leak’leri şöyle kontrol ediyosun

```c
system("leaks a.out");
```

     segfault’u ise lldb ile yapabilirsin  

```c
lldb ./a.out ve sonrasında r'ye basarak bakabilirsin
```

- so_long check list
    - [ ]  map must be rectangular (including square)
    - [ ]  dış duvarları 1 ile kaplı olmalı
    - [ ]  sadece 10PEC karakterlerinden oluşmalı. C’nin sayısı 1+, P ve E’nin 1 olmalı.
    - [ ]  harita .ber uzantılı olmalı
    - [ ]  haritada satır arası boşluk olmamalı
- resimleri nasıl ekliyoruz?
    - istediğimiz bir resmi (player, collectible, background, exit) jpg/png vs. formatta indiriyoruz
    - resize sitesinden 64x64 haline getiriyoruz [https://www.simpleimageresizer.com/](https://www.simpleimageresizer.com/)
    - background’ını kaldırıyoruz [https://www.remove.bg/upload](https://www.remove.bg/upload)
    - xpm’e çeviriyoruz [https://convertio.co/png-xpm/](https://convertio.co/png-xpm/)
    - bu kadar, sonra da images/ ‘e atip kullaniyoruz
    
    ---