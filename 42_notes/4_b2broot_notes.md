# 4 - born_to_be_root

BORN TO BE ROOT

- bu projede bir sanal makineye (Oracle Box VM) linux distrosu (Debian) kuracağız. GUI'si olmayacak, tüm komutlar CLI'den girilecek.

**`TO DO LIST IN BORN TO BE ROOT`**

- [ ]  davut abi pdf’ini birebir yap
    
    [davut2.pdf](4%20-%20born_to_be_root%207c07b89851a145859156bcf820c58707/davut2.pdf)
    
- [ ]  sonra sunlara calis
- Linux’ta sabit disklerin isimlendirilme mantığı şu şekildedir;
    
    Sabit diskler eğer IDE kanalından bağlı ise “hda”, “hdb” SCSI ve/veya SATA kanalına takılı ise “sda”, “sdb” gibi isimler alırlar. Örneğin birinci sabit disk “hda” olarak adlandırılır. İkinci sabit disk “hdb” şeklinde adlandırılır. Buradan da anlaşılacağı üzere a’dan z’ye kadar -eğer mümkünse- 26 adet sabit disk olabilir. Diskleriniz günümüzün popüler HDD kanalı olan SATA’dan bağlı ise bu durumda örneğimizdeki isimler “sda” ve “sdb” olacaktır.Sabit disklerin bölümleri ise 1’den 63’e kadar numara ile temsil edilirler. Örneğin birinci sabit diskin birinci bölümü “hda1” veya “sda1” olarak adlandırılır. Sistemdeki CD/DVD sürücüler ise “sr0”, “sr1” gibi isimler alırlar. Linux’ta her bir sabit disk max 63 parçaya bölünebilir.
    
- dosyaların isimleri
    - / is the root file system
    - /boot bilgisayarı boot edecek statik dosyaları tutuyor
    - /home kullanıcı kişisel dosyaları
    - /tmp geçici dosyalar
    - /usr statik veriler (static data)
    - /var değişken veriler (variable data)
    - /srv sistem tarafından sağlanan servis verileri
    - /opt add-on application software packages

EVALUATION

- .vdi numarası kontrol et
    
    yapman gereken b2br reposuna signature.txt içinde sanal makinenin .vdi kodunu atamaktır. bunun için makinenin dizininde shasum b2broot.vdi deyip cıkan sayıyı .txt'e at ve sonrasında git add/commit/push. bu iki sayi birebir aynı olmalıdır.
    
- sanal makineye giriş yapın
- kullanıcı parolası uygun mu değil mi diye kontrol edin
    
    chage -l bkaramol
    
- ufw kontrolü yap
    
    sudo systemctl status ufw
    
    ufw'nin izinlerine bakmak istiyosan da
    
    sudo ufw status numbered
    
- ssh kontrolü yap
    
    sudo systemctl status ssh
    
- OS kontrolü yap
    
    uname -a
    
- user kontrolü yap
    
    id bkaramol
    
    bütün kullanıcıların listesini görmek için /etc/passwd gitmelisin
    
    cut -d: -f1 /etc/passwd
    
- yeni kullanici olustur
    
    sudo adduser bkaramol2
    
- yeni kullanıcının parolasını değiştir
    
    passwd bkaramol2
    
- şifre politikalarını nası belirledin?
    
    1) sudo vim /etc/login.defs (max/min/warn_days ayarladim)
    
    2) sudo /etc/security/pwdquality.conf (difok= vs. ayarladim)
    
- evaluating isimli yeni bi grup olustur
    
    sudo addgroup evaluating
    
- yeni kullanıcıyı bu gruba ata
    
    sudo adduser bkaramol2 evaluating
    
- yeni kullanıcı atanmıs mı kontrol et
    
    groups bkaramol2 (ya da)
    
    id bkaramol2
    
- şifre politikasının avantaj ve dezavantajlarını anlat
    
    güvenlik cart curt
    
- makinenin server adına bak
    
    hostname
    
- makinenin adını değiştir
    
    1) sudo hostnamectl set-hostname new_name
    
    2) sudo vim /etc/hosts'ta da değiştir
    
    3) reboot
    
- diskleri göster
    
    lsblk
    SDA ilk diski temsil eder. Sonraki blok cihaz bölümleri sda’nın yanında ondalık sayı alarak gösterilir.
    
    sr0: çıkarılabilir cihazı temsil eder. CD/DVD olan.
    
    Cd - rom. Listelenen cihazlar içinde çıkarılabilir olup olmayanaları gösteren bölüm “RO”dur. (RO = removable) RO = 0 ise çıkarılamaz block device RO = 1 ise çıkarılabilir block device sda birincil cihazdır
    
    sda(1-4) arası primary diskleri temsil ederken Sda4 sonrası logical birimler olduklarını gösterir.
    
    mountpoint = Bu, cihazın monte edildiği bağlama noktasını görüntüler.
    
- yeni kullancıyı sudo'ya atayıp kontrol et
    
    1) sudo adduser bkaramol2 sudo
    
    2) id bkaramol2
    
- sudo visudo ile yazdıklarını anlat
- sudo komutlarının kayıtlarının tutuldugu /var/log/sudo/sudo.log'un calıstıgını kontrol et
    
    cd /var/log/sudo
    
    sudo cat sudo.log
    
- yeni bir porta izin ver
    
    sudo ufw allow/deny 8080
    
- yeni port iznini sil
    
    sudo ufw delete 8080
    
    ya da numbered diyip numarasını sil
    
- ssh kontrolü yap
    
    sudo vim /etc/ssh/sshd_config
    
    1) nopermitlogin no olmalı
    
    2) port 4242 olmalı
    
    3) sudo systemctl status ssh --> enabled/active olmalı
    
    değilse
    
    4) sudo ssh enable
    
- ssh nedir?

Linux sunuculara erişim sağlamak için SSH protokolü kullanıyoruz. SSH, also known as Secure Socket Shell, is a network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network. Yani uzaktaki bir sunucuya bağlanmak, ona komutlar ve dosyalar göndermek üzere kullanılan şifrelenmiş bir uzaktan bağlantı sağlayıcı protokolüdür.Diğer önemli değişiklik port değişikliğidir. SSH bağlantısının portu varsayılan olarak 22’dir. Portu değiştirerek saldırganların 22 portundan sunucuya erişimini engelleyeceğiz. (Biz de 4242 portundan bağlanarak güvenli bir SSH bağlantısı oluşturmaya çalışıyoruz).

- iTerm'den ssh'a bağlan
    
    ssh bkaramol@127.0.0.1 -p 4242
    
- monitoring.sh açıkla
    - uniq → tekrar eden satırları ayırır.
    - $1,$2 → sutünları tutar
    - xargs → öncesinde kullanılan çıktıyı bir sonraki komuta iletir.
    - arc -> mevcut işletim sisteminin mimarisini ve kernel versiyonunu gösterir
    - pcpu-> fiziksel işlemci sayısı
    - vcpu-> sanal işlemci sayısı
    - fram -> sunucunun erişilebilir ram miktarı
    - uram -> kullanılan ram miktarı
    - pram -> yüzde olarak kullanılan miktarı verir
    - fdisk -> sunucunun erişilebilir depolama alanı
    - udisk -> sunucunun kullanılan depolama alanı
    - pdisk-> diskin yüzde olarak kullanımını verir
    - cpul -> yüzde olarak işlemci kullanım oranını verir.
    - lb -> son yeniden başlatma tarihi ve saati (last boot)
    - lvmt -> LVM ile yapılandırılmış diskin bilgisini verir.
    - lvmu-> LVMnin aktif olma bilgisini verir
    - ctcp-> mevcut aktif bağlantı sayısı
    - ulog-> sunucuyu kullanan kullanıcı sayısı
    - ip -> sunucu ip adresi verir
    - mac-> sunucu mac adresi verir
    - cmds-> sudo ile çalıştırılmış komut sayısı
    - Cpu physical -> işlemci
    - vCpu → sanal işlemci sayısı
    - CPU load → Anlık işlemci yükü/kullanımı
    - Last boot → sanal makinenin en son açıldığı an
    - Connexions TCP → ssh ile sunucuyla bağlantı kuranların sayısı
    - Free bellek hakkında bilgi, kullanılan alan, kapasite, boş alan vs…. Free -m : mebi byte
    - Awk komutu -> grepe benzer şekilde örüntü temelli tarama işlemi
    - Top -> sunucu hakkındaki anlık istatistikleri verir.
- cron nedir?
belirli işlerin belirli zamanlarda tekrarlanarak yapılmasını bir otomasyona bağlayarak kolaylaştırır. Bir görevin ilerleyen zamanda tekrarlamak için komut verme işlemine cron denir. cron'u nası kurduk?
1) crontab -u root -e

*2) /10 * * * * bash /usr/local/bin/monitoring.sh* 

her 10 dakikada bir .sh komutunu calıstır.

- cron baslat/durdur
    
    1) sudo service cron stop
    
    2) sudo service cron start
    
    3) sudo systemctl disable cron
    
    4) reboot
    
- LVM nedir. logical volume manager. LVM disk bölümlendirme metodudur. bu sayede bilgisayarın sadece belli bir kısmını sanal makineye ayırabilirsin, dinamik boyutlu olan bu hafıza yerlerini arttırıp azaltabilirsin. physical/logical volume'lerden oluşur. bu ikisi birleşerek voluma group'u oluşturur. yani bir disk bölümlendirme tekniği olan LVM sayesinde disk alanını resetlemeden büyültebilir ya da küçültebilirsin.

sanal makineler nasıl çalışır

- sanal makineler bilgisayarın varolan donanımlarını kısmi olarak paylaşarak varolan sistemin sanal bir taklidini yaratırlar. bunu da hypervisor adlı bir program sayesinde yapar.
- kullanım alanları
    - yeni os denemeleri
    - mevcut os yedekleme
- vm'nin avantajları
    - çeviklik ve hız
    - maliyet
    - güvenlik
- debian centOs farkı
    - debian çoklu mimari destekliyor centOs desteklemiyor
    - centOs redhat debian debiancılar tarafından destekleniyor
    - centOs daha karmaşık ve komplike
    - debian'da sayısız paket vardır centOs sınırlıdır.
    - centOs daha çok iş için kullanılan bir distrodur
- debian paket yöneticisi apt’dir Centos’un yum.
- apt - advanced packaging tool. yazılım yüklemeye yarayan bir yazılımdır.
- Aptitude, işlevselliğe bir kullanıcı arabirimi ekleyen, böylece bir kullanıcının etkileşimli olarak bir paket aramasına ve yüklemesine veya kaldırmasına izin veren gelişmiş paketleme aracının ön ucudur. İlk olarak Debain için oluşturulan Aptitude, işlevselliğini RPM tabanlı dağıtımlara da genişletiyor. (RPM = RedHat Package Manager yani Redhat Paket yöneticisi anlamına gelmektedir.) Aptitude işlevselliği apt- get'den daha geniştir. aptitude alt-paketleri de indirirken apt indirmez. aptitude outdated paketlerin takibini yapar, apt yapmaz.
- SELinux (Security-Enhanced Linux) Linux’ da zorunlu erişim denetimi (MAC) mekanizmasına gerçekleşmesini sağlayan bir projedir.
- appArmor ise çok daha basit bir güvenlik protokolüdür. Arka planda sessizce çalışır. Sisteme zarar verebilecek ayarları, servisleri ve diğer ayarları kontrol edip sınırlandırır. Sistem açılışlarında default olarak aktiftir.
- SELinux ve APPArmor arasındaki fark? "Bu güvenlik sistemleri, uygulamaları birbirinden yalıtmak için araçlar sağlar ve bir uygulamanın güvenliği ihlal edildiğinde bir saldırganı sistemin geri kalanından yalıtır. SELinux kural kümeleri inanılmaz derecede karmaşıktır ancak bu karmaşıklıkla süreçlerin nasıl izole edildiği üzerinde daha fazla kontrole sahip olursunuz. Bu ilkelerin oluşturulması otomatikleştirilebilir. Bu güvenlik sistemine karşı bir grev, bağımsız olarak doğrulamanın çok zor olmasıdır. AppArmor (ve SMACK) çok basittir.
- pushlamadan önce user42 olusturdugunuzdan ve kullanicinin ona üye oldugundan emin olun...
1. crontab -u root -e > > > **2) /10 * * * * bash /usr/local/bin/monitoring.sh* > > her 10 dakikada bir .sh komutunu calıstır. >

belirli işlerin belirli zamanlarda tekrarlanarak yapılmasını bir otomasyona bağlayarak kolaylaştırır. Bir görevin ilerleyen zamanda tekrarlamak için komut verme işlemine cron denir.

---