çok basit haliyle teorisini gördüğümüz podları bu bölümde oluşturmaya başlayacağız.

hemen terminale geçelim.

Yani Windows'ta PowerShell ile Mac ve Linux üzerinde sistemlerin terminaline geçelim ve ilk olarak yeni

bir proje yaratalım.

Bakın şimdi:
run firstpod --image=nginx --restart=Never

olsun ve Enter'a basarak oluşturalım.

Evet arkadaşlar aynen docker run der gibi run diyerek bir pod oluşturabiliriz.

Bu komutla gördüğünüz üzere run diyor ve yeni bir obje oluşturuyorum.

Adına first diyor ve bu kodun içerisinde çalışacak konteynerin Engine x isimli image oluşturulmasını

istiyorum.

Son olarak da eğer bu kodun içinde konteyner kapanırsa yeniden çalıştırılmaması için 5 restart eşittir

never parametresini giriyorum.
==========================================================
Şimdi hemen kubectl "get pods -o wide" ile sistemde çalışan podları listeleyelim bakalım.

Oluşturduk ama sistemde bu pod çalışıyor mu?

Daha geniş bir bilgi vermesi için de wide komutunu veriyorum.

Gördüğünüz gibi şu anda arkadaşlar sistemde first adında bir pod çalışıyor.

Şimdi not kısmında bu kodun hangi node üzerinde çalıştığını görebiliyoruz.

Status kısmında da durumunu görüyoruz.

Bakın burada ready kısmı gerçekten önemli.

Buradaki 1 slash 1 şu anlama geliyor arkadaşlar bu pod içerisinde çalışması istenilen konteyner sayısı 1 ve bu konteyner şu anda çalışıyor ve hazır.

Get komutu sistemde çalışan kodları görmek istersek iyi ama spesifik bir pod ile ilgili detaylı bilgi almak istersek. Gördüğünüz gibi o wide opsiyonu ile bile sadece belirli başlı şeyler görebiliyoruz.
Yani IP'sini görebiliyoruz.
Şu anda yaşını görebiliyoruz.
Daha önce restart edilmiş mi, hangi node üzerinde çalışıyor vesaire birçok bilgi görüyoruz ama kısıtlı şeyleri görebiliyoruz.

**biz bir pod'un veya herhangi bir objenin daha detaylı bilgilerini görmek istersek burada kullanabileceğimiz bir tane Subcommand var:
ikinci olarak bunu göstermek istiyorum: kubectl describe pods firstpod
describe komutu arkadaşlar bizim bir objenin detaylarını görmemize imkan veriyor.
kubectl describe boşluk describe diyoruz.
Ondan sonra hangi obje tipinin üzerinde çalışmak istiyorsak onu yazıyoruz.
Daha sonra objenin ismini yazıyoruz.
Arkadaşlar kubectl describe dediğimiz zaman arkadaşlar bakın şimdi daha çok bilgi edindik.
Bu kod ne zaman oluşturulmuş?
Gördüğünüz gibi start time'ı nerede koşuyor?
Bu kod içerisinde çalışan konteynırın id'sini ve benzeri birçok bilgiyi bu describe komutuyla erişebiliyoruz.

Arkadaşlar bu ekranda özellikle dikkat etmenizi istediğim kısım bu alttaki event kısmı.
Bu komut ile kısmından bir nevi bu kodun tarihçesine ulaşabiliyoruz.
Adım adım neler olmuş, hangi aksiyonlar alınmış, Kubernetes neler yapmış bunların hepsini burada görebiliyoruz.
=============
Şimdi arkadaşlar ilk olarak kütüphaneler komponenti bizim verdiğimiz komut ile oluşturulan pod tanımını görmüş ve ona uygun bir node bulup oraya atamış.
Gördüğünüz gibi bunu bu event kısmından öğrenebiliyoruz arkadaşlar.
Sonrasında o modda çalışan millet hemen bunu oluşturmaya başlamış.
İşte image çekilmiş.
Ardından container oluşturulmuş.
Ve hemen ardından da başlatılmış.
Gördüğünüz gibi adım adım bu kod ile ilgili uygulanan işlemler buradan takip edilebiliyor ve bizler de ileride bunu yaparken bu kısma sıklıkla göz atacağız.
İşte arkadaşlar script bu ve benzeri ek bilgileri görmemize yarıyor.
===========================================
Şimdi gelelim bir başka komuta.

Arkadaşlar bu bölümde sizlere göstermek istediğim bir başka sub Command log olacak. Tahmin edebileceğiniz üzere container dünyasında konteyner logları en önemli araçlarımızdan biri oluyor.

Konteyner içerisinde çalışan ana uygulamanın ürettiği logları konteynerin stout ve Stout error çıkışlarına verdiğini biliyorsunuz.Ve native loglama altyapıları da konteynerlerin bu çıkışlarını gözleyerek bizlere ulaştırabiliyor.

Docker dünyasında container loglarına docker logs komutu ile erişebiliyorduk. kubernetes dünyasında ise tahmin edebileceğiniz üzere kubectl logs komutunu kullanıyoruz.

hemen bunu bir deneyelim.

Ne diyoruz?
logs firstpod

Ondan sonra da arkadaşlar podumuzun ismini yazıyoruz.

Kodumuzun ismini yazdıktan sonra gördüğünüz gibi bu kodun içerisindeki konteynerin oluşturduğu logları bize ekranda gösteriyor.Bu sayede biz kodun içerisinde çalışan konteynırların ürettiği loglara erişebiliyoruz.Eğer loglarla ilgili aksiyon almak istersek de bunları görebiliyoruz.
Fakat şimdi bazen bunları canlı olarak görmek isteyebiliriz.

Bakın pardon Ctrlfirst dediğim zaman bu bana bütün kodları listeliyor.Fakat buna ben yapışmak isteyebilirim.
Yani mesela bu bir web sunucu olduğu bir web container olduğunu düşünün.
O web konteynırdaki logları canlı olarak izlemek isteyebilirim.

Burada da kullanacağımız opsiyon Arkadaşlar "logs -f firstpod" opsiyonu opsiyonuyla bu kodun içerisindeki logları canlı olarak görebiliriz.Bu arada Ctrl C ile çıkabiliyorum aklınızda bulunsun ve hemen bir başka komuta geçelim.
==========================================
Şimdi yine Docker dünyasında çalışan konteynerlerin içerisinde ek bir uygulama ya da komut çalıştırmamız gerekir.

Örneğin konteynere bağlanmak için bir shell çalıştırmamız gerekir ve bunun için exec command kullanırız.

Ya da aynı command kullanarak komut çalıştırabilir ve bağlantı kurabilirsiniz.

bakın şimdi exec diyorum ondan sonra hangi kodun üzerinde komut çalıştırmak istiyorum?
$kubectl exec firspod -- hostname 
$kubectl exec firspod -- ls / 

Bu kodun içerisinde komut çalıştırmaya yarıyor. Aynı container içerisinde komut çalıştırma ile bire bir aynı.
======================================================

Peki bağlamak istersek?
Burada da yine exec komutunu kullanıyoruz.
$kubectl -it exec firspod  -- /bin/bash 


Exec diyoruz.
pod'umuzun ismini giriyoruz ondan sonra.

Shell'imizin adresini yazıyoruz.

Gördüğünüz gibi arkadaşlar exec ile ben şu anda bu first pod içindeki konteynerin içerisine bağlandım.
==================================
Son olarak da bu oluşturduğumuz pod'u nasıl sileceğimize bir göz atalım arkadaşlar ve bu bölümü sonlandıralım.

kubectl delete pods firstpod

Fakat arkadaşlar bu silme işlemlerini özellikle production ortamlarında dikkatli kullanın.

Çünkü gördüğünüz gibi bana emin misin diye sormadı.

Ne bileyim işte bir çöp kutusu yok hani oradan geri döndürelim vesaire.

Bu silindiği zaman silinecek arkadaşlar.

O yüzden özellikle bu silme komutlarını dikkatli şekilde kullanalım.

Özellikle production ortamlarında.

Hani durduk yere boş yere production'ı aşağı indirmeyelim arkadaşlar.
===========================
Fakat sizlere kötü bir haberim var.

Bizler production ortamında  diğer objeleri genellikle bu şekilde direkt kubectl komutları aracılığıyla yaratmıyoruz

Arkadaşlar ben bir komut girerek ve istediğim şeyin nasıl olmasını gerektiğini bu komut aracılığıyla tanımlayarak oluşturuyorsam, buna imperative yöntem diyoruz.

Bakın ben dedim ne yaptım dedim.

Dedim.

Ondan sonra buna bir isim verdim.

Böyle yapmıştım.

Hatırlıyorsanız first pod demiştim.

Ondan sonra imajını belirtmiştim.

Sonra ne istediğimi söylemiştim, restart demiştim.

Bu komutla bir pod oluşturulmuştu.

Oluşturduğum pod özelliklerini bir yere yazmadım arkadaşlar.

Sadece komuta girdim komutla oluşturdum.

Şimdi diyelim ki ben burada bir volume eklemek istiyorum.

Haydi bunu da komut olarak girdim.

Bu komuttan sonra gittim bir tane volume bla bla bla bla bla komutları girdim.

Arkadaşlar başka bir şey istedim.

Mesela buna bir label eklemek istedim.

Bunların hepsine geleceğiz arkadaşlar.

Bu arada yeter dedim bir komut daha girdim.

Bu kodun üzerinde bunu oluşturdum.

Şimdi arkadaşlar şu ana kadar sıkıntı yok.

Yani kodumu oluşturdum.

Ama ben bu kodun aynısını bir başka zaman tekrar oluşturmak istersem tekrar en başta komutu gireceğim.

Sonra işte volume komutunu gireceğim, sonra level komutunu gireceğim.

O bir sürü işim olacak.

Ayrıca tekrarlayabilmek için bu komutları bir yere kaydetmem ve sırasını da belirtmem gerekiyor.

Ben bu komutu arkadaşlar alacağım.

Bir notepad açacağım burada örneğin Ve artık bunu buraya kaydedeceğim bir komut bu olacak.

Pardon bunu buraya kaydedeceğim.

Bundan sonra ikinci komut bu.

Bla bla bla 3 komut bu bla bla bla.

Bu şekilde bunları bir yere kaydetmem gerekecek ki bunları daha sonra tekrar yapabileyim.

Tekrardan bunları oluşturabilirim.

Fakat bunun yerine şunu yapabiliyor olsaydım daha iyi olmaz mıydı arkadaşlar?

Şimdi istediğim kodu oluşturacak komutları tek tek girmek yerine, o pod'la olmasını istediğim özellikleri

bir dosyaya kaydetsem ve bu özelliklerde bir kod olsun istiyorum diye Kubernetes bir deklarasyonda bulunsam.

Tek tek container oluşturup volume labelları düzenlediği üç tane komut gireceğim.

Kubernetes bana şu dosyada özelliklerini belirttiği kod oluştur desem her ne ise o özelliklerde bir pod'u gerekli adımları girerek kendisi oluşturursa daha iyi olmaz mı?

Yani ben istediğimi tek tek yapmak yerine Kubernetes ile istediğimi deklare etsem ve o da onu olduysa.

Evet arkadaşlar bu mümkün ve biz buna deklaratif yöntem diyoruz ki daha önce konuştuğumuz docker-compose.yaml benzeri bir dosya.