# 8 - philosophers

`resources`

- https://github.com/achrafelkhnissi/Philosophers
- [https://hpc-tutorials.llnl.gov/posix/](https://hpc-tutorials.llnl.gov/posix/)
- https://github.com/anolivei/Philosophers42
- https://github.com/librity/ft_philosophers
- https://github.com/aoumad/Philosophers

**`STUDY LIST IN PHILOSOPHERS`**

- [ ]  mutex in C
- [ ]  what is threading, how to create threads in C
- [ ]  what is data race
- [ ]  şu fonksiyonları araştır
    
    usleep, gettimeofday, pthread_create, pthread_detach, pthread_join, pthread_mutex_init, pthread_mutex_destroy, pthread_mutex_lock, pthread_mutex_unlock
    
- [ ]  process vs. thread farkı
- [ ]  https://github.com/vcwild/philosophers
- [ ]  https://github.com/aabduvak/philosophers
- [ ]  [https://demirten.gitbooks.io/linux-sistem-programlama/content/threads/](https://demirten.gitbooks.io/linux-sistem-programlama/content/threads/)
- [ ]  [https://www.codequoi.com/en/threads-mutexes-and-concurrent-programming-in-c/](https://www.codequoi.com/en/threads-mutexes-and-concurrent-programming-in-c/)
- [ ]  codevault threads izle
- bu projenin temel amacı meşhur bir mantık sorusunu koda dökmek. bir masanın etrafında birden çok filozof oturuyor. ortada da yemek var. filozofların her biri aynı anda sadece üç şeyden birini yapabiliyor: yemek yemek, uyumak ya da düşünmek. masada da filozof sayısı kadar çatal var. yemek yemek için filozoflar sağındaki ve solundakini olmak üzere iki çatala ihtiyaç duyuyolar. yemek yemeleri bitince çatalları bırakıp uyuyorlar. uyanınca çatallar boşalana kadar düşünüyorlar. bu döngü filozoflardan herhangi biri açlıktan ölene kadar yahut da her biri opsiyonel argüman olan yemek yeme sayısı kadar yemek yiyinceye kadar devam ediyor, diğer türlü sonsuza kadar gidiyor.
- program şu parametreleri almalı (./philo …)
    - `number of philosophers` (int) : filozof ve aynı sayıda çatal sayısı
    - `time_to_die` (int mseconds) : eğer filozoflar son yemeklerinden ya da programın çalışmasından sonra bu kadar zaman içinde yemek yemeye *başlamazsalarsa* ölsünler.
    - `time_to_eat` (int msconds) : yemek yeme süreleri. bu sürede 2 çatalı bloke ediyolar.
    - `time_to_sleep` (int msconds) : uyuma süreleri
    - `nımber_of_times_each_philo_must_eat` (optional, int) : eğer bu parametre koyulursa her filozof en az bu sayı kadar yemek yiyince simülasyon biter, koyulmazsa biri ölene kadar sürer.
- filozoflar 1-n arası (n burada filozof sayisi) numaralandırılırlar ve sıralı şekilde otururlar random değil.
- Any state change of a philosopher must be formatted as follows:
◦ ms_passed X has taken a fork
◦ ms_passed X is eating
◦ ms_passed X is sleeping
◦ ms_passed X is thinking
◦ ms_passed X died
x burada filonun id’si
- filozof öldü mesajı ölümden sonra maks 10ms içinde ekrana yazdırılmalı.
- data race olmamalı.
- her filozof bir thread şeklinde tanımlanmalı.
- To prevent philosophers from duplicating forks, you should protect the forks state with a mutex for each of them.
- The philosophers alternatively eat, think, or sleep.
    1. While they are eating, they are not thinking nor sleeping;
    2. while thinking, they are not eating nor sleeping;
    3. and, of course, while sleeping, they are not eating nor thinking.
- Because serving and eating spaghetti with only one fork is very inconvenient, a
philosopher takes their right and their left forks to eat, one in each hand.
- When a philosopher has finished eating, they put their forks back on the table and
start sleeping. Once awake, they start thinking again. The simulation stops when
a philosopher dies of starvation.
- bir programın çalışması proses'tir. bir ya da birden fazla threadin çalıştırdığı program örneği diyebiliriz. Process’ler hayatlarına tek bir thread olarak başlar ve bu threade main thread adı verilir. Bir proces kendi içerisinde başka bir process daha oluşturabilir child process denir.
- thread nedir? OS tarafından oluşturulan işlem akışlarının her biri. peki (UNIX) proses nedir? yine OS tarafından yaratılır. çalışan programın bilgilerini tutar. threadler prosesler altında yaratılır ve çalışır - bunu yaparken prosesin kaynaklarını kullanır. her programlama dili threadleri farklı ele alıyodu, bu da karışıklıklara yol açtı. thread kullanımını standartlaştırmak için Posix Thread yani pthreadler yaratıldı.
- thread vs. process:
    - thread’ler proseslerin bir kısmını oluşturur.
    - Processler birbirinden izole bir şekilde çalışırken thread’ler aynı bellek kaynağını paylaşır.
    - Paralellism, birden fazla işlemci ya da çekirdekte aynı anda işlem yapılması anlamında gelmektedir. Proses çalışan programın her şeyini ifade eden bir kavramdır, thread ise yalnızca akışı belirtir.
    - prosesler sırayla çalışırlar. biri bloklanırsa diğeri çalışmaz (bilgisayarların donmasının nedeni genelde budur. çünkü bilgisayar o anki programdan sağlıklı veri alışverişi sağlayamadığı için sistem ilerleyemez ve donar). threadler ise aynı anda çalışabilir diğer bloklansa da bloklanmasa da (mutex).
    - process: program + state of all the threads executing in the program
    - A process is the instance of a computer program, a program in execution. Each process is started with a single thread, often called the primary thread, but can create additional threads from any of its threads. Several processes may be associated with the same program, a process can create another process (child process).
    - threadler light-weight prosesler heavy-weight olarak gecer yani birinin işleyişi hafifken diğeri ağırdır. bunu şurdan da anlayabiliriz thread’ler arasında geçiş yapmak için işletim sistemiyle ugrasmıyosun, proses degistirmek icin OS’ye sinyal göndermek zorundasın
    - bir proses durmuşsa diğer proses ilerleyemez. bilgisayarların donmasının sebebi budur. threadler ise durdugu zaman diger thread isleyisine devam edebilir.
- Yeni bir thread oluşturmak için `pthread_create` fonksiyonu kullanılır. Thread fonksiyonlarının kullanımı için `pthread.h` başlık dosyası include edilmelidir ve derlerken `gcc -o example example_thread.c -lpthread` kütüphaneyle derlenmelidir. Threadler ana program ile aynı adresleme alanını ve aynı file descriptor'ları kullanırlar.
    
    int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine) (void *), void *arg)
    

burada `thread` parametresi `pthread_t *thread;` ****şeklinde önceden tanımlanmalıdır. oluşan threade bu pointerla erişilecektir. `attr` parametresi thread spesifik olarak `pthread_attr_` ile başlayan fonksiyonlarla ayarlanmış, scheduling policy, stack büyüklüğü, detach policy gibi kuralları gösterir. `start_routine` thread tarafından çalıştırılacak olan fonksiyonu gösterir. `arg` ise thread tarafından çalıştırılacak fonksiyona geçirilecek `void*`'a cast edilmiş genel bir veri yapısını göstermektedir.

- Thread kullanılan bir uygulamada main() fonksiyonundan return edilirse, tüm thread'ler de sonlandırılır ve kullanılan tüm kaynaklar sisteme geri verilir. same goes for exit().
- `pthread_join` fonksiyonu ile, bir thread'in sonlanmasını bekleyebiliriz. Bu fonksiyonun kullanıldığı thread, sonlanması beklenen thread sonlanana kadar bloklan acaktır.
- sadece elinde kırmızı top bulunanların konuşabildiği bir oda düşün. her bir kişi eline topu alıyor, konuşuyor ve topu bir başkasına veriyor. top burada mutex, konuşanlar da threadler oluyor. bu eylemin kendisi ise proses.
- thread mantıgını anlamak icin su koda bakalım

```c
void myturn() {
	while(1) {
		sleep(1);
		printf("my turn\n");
	}
}

void yourturn() {
	while(1) {
		sleep(1);
		printf("your turn\n");
	}
}

int main() {
	myturn();
	yourturn();
}
```

```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void *myturn(void *arg)
{
	while (1)
	{
		sleep(1);
		printf("my turn\n");
	}
	return NULL;
}

void *yourturn(void *arg)
{
	while (1)
	{
		sleep(1);
		printf("your turn\n");
	}
	return NULL;
}

int main()
{
	pthread_t thread1;
	pthread_t thread2;

	pthread_create(&thread1, NULL, myturn, NULL);
	pthread_create(&thread2, NULL, yourturn, NULL);

	pthread_join(thread1, NULL);
	pthread_join(thread2, NULL);

	return 0;
}	
```

- A process is a program in execution. When a operating system executes a program it is called a process. So we may have a single program executed simultaneously multiple times which creates multiple processes. Also we may have a single program which creates multiple processes in the program. Each process has a unique ID called the process ID allocated by OS. her proses birkaç kısımdan oluşur
    - **text:** This is where the code of the process reside. This is a read-only section.
    - **data:** This is where global and static initialized variables are stored.
    - **rodata:** This is where constant variables are stored.
    - **bss:** This is where global and static un-initialized variables are stored.
    - **stack:** This is where the local variables and function calls are stored.
    - **heap:** This is where user allocated memory is stored. When the user uses malloc, calloc, new etc.
- Forking is nothing but creating a new process. We create a new process that copies all the elements of old process.
- Threading is a light weight process which shares all the section of the process except for the stack. A process can have multiple threads.
- threadler bir procesin birden fazla yerde birden fazla işi yapmasını sağlarlar. her bir thread aynı anda sadece tek bir iş yapabilirler. bir kod çalışmıyorken programdır. çalıştıktan sonra sonlanana kadar proses olarak nitelendirilir. her proses ömürlerine tek bir thread ile başlarlar, buna `main thread` denir. eğer main thread sonlanırsa diğer tüm threadler de sonlanır. threadler sadece prosesler altında var olabilirler. proseslerin aksine threadler birbirleriyle ilintili çalışırlar ve aynı bellek kaynağını paylaşırlar.
- There are several ways to access a thread in a multithreaded program, including:
    1. Joining a thread: You can wait for a thread to finish by calling `pthread_join`, which blocks the calling thread until the specified thread terminates.
    2. Detaching a thread: You can detach a thread using `pthread_detach`, which means that its resources will be automatically freed when it terminates, and it cannot be joined.
    3. Terminating a thread: You can terminate a thread by calling `pthread_exit`, which allows the thread to exit and return a value to the caller.
    4. Cancelling a thread: You can cancel a thread by calling `pthread_cancel`, which terminates the thread immediately.
    5. Setting thread attributes: You can set various attributes of a thread, such as its stack size or scheduling policy, by using `pthread_attr_init`, `pthread_attr_setstacksize`, and other related functions.
    6. Synchronizing threads: You can synchronize the execution of threads using synchronization mechanisms such as mutexes, semaphores, or condition variables.
    7. Sending signals to a thread: You can send signals to a thread using the `pthread_kill` function, which can be used to send any signal to a specified thread.

These are some of the most common ways to access a thread in a multithreaded program, but the exact methods available may depend on the implementation of the POSIX threads library.

- data race nedir? a data race is a situation in a multithreaded program where two or more threads access the same memory location concurrently, at least one of the accesses is for writing, and the threads' accesses are unsynchronized. This can result in unpredictable behavior and can be a source of bugs and errors in concurrent programs. A data race occurs when multiple threads access the same memory location without proper synchronization, leading to a situation where the value of the shared memory location can change unexpectedly. This can lead to inconsistent and incorrect results, as the order in which the threads access the shared memory location is not determined by the programmer. To avoid data races, it is important to use synchronization mechanisms such as mutexes, semaphores, or critical sections to ensure that only one thread at a time can access the shared resource. By using synchronization, you can ensure that the shared memory location is updated in a consistent and predictable manner, avoiding data races and ensuring the correct behavior of your concurrent program. Here's an example of a simple program with a data race:

```c
#include <pthread.h>
#include <stdio.h>

int shared_counter = 0;

void *thread_func(void *arg) {
    for (int i = 0; i < 100000; i++) {
        shared_counter++;
    }
}

int main() {
    pthread_t thread1, thread2;

    // Create two threads
    pthread_create(&thread1, NULL, thread_func, NULL);
    pthread_create(&thread2, NULL, thread_func, NULL);

    // Wait for the threads to finish
    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    printf("Shared counter: %d\n", shared_counter);
}
```

This program creates two threads that both increment a shared counter in a loop. However, since the access to the shared counter is not synchronized, it is possible for the two threads to access the shared counter at the same time, leading to a data race. This can result in an incorrect value for the shared counter when the program finishes. To avoid this data race, you would need to use a synchronization mechanism such as a mutex to ensure that only one thread at a time can access the shared counter.

threadler aynı adresi kullandıkları datarace olayı gerçekleşiyor:

Bir değişkenin değerini arttırmak üç adımdan oluşuyor.

- 1-> Değişken değerinin okunması
- 2-> Değişken değerinin arttırılması
- 3-> Değişken değerinin yazılması/işlenmesi
Bu işlemler olurken biri okuyup arttırırken diğeri işlediği durumda
ortalık karışıyor çünkü biri 5 yaparken diğeri 6 yapıyor aynı değişkenle bu durumda diğer thread 6 olarak okucakken ikinci thread sonradan 5
yaptığı için değeri 5 olarak okuyor. Bu durumun yaşanmaması içinde mutex yapıları ile threadleri bekletip işlem yaptırıyoruz.

`to check for data races, use -fsanitize=thread`

- what is mutex? mutexler, çoklu threadlerin kullanıldıgı ortamlarda, paylaşılan hafıza alanları veya veri yapılarına birden fazla threadin aynı anda okuma ya da değiştirme işlemleri yapmasını önlemeye yarayan araçtır. mutual exclusion da açılımı.
    - `pthread_mutex_t` veri tipinde tanımlanır.
    - `pthread_mutex_init()`ile mutexi ilklendiriyoruz.
    - `pthread_mutex_destroy()`ile mutexi siliyoruz,
    - `pthread_mutex_lock()` ile mutexi kitliyoruz.
    - `pthread_mutex_unlock()`mutex_lock’ladıgın bir şey yalnızca o thread içinde ulaşılabilirdir. başka bir thread tarafından kitlenebilir olması için önce o thread’de mutex_unlock kullanıyoruz.
- fonksiyonlar
    - `usleep:` bekletmeye yarıyor
    
    ```c
    #include <unistd.h>
    
    int	main(void)
    {
    	printf("a\n");
    	usleep(10000000);
    	printf("b\n");
    }
    ```
    
    - `gettimeofday:` 1 ocak 1970’ten o ana kadarki zamanı saniye ve microsaniye tipinden verir.
    
    ```c
    int gettimeofday(struct timeval *tv, struct timezone *tz);
    ```
    
    prototipi şu şekildedir. ilk parametresi  zamanı tutacak olan *struct timeval* structının elemanıdır. ikinci parametre ise zaman dilimini tutar (timezone UTC+3 vs). fakat bu parametre atıl oldugundan NULL denir genelde. mesela 
    
    ```c
    #include <time.h>
    
    int main(void)
    {
    	struct timeval	tv;
    
    	gettimeofday(&tv, NULL);
    	printf("Seconds: %ld\n", tv.tv_sec);
    	printf("Microseconds: %d\n", tv.tv_usec);
    	return (0);
    }
    ```
    
    - `pthread_create:` bu fonksiyon yeni bir thread oluşturmada ve bu thread’de bir fonksiyon çalıştırmaya yarıyor.
    
    ```c
    int pthread_create(pthread_t *thread, const pthread_attr_t *attr, 
    		   void *(*start_routine) (void *), void *arg);
    ```
    
    ilk parametre is a pointer to a `pthread_t` structure that will hold the ID of the new thread.
    ikinci parametre is a pointer to a structure that contains features to the newly created thread.
    ücüncü parametre is a pointer to the function that will by run in the thread
    dördüncü parametre is a parametre to this function 
    
    ```c
    #include <pthread.h>
    #include <stdio.h>
    
    void	*myThreadFunction(void *arg)
    {
    	int	*num;
    
    	num = (int *)arg;
    	printf("Hello from thread %d\n", *num);
    	pthread_exit(NULL);
    }
    
    int	main(void)
    {
    	pthread_t	        myThread;
    	int			threadArgs;
    	int			rc;
    
    	threadArgs = 1;
    	rc = pthread_create(&myThread, NULL, myThreadFunction, &threadArgs);
    	if (rc)
    	{
    		printf("Error:unable to create thread %d\n", rc);
    		return (-1);
    	}
    	printf("Main program exiting.\n");
    	pthread_exit(NULL);
    }
    ```
    
- fork() usage: child proses yaratmak icin fork() kullaniyoruz.

---