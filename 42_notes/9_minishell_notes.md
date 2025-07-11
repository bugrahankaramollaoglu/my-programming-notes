# 9 - minishell, dünyanın en saçma projesi

**`RESOURCES`**

- [ ]  [https://www.codequoi.com/en/creating-and-killing-child-processes-in-c/](https://www.codequoi.com/en/creating-and-killing-child-processes-in-c/)
- [ ]  [https://www.codequoi.com/en/pipe-an-inter-process-communication-method/](https://www.codequoi.com/en/pipe-an-inter-process-communication-method/)
- [ ]  [https://www.codequoi.com/en/sending-and-intercepting-a-signal-in-c/](https://www.codequoi.com/en/sending-and-intercepting-a-signal-in-c/)
- [ ]  [https://www.codequoi.com/en/handling-a-file-by-its-descriptor-in-c/](https://www.codequoi.com/en/handling-a-file-by-its-descriptor-in-c/)
- [ ]  [https://www.codequoi.com/en/errno-and-error-management-in-c/](https://www.codequoi.com/en/errno-and-error-management-in-c/)
- [ ]  [https://brennan.io/2015/01/16/write-a-shell-in-c/](https://brennan.io/2015/01/16/write-a-shell-in-c/)
- [ ]  [https://www.youtube.com/watch?v=cex9XrZCU14&list=PLfqABt5AS4FkW5mOn2Tn9ZZLLDwA3kZUY](https://www.youtube.com/watch?v=cex9XrZCU14&list=PLfqABt5AS4FkW5mOn2Tn9ZZLLDwA3kZUY)
- [ ]  [explainshell.com - match command-line arguments to their help text](https://explainshell.com/)
bash komutlarını çok güzel açıklıyor

---

the project is about writing a unix shell, a miniature copy of bash. bash is actually a program written by Brian Fox for GNU project. linuxların cogunda default olarak kullanılır. 2019’a kadar maclerde de default shell bash’ti fakat macOs Catalina’yla beraber maclerin defaul shell’i zsh oldu. 

- en önemli konulardan biri pipe. iki anlamda pipe var biri komut olan `(|)` diğeri fonksiyon olan `pipe()`. fonksiyon olan pipe parent ve child prosesler arası data alışverişinde bulunmanı sağlıyor. bunu da write() ve read() fonksiyonlarıyla yapiyosun. doğal olarak write ile yazma read ile okuma işlemi yapiyoruz ama nereye? fd isimli iki elemanlı bir integer arraye. bu arrayin birinci elemanı yani fd[0] read için fd[1] ise write için kullanılacak. :

```c
/*  pipe() function creates a communication channel between processes */
/*  it is used to send a data through a file's read/write end */

int main() {
	// array to store FDs for write and read end of the pipe
	int fd[2];
	
	// bu mesajı child prosesten maine göndereceğiz
	char message[] = "hello child process";

	// pipe() fonksiyonu sayesinde fd arrayini bir iletişim kanalı haline getirdik
	pipe(fd);

	// forklama işleminden sonra child proses yaratıldı
	int pid = fork();
	// int yerine pid_t kullanmak daha doğru
	
	// pid 0 değilse parenttayiz demektir
	if (pid > 0) {
		// parent

		// close the read-end of pipe
		close(fd[0]);

		// write message to the write-end of the pipe
		write(fd[1], message, sizeof(message));
		// yazma işlemi bitince write-end'ini kapiyoruz
		close(fd[1]);
	} else {
		// 0'sa childdayiz demektir.
		// gönderilecek mesajın kopyasını tutacak bir başka char str yaratiyoruz
		char receivedMessage[100];

		// close the write-end of pipe bc we won't need it when reading
		close(fd[1]);

		// read message from the read-end of the pipe
		// remember that read(a,b,c) reads from source a to source as much as c bytes
		read(fd[0], receivedMessage, sizeof(receivedMessage));
		printf("received message in child process is %s\n", receivedMessage);
		close(fd[0]);
	}
}
```

- gelen komutları shellinde kullanmanın 4 adımı var
    1. read → komut satırından gelen şeyi STDIN’den char string olarak oku
    2. lexer → seperate the string accordingly like from spaces, redirections, pipes etc.
    3. parse → then allocate the tokens that came from lexer accordingly.
    4. execute → then execute the tokens that are commands with their parameters (if given)
- we need to check for EOF or errors while reading. EOF (end of file) means that either we were reading commands from a text file which we’ve reached the end of, or the user typed Ctrl-D, which signals end-of-file. Either way, it means we should exit successfully, and if any other error occurs, we should fail after printing the error.
- shell 3 parta ayrılıyor
    1. lexer: Lexer, metin girdisini tararken belirli dilbilgisi kurallarına dayalı olarak metni analiz eder. Bash shell için lexer, girilen metni parçalara ayırır ve her parçayı birer **"token"** olarak tanımlar. Tokenler, komutlar, argümanlar, değişkenler, operatörler vb. gibi dilbilgisi yapılarını temsil eder. Lexer, metindeki karakterleri okur, bu karakterlerin anlamsal gruplara ayrılmasını sağlar ve daha sonra bu tokenlerin bir listesini oluşturur. mesela 
    
    ```c
    3 + 5 * 4
    ```
    
    gibi bir komut geldi. lexer bunu
    
    ```c
    3, +, 5, *, 4
    ```
    
    olarak ayırır ve shell dilinin gramerine göre uygun yerlere yerleştirir. mesela tam sayı olarak 3, 5 ve 4’ü alır, operator olarak + ve *’ı alır gibi.
    
    1. parser: parser ise lexerın döndürdüğü token listesini alır ve kontrollerden geçirir, sözdizimsel olarak uygun yerlere yerleştirir. 
    2. executor: Executor, parser tarafından oluşturulan dilbilgisi ağacını alır ve bu ağaçtaki her komut için bir işlem oluşturur. Bash shell için executor, komutları işletmek ve sonuçlarını elde etmekle sorumludur. Executor, komutları işletirken, değişkenleri değerlendirir, dosya işlemlerini gerçekleştirir, diğer programları çalıştırır ve gerektiğinde çıktıyı bir sonraki komuta yönlendirmek için boruları (pipe) oluşturur. 
- çevre değişkenleri (environment variables) nedir? bunlar çalışan bir programı özelleştirmek için eklenebilecek değişkenlerdir. en klasikleri PATH (executable aranacak dizin), HOME (ana dizin) vs.’dir. export metoduyla ortam değişkeni atayabilirsin

```c
export myEnv = 'myVal'
```

daha sonra bu ortam değişkenlerine `env` komutuyla bakabilirsin. atadığın bir değişkeni silmek içinse `unset varName` demen yeterli 

```bash
export x=42
env # x=42 yaziyor
unset x # artık yazmıyor
```

ayrıca `declare` ile de atayabilirsin 

```c
declare -x X=42
```

set metodu windowsta kullanılır genelde, declare unixte o yüzden ikincisi daha doğru. ya da export x=42 desen o da declare gibi kullanılıyor. 

ortam değişkeni atamanın bir başka yolu da kod kullanmaktır - setenv()  

```c
#include <stdlib.h>

int main()
{
	setenv("MY_NAME", "bugra", 1);
	char *val = getenv("MY_NAME");
	if (val)
		printf("%s\n", val); // bugra
}
```

C’de spesifik bir ortam değişkenine getenv() fonksiyonuyla ulaşılır. 

```c
int main()
{
	char *myPath = getenv("HOME");

	if (myPath != NULL)
		printf("ana dizin: %s\n", myPath);
	else
		printf("ana dizin bulunamadi\n");
}
```

bazı özel ortam değişkenleri 

```markdown
USER=bkaramol
PATH
PWD
OLDPWD (bir önceki dizin, cd - ile ulaşılır)
HOME
```

ortam değişkenlerine kod üzerinden iki şekilde ulaşılabilir. main’e üçüncü parametre olarak

```c
int main(int ac, char **av, char **env) {
	for (char **e = env; *e; e++) 
		printf("%s\n", *e);
}
```

ya da environ özel değişkeniyle

```c
extern char **environ;

int main() {
  char **s = environ;

  for (; *s; s++)
	printf("%s\n", *s);
}
```

- parantez içinde birden fazla komutu aynı anda çalıştırabilirsin

```c
(touch myFolder; mkdir asd; echo "bugra")
```

- gelen komutları anlamlandırabilmek ve onlara göre işlem yapabilmek için lexer ve parser kullanıyoruz. lexer gelen her şeyi tokenlara ayırmaya yarıyor. mesela

```bash
print: 4 * myVar + 1
```

dedik. lexer bunu {`print` - `:` - `4` - `*` - `myVar` - `+` - `1`} olarak ayırıyor. parser ise bunları ağaç şemasına döndürmeye yariyor çünkü sıraları da önemli. + ya da * sonda gelemez, : başta gelemez vs. 

- her bir dosya açıldığında, gnu’dan ya da kod yoluyla, OS o dosyaya özel integer formatında bir integer yaratır (file descriptor). bu entry’de dosyanın fd’si ve tuttugu içerik saklanmaktadır. ilk üç fd OS’a ayrılmıştır, gerisini kullanıcı doldurur. bunlar
    - 0 - STDIN yani standart input
    - 1 - STDOUT yani standart output
    - 2 - STDERR yani standart error’dur.
    
    bunlar da esasında birer dosyadır. sırasıyla input output ve hata kodlarını tutarlar. 
    
- echo’yu -n flagiyle kullanırsan sonuna \n koymaz. minishell’de bunu da dahil etmelisin

```bash
echo -n bugra
bugra$
```

- `unset` should unset variables from the environment. yani şu komut çalışmalı

```bash
$ export H=42
$ env
...
H=42
$ unset H
$ env
(no H anymore)
```

- **`lexerParse`**
lexer bir inputu, minishell özelinde komut satırından gelen stringi anlamlı en küçük parçalara ayırmaya yarıyor. gelen stringi karakter karakter okuyup önceden belirlenmiş kurallara göre parçalara ayırıyor, bunu da 2D boyutlu olması sayesinde yapiyor. temelde iki görevi var
    1. tokenization yani tokenlara ayırma
    2. lexical analysis yani her bir tokenı anlamlandırma. mesela 5 ifadesini string olan 5 değil de integer olan 5 olarak yeniden yorumlama gibi ki doğru sonuca ulaşılabilsin
    
    parser lexerdan sonra geliyor. lexer metni tokenlara ayırdıktan sonra parser da bu tokenları programlama dilinin gramer kurallarına göre düzenliyor ve anlamlandırıyor.
    
    1. sentaks analizi yapiyor, sentaks hataları vs. var mı diye kontrol ediyor.
    2. yapi kurumu: lexerın tokenlerini hiyerarşik bir sıraya diziyor. meslea 
    
    ```bash
    grep, a, |, .c, ls
    ```
    
    gibi bi işlem geldi. bunu parser tree ya da command table denen bir tabloya 
    
    ```bash
    ls a | grep .c
    ```
    
    şeklinde düzenleyerek yerleştirir.
    
- AST (abstract syntax tree) nedir? bu bir veri yapısıdır. aldıgı inputu hiyerarşik ve dile uygun olarak düzene sokmaya yarar. mesela

```bash
x = 5 + y
```

ifadesini 

```bash
    =
   / \
  x   +
     / \
    5   y
```

haline getirir

- redirections: redirectionlar sayesinde nereden input alacagımızı ya da nereye output verecegimizi belirleyebiliyoruz.
    - **`<`** ifadesine STDIN redirection denir. bir dosyadan input alır. soluna yazdıgın ifadenin inputunu sagdakinden alır
    
    ```bash
    cat < asd.txt
    ```
    
    asd.txt dosyamızın içeriği bugra olsun. cat çalışması için bir inputa ihtiyaç duyar, bunu da < sayesinde asd.txt’in içeriğiyle sağlarız. (string değil dosya bekler). aynı şeyi `echo` ile denersen çalışmaz 
    
    ```bash
    echo < asd.txt
    ```
    
    çünkü echo cat gibi STDIN’den okuma yapamaz, direkt input bekler. 
    
    - **`>`** ifadesine STDOUT redirection denir. soldakinin outputunu sağdakine input olarak verir. eğer dosya yoksa yaratır.
    
    ```bash
    a.out > result.txt
    ```
    
    burada a.out dosyası çalıştırıldığında STDOUT’a (mesela printf) bir şeyler yazdırıyor olsun. tek başına çalıştırdığımızda terminale yazdıracakken redirection kullandıgımız icin terminale değil result.txt içine yazar. ya da
    
    ```bash
    cat bugra > name.md
    ```
    
    çoklu çalıştırırsan da her birine yazdırılır 
    
    ```bash
    echo "bugra" > a > b > c
    ```
    
    - **`>>`** ifadesi ise >’nin aksine silmeden yazar yani ekleme (append) yapar. buna da append redirection denir.
    
    ```bash
    cat cemre >> name.md
    ```
    
    name.md’nin içeriğini sıfırlamadan üzerine yazdı
    
    - **`2>`** ifadesine STDERR redirection denir. hata mesajlarını hata dosyasına yazdırmaya yarar.
    
    ```bash
    gcc a.c 2> hata.txt
    ```
    
    a.c ifadesi hata verdiginden ötürü derlenemeyen bir kod olsun. bu derlemenin tüm hata ve warning mesajlarını yukarıdaki kodla hata.txt içerisinde saklayabiliriz
    
- örnek

```bash
a.out | wc -l > dosya.txt
```

a.out dosyası 30 satır kod üretiyor, wc -l ile bu satır sayısını alıyoruz, > sayesinde de 30’u dosya.txt içerisine yazdırıyoruz.

- heredoc: heredoclar sayesinde bir inputu bir scripte ya da programa redirect edebiliyoruz. **`<<`** şeklinde karşımıza çıkıyor. sentaksı

```bash
cat << delimiter
text1
text2
text3
delimiter
```

delimiter boşluk vs. içeremez ve tek kelime olmalıdır. 

```bash
$ wc -l << EOF
heredoc> this
heredoc> is
heredoc> a
heredoc> nice
heredoc> death
heredoc> EOF
5
```

EOF aradığımız için EOF görünce duruyor ve o zamana kadarki satırların wc -l’sini yazdırıyor terminale. yani heredoc’un en önemli özelliği tek seferlik bir input değil stream of input beklemesi. bunu < ile yapamiyoruz. 

- redirectionları birleştirerek de kullanabilirsin

```bash
wc -w < metin.txt > kelimeSayisi.txt
```

- difference between ‘ ‘ and “ “ : envVar’ları alırken ‘ ‘ çalışmazken “ “ çalışıyor

```bash
export x=42
echo x        # x
echo $x       # 42
echo '$x'     # $x
echo "$x"     # 42
```

bunun sebebi şu: bash ‘ ‘ arasında gördüğü her şeyi string literal olarak algılıyor. “ “ ise öyle algılamıyor ve variable expansion uyguluyor.

- **`$?`** ifadesi son çalıştırılan komutun exit statusunu saklı tutar.

```bash
echo asd
$? # 0   (başarılı olduğumuz için)
cat asd 
$? # 1   (başarısız olduğu için)
/bin/ech0
$? # 127 (komutu bulamadığı için)
```

- **`$0`** o anki çalıştırılan programın adını verir

```bash
echo $0 # bash, sh, zsh her ne ise
```

- operatör olan pipe ( | ) : solundaki değerin outputunu sağdakine input olarak verir. farklı kullanım örnekleri

```bash
# 1. komutun çıktısını 2. komuta girdi olarak verme
command1 | command2

# 1. komutun çıktısını 2. komutla filtreleme
echo "jfjdsfjkshasdalskfjsdj" | grep "asd"

# satır sayma
ls | wc -l

# sırala
ls | sort

# 1.
cat file.txt | grep "anahtarKelime"

# 2.
./a.out | wc -l

# 3.
cat file.txt | grep "anahtarKelime" | sort

# pipe'ın okunma sırası soldan sağadır.
# o yüzden aşağıdaki tac'a değil (satırları tersten verir) sort'a göre çalışır
cat file.txt | tac | sort
```

pipela ayırdıgın komutlar birbiri ardına değil aynı anda başlar 

```bash
sleep 5 | ls
```

- && operatörü yalnızca soldaki ifade başarılıysa sağındakini çalıştırır

```bash
git add . && git commit -m "asd" && git push
```

- || operatörü ise yalnızca soldaki ifade başarısızsa sağındakini çalıştırır

```bash
g++ deneme.py || echo "başaramadık abi"
```

- bütün bash komutları esasında ana dizinde birer programdır (like .exe). çoğu /bin’de tutulur. o yüzden ls yazmakla /bin/ls yazmak arasında bir fark yoktur. yalın haldeki komutların her biri bin/* e atanmış birer aliastır.

```bash
/bin/ls -l # demekle ls -l demek aynı şeydir
/bin/echo -n "bugra" #
```

- aşağıdaki ifade a.txt içerisinde

```bash
echo bugra > a.txt kara molla oglu
```

bugra kara molla oglu yazdırmalı. sıralama ters gözükse de > ifadesi sağında gördüğü ilk dosyayi seçer ve orada işi biter. kalanların hepsi bu komuta input olarak alınır.

- `environment variables` ve `shell variables` arasındaki fark: ortam değişkenleri daha genel shell ise daha lokaldir, yalnızca o shellde geçerlidir. env_var ise tüm child proseslerde tutulur. `export` komutu sayesinde shell değişkenlerini ortam değişkenleri haline getiririz.
- terminale **`set`** komutunu girdiğimizde tüm shell variables, environment variables, defined variables vs. gösterir. **`env`** komutu ise sadece environment variableları gösterir.
- `make -n` flagi sayesinde çalıştırmadan make çıktılarını görebilirsin.
- minishell’de neden child process kullanmak zorundayız? komutları parselamayı ve çalıştırmayı tek proseste yani ana shellde yapamayiz çünkü eğer hatalı komut verirsek tüm shell çöker ve çökmemesini istiyoruz. bütün sub process mantığının temeli budur, temelde init (pid 0) çökmemesi içindir.
- genelde child’ın pid’si parentınkinden büyüktür ama bazı istisnasi durumlarda OS kullanılmamış eski pid’leri kullanmış olabilir ve bu tür durumlarda parent_pid daha küçük olabilir.
- çoklu directionlar şöyle çalışır

```c
cat > aa > bb >> cc >> dd
```

- iç içe tırnaklar nası çalışmalı?

```markdown
# echo bugra || 'bugra' || "bugra"
bugra
# echo b"ugra" || b'ugra'
bugra
# echo ''bugra'' || """"bugra""""
bugra
# echo "bu'gr'a"
bu'gr'a
# echo 'bu"gr"a'
bu"gr"a
# echo mer"haba'ben'im"'ad"ım'
merhaba'ben'imad"ım
# echo 'bugra"han"kara'
bugra"han"kara
```

- sonuç ne olur?

```markdown
echo 1"234'5"67'89"0'
```

- what’s the diff between command and a token? a command is a structure with its own syntax and sentence completion. token on the other hand is a parsed command.

```
# tokens
[git] [commit] [-m] ["asd"]

# command
[ls] [echo -n] [gcc ./asd.c] ...

```

- arka planda sürekli leak kontrolü yapmanın yolu bir başka bashte şu komutu çalıştırmaktır

```bash
while 1
leaks minishell
sleep 1
done
```

- bazı özel dolar kodları

```bash
$$ is the PID of the current process.

$? is the return code of the last executed command.

$# is the number of arguments in $*

$0 is the name of the currently running program

$* is the list of arguments passed to the current process
```

- `kill -9 pid` direkt öldürürken `kill -1 pid` rebuild etmeye calısır.
- SIGKILL (ctrl z) ile SIGQUIT (ctrl \) farkı: sigkill and sigquit both will kill the process but the later will also force the core to dump. Forcing a core dump means generating a file, often referred to as a "core dump" or simply a "core file," that contains a snapshot of a process's memory at the moment it terminated due to an unhandled signal, such as SIGQUIT. This core dump file is a crucial debugging tool