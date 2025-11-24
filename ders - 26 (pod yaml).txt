Şu ana kadar Kubernetes üstünde iş yüklerimizi objeler şeklinde oluşturabildiğimizi. Bu objeleri kubectl ile imperative şekilde oluşturabildiğimizi, oluşturabildiğimiz çeşitli obje tipleri olduğunu ve bunlardan en temel olanlarından birinin de pod olduğunu öğrendik.

Fakat bu objeleri illa imperative şekilde oluşturmak zorunda değiliz.Kubernetes bizlere oluşturmak istediğimiz objeleri JSON ya da formatlarında tanımlayabilme ve bu tanımıKubernetes ile deklare ederek de oluşturabilme imkanı sunuyor.

Fakat bizler genellikle JSON yerine tercih ediyoruz.

JSON yazması ve okuması bir nebze zor olduğu için.

Onun yerine yazması ve okuması daha kolay olan tercih ediliyor.

ben de eğitimde bunu tercih ettim.

Bizler Kubernetes objelerini dosyaları olarak oluşturmak istediğimizde belirli bir formatı takip ederek oluşturmamız gerekir.
Her objenin tanımı değişiktir ama hepsi temel bir formatı takip eder.
=================
Şimdi arkadaşlar eğitim repository'sinde klasörün altında ObjectTemplate adında bir dosya var.

Arkadaşlar şu anda ekranda gördüğünüz gibi 4 anahtarlı bir tane template dosyamız var.

Bu ekranda gördüğümüz 4 anahtarın ilk üçü yani API, version ve metadata her Kubernetes obje tanımında bulunması gereken 3 üst seviye anahtar.
Kubernetes altında oluşturacağımız her türlü obj bu 3 üst seviye bilgiler tanımlanarak oluşturulur.
Sonuncusu ise objelerin çoğunda bulunur fakat bazılarında bu kısım olmayabilir ya da başka anahtarlarda bulunabilir.
======================================
Şimdi ilk olarak ikinci satırdaki ile başlarsak. Arkadaşlar burası bizim oluşturmak istediğimiz objenin ne objesi olduğunu tanımladığımız yerdir:
Yani ben ne oluşturmak istiyorsam onu buraya yazarım.

Pod oluşturmak istiyorum.
Pod yazarım.

Servisi oluşturmak istiyorum.
Servis yazarım, deployment deployment yazarım.

Hangi tipte objeyi oluşturacaksam burada onu yazarım.
Bizim örneğimizde biz pod oluşturmak istediğimiz için buraya pod yazıyorum.
Yani benim kubernetes oluşturmak istediğim objenin tipi pod.
API version ile devam edersek ilk satırdaki bu kısım bizim oluşturmak istediğimiz obje tipinin Kubernetes API ında hangi endpoint üstünde ya da kaba tabirle hangi API'da tanımlandığını belirttiğimiz kısım. Şimdi bu bizim kendi kafamızda belirlediğimiz bir şey değil.
Arkadaşlar her Kubernetes objesinin sunulduğu bir API var ve bizim o objenin API bilerek buraya yazmamız lazım.

Peki bunu nasıl bulacağız?

Hangi API deployment hangi api?

Bunu nasıl bilebiliriz?

Arkadaşlar cevap oldukça basit.
==================
Buna dökümantasyonundan bakabilir ya da size daha önce gösterdiğim şekilde kubectl aracılığıyla bunu öğrenebilirsiniz.
Gelin hemen pod'un içine bakalım. kubectl aracılığıyla bunu öğrenelim.

Neydi komutumuz?

"kubectl explain pods" komutunu kullanıyoruz.
Ve hangi objenin özelliklerini öğrenmek istiyorsak objeyi yazıyoruz.Gördüğünüz gibi ben kodun özelliklerini öğrenmek istediğim için explained yazdım ve bakın versiyonu neymiş.

Arkadaşlar hangi API'da duruyormuş ve V1 API da duruyormuş.

Mesela gelin aynı şekilde deployment ine bakalım.

Bakın Deployment Apps view'da duruyormuş mesela başka neye bakabiliriz?

Service account'a bakalım.

Service account da duruyormuş gördüğünüz gibi.

Arkadaşlar bunları ezberlemenize gerek yok.

Bunların hangi API'da durduğuna.

Biz bu şekilde explain komutuyla ya da Kubernetes in kendi dökümantasyonuna girerek bakabiliriz.

Şimdi dönelim tekrardan objects template dosyamıza.

Biz bir pod oluşturmak istiyoruz.
Burada arkadaşlar v1 API da duruyor.Bunu bu şekilde tanımladık.
=================
Şimdi dosyamızdaki üçüncü kısım METADATA kısmı her objenin dosyasında bulunması gereken API

version, kayıt ve metadata kısmı var.

Metadata bizim bu obje ile ilgili bilgileri tanımladığımız yerdir.
Burada arkadaşlar isim gibi, namespace gibi, label gibi, annotations gibi obje özel bilgileri tanımlarız.
Metadata kısmı api version ve kind gibi tek value olan string bir alan değildir.
Arkadaşlar bir dictionary'dir ve altında birden fazla bilgi tanımlayabiliriz.
Gelin hemen tanımlayalım ne yapalım.
Bakın geliyorum Metadata nın altına hemen bir satır aşağıya geçiyorum ve ondan sonra arkadaşlar iki tane boşluk bırakıyorum ve şunu yazıyorum.
Name ne olsun?
Bunun name ismi first olsun arkadaşlar.
bakın biz metadata altında oluşturduğumuz objenin temel bilgilerini tanımlıyoruz.
Bunu söyledim bakın name firstport şeklinde.

Ben bu yarattığım objeye firstport diye bir isim veriyorum.

Şimdi burada tanımlayabildiğimiz bir başka daha değer girelim.

Bir tane label tanımlayalım.

Arkadaşlar şöyle yapıyorum.

Bakın diyorum yeni bir tane anahtar açıyorum sonra alta geçiyorum iki tane boşluk bırakıyorum ve şunu diyorum.

App front end. Arkadaşlar Labels ile bu objeye atayacağım labelları etiketleri tanımlıyoruz.

Ben burada ki yani anahtarı app values yani değeri de front end olan bir etiket atıyorum.

Labellar Kubernetes dünyasında oldukça önemlidir arkadaşlar ve biz buna ayrı bir bölüm olarak geleceğiz.

Şimdilik sadece metadata altında tanımlandığını bilin arkadaşlar.

Bakın şimdi gördüğünüz üzere metadata altında objeyi betimleyen bilgileri tanımladık.

Metadata kısmı bunun içindir.

Yani bu objeye yönelik bilgileri metadata kısmı altında tanımlıyoruz.
=========================
Şimdi geçelim son kısım olan spec kısmına.

Arkadaşlar burası her obje tipine göre değişen kısımdır.

Spec kısmında oluşturmak istediğiniz objenin özelliklerini belirtiriz.

Her obje için buraya girebileceğiniz bilgiler farklıdır.

Örneğin pod oluştururken buraya istediğiniz container bilgilerini girerken, servis objesi oluştururken

service objesinin özelliklerini tanımlarız.

Yani her obje tipine göre burda tanımlayabileceğimiz bilgiler değişir ve biz burada kullanabileceğimiz

tanımları genelde dokümantasyona bakarak bulur ya da zaman içerisinde oluştura oluştura tecrübe kazanır

ve bir şekilde öğreniriz.

Şimdi biz bu örnek üzerinden gidersek bizler bir kod oluşturmak istiyoruz dimi?

Bu kodun stack kısmında bu kodu oluşturan konteynırları ve onlarla ilgili bilgileri tanımlarız hemen.

Bakın arkadaşlar stack altına geliyorum hemen bir sonraki satıra geçiyorum ve 2 tane boşluk bırakıyorum

ve diyorum ki konteyner tanımlamak istiyorum.

Konteyner dedim.

Hemen onun altına geçiyorum arkadaşlar ve oluşturmak istediğim konteynerı tanımlamaya başlıyorum Şimdi

hemen bunu da ne yapalım ismi ne olsun?

Name olsun çünkü index bir konteyner çalıştırmak istiyorum.

Imagine olsun.

Engineers isimli konteyner imajından çalıştırmak istiyorum.

Bir de bunun portunu da export edelim arkadaşlar.

Portunu export etmek için konteyner port diye.

Bakın ben yazarken gördüğünüz gibi otomatik tamamlamayı bana öneriyor.

İşte bu yüzden ben Visual Studio kullanmak istedim arkadaşlar.

Bu yüzden ben bu kubernetes ve extensionlarını yükledim.

Bu tarz güzelliklere sahip olabiliyorsunuz.

Visual Studio kodu ve extension'larını kullanırsak hangi portu açacağız?

80 portunu açacağız.

Ne dedim arkadaşlar Engine Engine isimli image oluşturulsun ve container'da konteyner dışında 80 portu

aracılığıyla erişebilirsin.

Tanımı bitirdim bakın şimdi bir yukarıdan aşağıya bir daha bu şeye bakalım dosyasına bakalım.

Ben şu anda bir yama dosyası oluşturdum arkadaşlar.

Bu dosyasının içerisinde bir adet port objesi tanımlıyorum.

Port tipi objeler one isimli API bulunduğu için API version bunu tanımlıyorum.

Bu kodun isminin first kodu olmasını istediğimi belirtiyor ve eşittir Frontend isimli bir etikete sahip

olacağını tanımlıyor.

Spec kısmında ise bu kodu oluşturacak container'ı tanımlıyor.

Ona bir isim veriyorum.

Hangi imajın yaratılması gerektiğini ve hangi porttan public olacağını söylüyorum.

Böylelikle.

Oluşturmak istediğim objenin nasıl olması gerektiğini tanımlamış oldum.

Şimdi bu dosyayı bir save ile kaydedelim.

Aslında kaydetmenize gerek yok çünkü repository'de bu dosyayı göreceksiniz.

Bakın burada pod bir diye bir dosya var.

Ben bunu kaydettim.

Bakın aynı dosya burada görebiliyorsunuz.

Sadece burada frontend kullanmışız, burada kullanmışız.

Bakın bunu zaten kaydetmenize gerek yok.

Ben bunu repository altında kaydettim.

Pod bir yağmur şeklinde duruyor arkadaşlar.

Şimdi geçelim pod dosyasından ne şekilde bir obje oluşturabileceğimizi, Kubernetes, kubernetes ile

nasıl gönderebileceğimize bakalım.

Şimdi arkadaşlar hemen Yani terminalime geçiyorum ve terminalde bu pod1 dosyasının olduğu klasöre geçiyorum.

Klasör klasörü.

Hemen bakalım.

Pod Bir yama dosyası burada mı?

Burada.

Şimdi arkadaşlar dosyalarımızı Kubernetes API deklare etmek için biz apply komutunu kullanıyoruz ve

diyoruz ki apply.

Ondan sonra ardından ekliyorum ve apply etmek istediğim dosyamı belirtiyorum.

Benim burada apply etmek istediğim dosyası hangisi?

Pod1 dosyası yani Kubernetes ise şunu diyorum Bak güzel kardeşim ben şurada bir obje tanımladım.

Pod bir yama dosyası olarak bir obje tanımladım.

Bu tanımı al ve bu tanım da yazılan obje benim için oluştur.

Bakın gördüğünüz gibi first pod isimli pod oluşturuldu.

Arkadaşlar bakın ben ne yaptım ne ettim şu ana kadar.

Arkadaşlar ben size şunu dedim.

Bak güzel kardeşim Ben şurada Pod pod 1.2 isimli bir yama dosyası oluşturdum.

Bu dosyanın içerisinde bir obje tanımladım.

Bu tanımı al ve bunu Kubernetes ile bu tanımı aldı ve bunu doldurdu.

Şimdi gelin Script Sub commentini hatırlıyorsunuz.

Bu script Sub Command ile bu objelerin özelliklerine bakabiliyorduk.

Gelin hemen yarattığımız objenin özelliğine bakalım.

Script diyorum.

Hangi objenin özelliklerine bakacağım.

Objenin özelliklerine bakıcam.

Objenin adını First post.

Bakın gördüğünüz gibi benim istediğim özelliklerde bir pod oluşturulmuş.

Yani amacımıza ulaştık demek yerine bunların yapmak istediğimiz her şeyi burada dosyası olarak tanımladık

ve dosyayı apply ile Kubernetes Cluster a gönderdik.

Kubernetes cluster da bizim tanımladığımız özelliklerde işte gördüğünüz gibi.

Bakın arkadaşlar First pod post labelları tanımlanmış 80 portu dış dünyaya açılmış, index imajından

oluşturulmuş, index imajı çekilmiş bir container yaratılmış bulunan bir pod oluşturulmuş.

Şimdi arkadaşlar objeleri bu şekilde yemin dosyaları olarak tanımlayarak deklaratif şekilde oluşturmanın

küfran dan farkı ve avantajları nelerdir biraz bundan bahsetmek istiyorum arkadaşlar.

İlk avantajı şu.

Artık elimde gördüğünüz üzere versiyon kontrol altına sokabileceği bir dosyam var.

Ben bu yemin dosyasını bir tripository de tutabilir ve üstünde yapılacak her türlü değişikliği takip

edebilirim artık.

Dolayısıyla uygulamam da yapılan değişiklikleri merkezi bir yerden kontrol etme şansım oluyor arkadaşlar.

Örneğin uygulamada bir değişiklik yapacaksam operatörün Kubernetes ile bağlanıp ram vs şeklinde gerekli

komutu girmek yerine dosya üzerinde gerekli değişikliği yapar ve bunu gider.

Git repository'sine gönderir.

Git içindeki dosyayı günceller ve bunu otomatik bir.

Continuous deployment sistemi bu değişikliği, bu dosya üzerinde yaptığınız değişikliği farkeder ve

deployment ı güncelleyebilir.

Her türlü değişiklik kaydını da dosya geçmişinde tutulmuş olur.

Operatör hangi komutu girdi acaba komut ne zaman girdi vesaire takip etmeme gerek kalmaz.

Böyle bir pipeline oluşturabilirim.

Bu en temel avantajlarından bir tanesidir.

Ama deklaratif yöntem sadece bu versiyon kontrol kapasitesi kazandırmaz.

Bundan daha da önemli bir kabiliyet verir.

Bakın şimdi deklaratiful dosyalarını vs unutun.

Bu dosyalarımız yok.

Yeni bir tane pod yaratmak istiyorum.

Tekrardan döneyim buraya.

Ne diyorum?

Bakın şimdi diyorum dosyalarını bilmiyorum.

Second pod diye bir pod oluşturacağım imaj olarak gene engine'den Oluşturulmasını istiyorum.

5 5 port ile arkadaşlar 80 portunu açıyorum hatta gelin buna label da verelim aynısı olsun biraz öncekinin

label eşittir diyorum.

Neydi epico front end de ondan sonra restart i could never diyorum.

Arkadaşlar şimdi bakın birebir aynı pardon bu port.

Port 1 tane olacak.

Bakın arkadaşlar aynı kodu yani şunu şunun aynısını bu sefer ne yaptım.

Değişik bir isimle gittim imperative olarak yani run ile çalıştırdım run ile oluşturdum.

Şimdi ben burada ek bir bilgi eklemek istiyorum diyelim.

Diyelim ki bir label daha eklemek istiyorum.

Bakın aynı komuta buna ekleyelim.

Yani şu komutun aynısını Gidelim bir tane de mesela ne olsun?

Diyelim ki Team Developer diye bir tane daha label eklemek istediğimi söylüyorum.

Şimdi Enter'a basıyorum.

Bana bir hata verdi.

Ne dedi?

Or exist yani second port diye bir tane port zaten var.

Diyor ki kardeşim bak second port isminde bir port zaten var.

Sen yeniden bu isimde bir pod yaratamazsın.

Gördüğünüz gibi ben Kubernetes aslında mevcut kodu güncellemek istedim ama imperative olarak ben ona

olmasını istediğim halini söyleyemiyorum.

Arkadaşlar ona olmasını istediğim şeyi komutla gönderiyor.

Dolayısıyla Kubernetes benim yeniden bir obje yaratmak istediğimi düşündü.

Denedi ama aynı isimde bir obje zaten çalıştığı için yapamadı.

Ben bunu nasıl yaparım Gider second silerim yeniden yeni komutla oluştururum, sil yap ekle çıkar.

Arkadaşlar bu işler oldukça fazla zaman alır ve çok fazla hataya açık olur.

Bakın şimdi bunu deklaratif olarak yapmak istesem işler nasıl kolaylaşacak?

Şimdi tekrardan bir dosyamıza dönelim arkadaşlar.

Bakın aynısı komut yerine bunu şöyle yapıyorum, deklar olarak yapıyorum.

Tamam diyorum.

Developer olarak bunu tanımlıyorum arkadaşlar ve kaydediyorum.

Şimdi tekrardan dönüyorum buraya.

Apply desfold 1.20 diyorum bakın gördüğünüz gibi first configure dedi.

Hatta gelin buna tekrardan bir script ile bakalım.

Bakın gördüğünüz gibi bu kodun üzerinde yeni bir tane daha tanımlanmış label tanımlanmış arkadaşlar.

Şimdi arkadaşlar Kubernetes ile daha önceden kod isimli bir tanım vermiştim ve bu tanımdan pod oluşturulmuştu.

Benim istediğimi aldı ve gerçekleştirdi.

Şimdi ona ben az önce bu tanımı güncelleyerek bir daha verdim.

Kubernetes mevcut tanıma baktı, yani daha önceki tanımına baktı ve benim son gönderdiğim tanıma baktı

ve arada fark gördü ve bu farkı kapatmak için gerekli aksiyonları aldı.

Ben ona Git, sil, yeniden oluştur, label gir şunu yap bunu yap komutu girmedim.

Ben ona istediğim halini söyledim.

Yani ben ona dedim ki artık bu first pod isimli kodun yeni tanımı bu.

Ben bu tanımı bunun üzerinden yaptım ve bunu Kubernetes e gönderdim.

Yani ona istediğim halini söyledim o da istediğim halini oluşturdu.

Evet arkadaşlar deklaratif ve imperative arasındaki fark budur.

Birinde olmasını istediğiniz halini söylersiniz, diğerinde de olmasını istediğiniz hali siz adım adım,

tek tek yaparsınız diyerek bu imperative decorative konusunda işlediğimize göre son bir tane daha konumuz

vardı Artık ona geçerek onu da aradan çıkartarak bölümü kapatabiliriz.

=====================================
Arkadaşlar bu noktada size bir şey daha göstermek istiyorum.

Şimdi bakın az önce dosyamızda bir değişiklik yaptık ve bunu yeniden apply komutu ile gönderdik ve objemizi

güncelledik.

Şimdi sizlere bir başka yöntem daha göstermek istiyorum.

Bakın şu komutu giriyorum hemen geçelim.

kubectl edit diyorum.

Bu sefer edit komutunu giriyorum arkadaşlar daha sonra hangi obje üzerinde çalışmak istiyoruz ve çalışmak

istediğimiz objenin adı nedir?

Arkadaşlar Edit komutu herhangi bir kubernetes objesinin üstünde direkt bir değişiklik yapmak istediğiniz zaman kullanılır.Bu komutu girer ve enter'a basarsanız.

Arkadaşlar Kubernetes cluster'dan bu objenin mevcut halini formatında çeker ve bu dosyayı sizin elinizde

varsayılan olarak tanımlanmış tek text editör ne ise onunla açar.

Arkadaşlar benim şu anda vim olduğu için bu dosyayı açtı.

Şimdi ben bu dosya üzerinde değişiklik yaparsam, örneğin bir tane daha eklersem buraya gelip arkadaşlar

hemen şöyle yapalım.

Ye basıyorum ve interaktif moda geçiyorum.

Mesela ne diyeyim buna Bir tane daha label ekleyelim ne diyelim 8.

Fandom.

DA mental.

Test diyelim.

Böyle bir label daha ekleyelim arkadaşlar.

Ve şimdi dosyayı da hemen burada.

İnteraktif moddan çıkayım ve bu dosyayı da kaydedip buradan çıkayım.

Arkadaşlar Bakın şimdi ben bu dosyayı kaydettiğim anda Kubernetes bu değişikliği hemen bu dosya üzerinde

daha doğrusu hemen bu obje üzerinde uygular.

Arkadaşlar gördüğünüz gibi ben az önce Edit force komutunu girdim Enter'a bastım.

Kubernetes bu objenin yeni halini Kubernetes cluster'dan çekti ve benim varsayılan text editörü ile

bunu açtı.

Artık bunun üzerinde ben canlı bir şekilde güncelleme yapabilirim.

Arkadaşlar bu güncellemeyi yaptıktan sonra bunu kaydedip kapatırsam.

Arkadaşlar bu gördüğünüz gibi şu anda bir şey kaybetmediğim için olmadı.

Ama az önce yaptığım da gördüğünüz gibi bunu günceller.

Bu şekilde de dosyalarımızı, objelerimizi güncelleyebiliriz.

Ama bunu çok sık kullanmıyoruz arkadaşlar.

Sadece şunu da göstereyim bakın hani belki bana inanmayacaklar olabilir.

O yüzden onları da ikna edelim.

Tekrardan describe ile first koda bakalım.

Bakın gördüğünüz gibi ben edit ile eklediğim pardon edit ile eklediğim label da buraya gelmiş.

Evet arkadaşlar edit komutunu da öğrendik ama bu noktada bir şey daha eklemek istiyorum.

Bizler normalde bu yöntemi kullanıyoruz arkadaşlar.

Edit yöntemini Hani bunun yerine versiyon kontrol altına aldığımız kendi dosyalarımızda değişiklik yapıyoruz.

Yani ben gidip edit yapmak yerine burada değişiklik yapıp apply ile oraya gönderiyorum ve bunu da böyle

yapmamız gerekiyor.

Çünkü öbür türlü edit'te yaptığım şey bu dosyanın üzerinde yok.

Yani ben edit ile direkt canlı olarak objeyi güncelledim.

Bunun üzerinde güncelleme.

Dolayısıyla bunu bir daha birisi Kubernetes API ile gönderirse buradaki hali geçerli olacak.

O yüzden siz de mümkün mertebe her türlü değişikliğinizi dosyalarınız üzerinde yapıp Apply ile gönderin.

Sadece travel yaparken vesaire böyle hızlıca dosya üzerinde bir şeye bakmamız gerekiyorsa o zaman kullanıyoruz

diyelim ve artık bu bölümü kapatalım arkadaşlar.

Bu bölümde objeleri tanımladığımız yani dosyalarının nasıl oluşturulduğunu ve dekoratif yaklaşımın tam

anlamıyla ne demek olduğunu gördük.

Şimdi kısa bir mola verelim ve ardından konumuza pod konusuna devam edeceğiz.