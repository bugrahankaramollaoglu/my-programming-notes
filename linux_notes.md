# linux notları

- kernel işletim sisteminin kalbi, yani çekirdeği çalıştıran bir programdır. bütün diğer programlar buna bağlıdır ve her şeye izni vardır.
- kernele shell yani kabuklar üzerinden erişiyoruz. system call üzerinden çalışır. en yaygını bash’tir. hangi shelli kullandıgını ögrenmek icin

```bash
echo $SHELL
```

- bir ortam değişkeni olan PATH nedir?

```bash
echo $PATH # /home/bugra/perl5/bin:/home/bugra/.local/bin:
# /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:
# /bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin:/home
# /bugra/flutter/bin:/home/bugra/.fzf/bin
```

path’e bir dizin eklemek için 

```bash
PATH=$PATH:/usr/local/newCommand
```

- ortam değişkenlerini görmek için

```bash
printenv
env
```

to change the value of an environment variable

```bash
export VAR_NAME=newVal
```

- you can separate commands with `;` to use respectively

```bash
ls; ls-l; clear; pwd; clear
```

you can separate commands with `&&` to execute respectively (right-command works only left-one executed successfully)

```bash
git add . && git commit -m "asd" && git push
```

you can separate commands with `||` to execute respectively (right-command works only left-one executed unsuccessfully) 

```bash
rm myDir || echo "did not work"
```

- to see the details of a command use

```bash
cat --help # or
man cat
```

man kullanırken flagler

```bash
man1 # general user programs
man2 # system programs
man3 # library functions (related to C)
```

bir komutun tüm türevlerini aratmak için 

```bash
man -k strl

# strlcat (3bsd)       - size-bounded string copying and concatenation
# strlcpy (3bsd)       - size-bounded string copying and concatenation
# strlen (3)           - calculate the length of a string 
```

to update man database, say 

```bash
mandb
```

- to see your linux distro

```bash
uname -v # -a shows everything about kernel
lsb_release -a
cat /etc/*release # more detailed
```

- to see calendar and time

```bash
cal # shows current date
cal 2023 # shows 2023
cal 5 2001 # shows may 2001

date
```

- to see the name of your computer

```bash
hostname
whoami
```

- to see for how long computer has been running

```bash
uptime
```

- to see the directory of a command

```bash
which cat
```

- diskleri görmek için

```bash
df -h
```

- to see ram usage

```bash
free -m
```

- to see all your previous commands

```bash
history

# to see the last 5 commands
history 5 # for bash. use -5 in sh)

# later you may use command number like this for easy access
!1040

# you may use !! to access your last used command
!!
```

- to do reverse of what cat does

```bash
tac file
```

- to reverse each line

```bash
rev file
```

- to sort

```bash
sort file
```

- to count words

```bash
wc file
```

- to compare two files

```bash
diff file1 file2
diff3 file1 file2 file3 # to compare three files
```

- to execute a command, use

```bash
find /home/bugra/Desktop -name *.cpp -exec rm {} \;
```

- benzer bir şeyi xargs ile yapabilirsin. xargs kendisine girdi olarak verilen verileri tek tek kendisinden sonraki komuta argüman olarak verir

```bash
find /home/bugra/Desktop -name "*.cpp" | xargs ls -l
ls .*c | xargs -p rm
```

- to zip multiple files

```bash
tar -cf myTar.tar file1 file2 file3 # create .tar file
tar -xvf myTar.tar # unzip .tar file
```

- password change

```bash
passwd
```

- add and see user(s)

```bash
adduser
useradd

users
```

- remove user

```bash
deluser bugra
```

- to see processes use

```bash
ps -e 
pstree -p # for tree syntax with PIDs
```

- crontab: belli sürelerde skriptler çalıştırmanı sağlar. `crontab -e` ile giriş yapabilirsin

```bash
#!/bin/bash

# This script simply appends the current date and time to a log file
echo "Script executed at $(date)" >> ./Desktop/date.log
```

```bash
#!/bin/bash

while true; do
    # Add the command to run your script here
    ./Desktop/test.sh

    sleep 30
done
```

```bash
* * * * * /path/to/test_script.sh
```

- `service` komutuyla servislere erişiriz

```bash
service --status-all
```

```bash
service bluetooth status
service bluetooth stop
service bluetooth start
service bluetooth restart
```

- linuxta 0-6 arası 7 tane çalışma seviyeleri vardır. örneğin 0 seviyesi hiçbir programın çalıştırılmadıgı evre, 6reboot evresi, 3 çok kullanıcılı çalışma evresi vs. mesela init 0 bilgisayarı kapatır çünkü 0 seviyesine indirir. init 6 == reboot vs.
- `shutdown -h now` bilgisayarı o an kapatır, `shutdown -h now+10` 10 dakika sonra kapatır.
- redhat, centos ve fedora paket yükleyicisi olarak `rpm` ve `yum` kullanırken ubuntu ve debian `deb` ve `apt` kullanır. mesela bir .deb dosyası indirdik ve bunu kurmak istiyoruz, şöyle kurarız

```bash
dpkg -i asd.deb
```

- terminalde çalışmak risklidir çünkü explorer gibi ctrl+z yapamazsın. dosyalar direkt silinir.
- 2 tane temel unix shell’i vardır. shell ve bash. tüm shell’ler sh da denen bourne shell’den doğmadır. kurucusu steve bourne.
- linux satırının başında `$` işareti standart kullanıcı olarak giriş yaptığını gösterir. `#` ise root olarak varsındır demektir. `~` işareti o an home klasöründesindir demektir.
- gizli dosyalar `.` ile başlar.
- inode nedir? ls -li
- muhtelif kodlar

```bash
find . -type f ! -name “.cpp” -delete
```

```bash
i=1; for i2 in "*.py"; do mv "$i2" "$i.py"; ((i++)); done
```

```bash
for i in {1..20}; do touch "$i.c"; done
```

```bash
cat file | tail -n 5
```

```bash
cat file | head -n 5
```

```sql
find . -delete
```

```bash
find . -type f -name "*.doc" -exec rm {} \;
```

```bash
cat file | grep "CAT"
```

```bash
find . -type f | wc -l
```

```bash
echo {1..10}; tr ' ' ','
```

```bash
find . -name "*.txt" -exec sed -i '/my password: bugra55/d' {} \;
```

```bash
awk '{ sum += $1 } END { print sum }' file.txt
# \n ile değil ; ile ayrılmışlarsa awk + -F'n' ile spesifik ayraç verebilrsin 
awk -F';' '{ sum += $1 } END { print sum }' file.txt
```

```bash

```

- curl metodu ile bir komutun cheatsheetine ulaşabilirsin

```markdown
# curl cheat.sh/grep
# curl cheat.sh/cat
# curl cheat.sh/mv ...
```

- what is stderr and stdout? stdout is used to display the regular output of a program, which may include text, numbers, or other data. This output can be redirected to a file or piped to another program for further processing. stderr is used to display error messages or other diagnostic information that is generated by a program. This output is typically displayed in the terminal window where the program is running, and can also be redirected or piped like stdout.
- `-` ile başlayan bir dosya yaratamazsın. yaratmak için başına `--` getirmelisin

```markdown
# create -asd 
touch -- -asd
mv ./-asd ./- (artık - isminde dosyan oldu)

# read -
cat < -
```

- file glob expansions
    - `*` bir türün tüm örneklerini alır
    
    ```markdown
    # .txt ile biten tüm dosyaları listeler
    ls *.txt
    ```
    
    - `?` tek bir örneği alır
    
    ```markdown
    # deneme ile başlayıp bir karakter takip eden .c uzantılı dosyaları alır
    ls deneme?.c (deneme1.c, denemee.c vs.)
    
    # tek karakterli .rs uzantılı dosyaları alır
    ls ?.rs (a.rs, b.rs vs.)
    ```
    
    - `[]` belli bir aralığı alır
    
    ```markdown
    # deneme3-9.c aralığını alır
    ls deneme[3-9].c
    
    # denemea, denemeb'yi alir
    ls deneme[ab]
    
    # a, b ya da c ile başlayıp .txt ile bitmeyenleri alır
    ls deneme[!abc].txt
    ```
    
- `' '` ve `" "` farkı: “ “ ile kullandığın stringlerde $ jokerini kullanabilirsin

```bash
$ name = bugra
$ echo "my name is $name" # my name is bugra
$ echo 'my name is $name' # my name is $name
```

- `hard link` vs. `soft link (symbolic)`: hard link bir dosyanın ya da klasörün filesystem’deki fiziksel yerine gösterilen referanstır. hard linkle yarattığın yeni dosya ya da klasör orijinal olanla aynı data segmentini gösterir. OS için aralarında hiçbir fark yoktur. aynı inode numarasına sahiptir. sembolik link ise o dosyanın dizinine referans gösterir. windowstaki kısayollardır. inode numaraları orijinal dosyadan farklıdır. haliyle hafızada aynı segmenti göstermezler.
- tac → catin tam tersi, içeriği tersten yazdırır
- grep → belli bir pattern arar ve onu bulup verir

```markdown
# şeması
grep [options] [pattern] [file_or_directory]

# mesela bir dosyada bugra kelimesini aratacaksin
sudo cat deneme.txt | grep bugra (ya da)
grep bugra deneme.txt

# bütün dosyalarda aratsin istiyosan
grep "bugra" * (ya da tüm cpp'lerde aratacaksan)
grep "bugra" *.cpp

# -i küçük/büyük harfi ignore etmek istiyosan 
grep -i "bugra" deneme.txt

# birden fazla dosyada da arama yapabilirsin
grep "bugra" deneme.txt deneme2.txt deneme3.txt

# birden fazla kelime aratacaksan (\| kullan) (either of them)
grep "bugra\|cemre" deneme.txt

# kaç satırda bulunduğunu öğrenmek için (-c) kullan
grep -c "bugra" deneme.txt

# kaç satırda bulunmadığını öğrenmek için de (-c -v) kullan
grep -c -v "bugra" deneme.txt

# grep'i pipe'larla da kullanabilirsin
history | grep -c clear # kaç kere clear komutu çalıştırdın

# zip'lerle kullanmak içi (zgrep) kullanmalısın
zgrep pattern_to_search compressed_file

# -C x  x satır altındaki ve üstündeki satirlari alir
man memchr | grep -niC 5 RETURN 
```

- pipe → output yönlendirmeni sağlar

```markdown
# soldakinden gelen şeyi sağdakine atar
first_command | second_command

# bunu uzatadabilirsin, her komutun outputu sağdakine input olarak gider
first | sec | third ...

# genelde grep'le kullanılır
ls | grep 'cmpe'
```

- find → dosya aramanı sağlar. farklı flaglerle kullanabilirsin.

```markdown
# şeması
find [path] [expression]

# -name belli bir isimdeki dosyaları arar
find . -name "*.txt"

# -type belli bir tipteki dosya ya da klasörleri arar
# -f dosyaları, -d klasörleri arar
find . -type f "*.c" (o dizinde .c uzantılı tüm *dosyaları* arar)
find . -type d "dsa" (o dizinde içinde dsa geçen tüm *klasörleri* arar)

# -size belli bir boyuttaki dosyaları arar
find /home -type f -size +1m (/home ve altında 1mb'tan büyük dosyaları arar)

# -empty boş olanları arar
find /etc -type d -empty (/etc ve altında boş klasörleri arar)

# -mtime düzenleme zamanına göre arar
find . -type f -mtime -7 (son 7 günde değiştirilmiş dosyaları arar)

# -delete bulduklarını siler
find . -name ".out" -type f -delete (o dizinde out uzantılı tüm dosyaları siler)

# -perm izinlere göre arar
find . -type -perm 777 (777 izinli tüm dosyaları arar)
```

- cat → dosya yaratmaya, içine yazmaya ve içeriğini yazdırmaya yarar

```markdown
# bir dosyanın içeriğini okur
cat asd.txt

# iki dosyayı birleştirip yazdırır
cat dosya1.odt dosya2.odt

# dosya yaratip içine yazarsın, ctrl+d ile çıkarsın
cat > dosya.txt

# içeriğini silmeden eklemek için
cat >> dosya.txt

# -n ile satır numaralarıyla okursun
cat -n dosya.txt

# sadece ilk 5 satırı okuma
cat dosya.txt | head -n 5

# sadece son 5 satırı okuma
cat dosya.txt | tail -n 5

# sort ile sıralı yazdır
cat asd.txt | sort
```

- rm → basically, removes things

```markdown
# şeması
rm [options] [files/directories]

# removes a single file
rm fileName

# -r klasör ve alt klasörlerini siler (recursively)
rm -r folderName

# -f sormadan siler (force)
rm -rf folder/fileName

# -v sildiklerini yazdirir (verbose)

# belli bir uzantıyı silme
rm *.cpp (cpp uzantılı tüm dosyaları siler)
find . -type f -name "*.txt" -exec rm {} \;

# belli bir uzantı harici tüm dosyaları silme
rm !(*.cpp)
find . -type f ! -name "*.txt" -exec rm {} \; (.txt olmayan her şeyi siler)

# bir klasördeki tüm boş klasörleri silme
find . -type d -empty -exec rmdir {} \;

# bir klasörü ve içeriğini istisnalı silme
rm -r directory_name/!(file_to_keep)

```

- rmdir → klasörleri siler

```markdown
# eğer klasör boşsa
rmdir folderName

# eğer boş değilse rm -rf kullanmalisin
rm -rf nonEmptyFolder 
```

- man → bir fonksiyonun vs. manual’ini verir

```markdown
# manualini verir
man strcmp

# -k belli bir keyword içeren tüm fonksiyonları verir
man -k memchr
```

- which → bir komut yüklü mü değil mi kontrol eder, varsa dizinini verir

```markdown
# mesela
which cat (/usr/bin/cat)
```

- uname → sistemin hakkında bilgi verir

```markdown
# -a ile detaylı bilgi alirsin
uname --all, -a
```

- su → kullanıcı değiştirir

```markdown
# mesela
su bugra

# - ile roota geçersin
sudo su -

# kullanıcı değiştirmeden belli bir kullanıcı olarak bir komutu çalıştırma
su - userName -c <command>
```

- whoami → o anki kullanıcıyı görürsün

```markdown
# whoami
```

- neofetch → sistemle ilgili bilgi verir

```markdown
# neofetch
```

- useradd, adduser (The adduser command is a symbolic link to the useradd command.)

```markdown
# kullanıcı ekler
sudo useradd cemre

# kullanıcı siler
sudo deluser cemre
```

- passwd → şifre işlemleri

```markdown
# o anki kullanıcının şifresini değiş
passwd

# belli bir kullanıcınınkini değiş
passwd userName

# kullanıcının şifresini sil
passwd -d userName
```

- pwd → o anki dizini verir

```markdown
pwd
```

- cd → dizin değiştirmeye yarar

```markdown
# ana dizine git ($HOME)
cd

# belli bir dizine git
cd <belli_bir_dizin>

# üst dizine git 
cd ..

# bir önceki seçili dizine git
cd -
```

- ls → listelemeye yarar

```markdown
# -l detaylı liste halinde listeler (alt alta)
ls -l . (nokta demesen de olur, o anki dizini anlar)

drwxrwxr-x 2 bugra bugra 4096 Oca 25 23:00 abc

burada ilk hane o şeyin tipini verir. - yaziyosa file, d yaziyosa klasördür
kalan 9 hane üçer üçer kullanıcının/grubun/herkesin okuma/yazma/çalıştırma
izinlerini verir, yoksa - koyar.  
ikinci hane bağlı hard linklerin sayısını gösterir.
hard linkler ln dosya dosya2 şeklinde kopyalanır
ücüncü hane dosyanın/klasörün sahibi
dördüncü hane grup sahibi
besinci hane boyutu
altıncı hane son değiştirme tarihi
yedinci hane de ismi

# -a gizli dosyaları listeler
ls -a (sadece . ile başlayanlar listelenir)

# tür de belirtebilirsin
ls -l *.c (sadece .c ile biten dosyalar listenelir)

# -r küçükten büyüğe sıralar (reverse)
ls -lr

# -S boyuta göre sıralar

# -m virgüllerle ayirir
ls -m 

# -R alt klasördeki dosyaları ve klasörleri de listeler

# -t modifikasyon tarihlerine göre sıralar

# -d sadece klasörleri listeler
ls -d */

# -h human-readable boyutlarını verir (1mb, 20kb vs.)
ls -lh

# --color renkli verir

# -F klasörlerin sonuna / koyarak, dosyaların koymayarak verir
# aynı şeyi -p de yapar

# her klasör ve dosyanın path'ini listeleme
ls -d1 $PWD/**

# -X uzantısına göre listeler
```

- mkdir → klasör oluşturur

```markdown
# şeması
mkdir myFolder

# -p ile nested dizin oluştur
mkdir -p myFolder/itsFolder/thirdFolder
(eğer -p kullanmazsan myFolder yoksa oluşturmaz, ama -p ile yoksa da oluşturur)

# {} ile aynı ismin altında dizinler oluştur
mkdir -p python/{pythonLeetcode,pythonCodeWars}
python altında iki klasör oluşturur
```

- cp → kopyalar

```markdown
# şeması
cp dosya1 dosya2 (aynı dizinde)

# farklı dizinlerde
cp ~/Desktop/dosya1 ~/Downloads/dosya2

# recursively olsun istiyosan -R ekle
```

- mv
- ln
- du
- lsblk
- mkfs
- df
- wc
- chmod
- chown
- tr → harfleri değiştirir, translate eder

```markdown
# bütün t'leri d yapalim
echo "he is my tat" | tr t d <!-- he is my dad -->

# bütün küçük harfleri büyüğe çevirelim
echo "bugraKARA" | tr '[:upper:]' '[:lower:]' <!-- BUGRAkara -->
```

[:xxx:] ifadelerine karakter set expression denir. lower, upper, alpha, digit, alnum, blank vs. gibi türevleri vardır.

- diff
- cmp
- head, tail
- less, more
- du → hafıza gösterir

```markdown
# kısaca tüm hafızayi görme
du -hs *
```

- touch
- ps
- awk

```markdown
# awk komutu text işlemeye yarar

# bir metinden belli bir alanı almaya yarar
(a.txt --> bugra kara molla oglu)
awk '{ print $1, $3 }' a.txt (bugra molla yazdirir)

# 
```

- kill
- history
- crontab
- mv
- &
- &&

```markdown
# bu operatör eğer com1 başarılı çalışırsa com2'yi çalıştırır
# onu da com1'in exit statusunun 0 olup olmadıgından anlıyor
com1 && com2
```

- > output redirector
- >> append operator
- < input redirector