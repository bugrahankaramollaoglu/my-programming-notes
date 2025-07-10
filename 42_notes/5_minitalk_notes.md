# 5 - minitalk

- useful links
    - [**https://github.com/filunieto/minitalk_git/wiki/**](https://github.com/filunieto/minitalk_git/wiki/)
    - [KILL FUNCTION IN C - C COURSE #20](https://www.youtube.com/watch?v=qXP4F49K1XM&list=PLyLXXSiuhPPdDGWUm4QlctAq2UDvcOIcP)
    - [https://www.codequoi.com/en/creating-and-killing-child-processes-in-c/](https://www.codequoi.com/en/creating-and-killing-child-processes-in-c/)
    - [https://www.codequoi.com/en/sending-and-intercepting-a-signal-in-c/](https://www.codequoi.com/en/sending-and-intercepting-a-signal-in-c/)
    - [**https://github.com/pvaladares/42cursus-02-minitalk**](https://github.com/pvaladares/42cursus-02-minitalk)
    - [**https://www.youtube.com/watch?v=83M5-NPDeWs**](https://www.youtube.com/watch?v=83M5-NPDeWs)
    - [**https://www.youtube.com/watch?v=PErrlOx3LYE**](https://www.youtube.com/watch?v=PErrlOx3LYE)
    - [**https://github.com/mlanca-c/Minitalk/wiki**](https://github.com/mlanca-c/Minitalk/wiki)
    - [**https://www.gnu.org/software/libc/manual/html_node/Checking-for-Pending-Signals.html**](https://www.gnu.org/software/libc/manual/html_node/Checking-for-Pending-Signals.html)
    - [**http://www.cs.kent.edu/~ruttan/sysprog/lectures/signals.html**](http://www.cs.kent.edu/~ruttan/sysprog/lectures/signals.html)
    - [**http://www.cs.kent.edu/~ruttan/sysprog/lectures/signals/sigaction.html**](http://www.cs.kent.edu/~ruttan/sysprog/lectures/signals/sigaction.html)
    - [**https://github.com/ablaamim/Minitalk**](https://github.com/ablaamim/Minitalk)
    - [**https://github.com/j4k0m/minitalk**](https://github.com/j4k0m/minitalk)

**`STUDY LIST IN MINITALK`**

- [ ]  basit anlamda unix sinyalleri nedir nasıl kullanılır
- [ ]  SIGUSR1 SIGUSR2 nedir
- [ ]  pause(), sleep(), usleep() nedir farkları nedir
- [ ]  getpid(), kill(a, b) fonksiyonu nedir ne işe yarar
- [ ]  bitlerin çalışma mantığı nedir nasıl çalışır nasıl decimale çevrilir
- [ ]  bitwise operatörleri (&, >>, <<)
- [ ]  static int nedir
- [ ]  post/pre increment farkı
- bu projede iki terminal arası mesaj yolluyoruz. iki terminalde iki ayri main’de sürekli çalışıyor. mesajları (stringleri) iki adet sinyal kullanarak yolluyoruz (SIGUSR1 ve SIGUSR2). mesajları bit bit yollamak zorundasın. o yüzden bu sinyallerden birini 0 birini 1 bitini göndermek için kullanacağız.
- getpid() built-in fonksiyonuyla çalıştırıldığı mainin proses id’sini öğrenebilirsin:

```c
int main() {
	int myPid = getpid();
}
```

- kill(pid, SIG_X) fonksiyonu, SIG_X sinyalini pid id’li prosese gönderir. yani kill() sinyal göndermeye yarar, sonlandırmaya değil.

**`TO DO LIST IN MINITALK`** 

- [ ]  tüm proje şu dosyalardan oluşuyor
    - client.c
    - server.c
    - minitalk.h
    - makefile
- [ ]  hem serverda hem clientta main olacak. server’daki main pid alip bi terminale yazdıracak ve signal fonksiyonu yardımıyla sürekli SIGUSR1 ve SIGUSR2 sinyali bekleyecek. bunlardan birini 0, birini 1 olarak kullanacağız. hangisi hangisi fark etmiyor.
- [ ]  bu iki sinyale gelen parametreler bir fonksiyona gidecek o fonksiyonda hangi sinyalin 1 hangisinin 0 olduğuna karar verip bir başka fonksiyona atacağız.
- [ ]  3. fonksiyon ise bir `static int` te 8 bit biriktirmeye çalışacak biriktiği anda write ile yazdıracak.
- [ ]  tüm bunlar olurken client’a gelen mesaj bitene kadar harflerinin bitlerini işlemlere sokarak n. harfinin bitlerini server’a göndereceğiz. 2
- [ ]  bu projenin bir püf noktası komut satırından gelen pid’nin str olarak geldiğini, atoi’yle inte çevirmemiz gerektiğini unutmamak.

---