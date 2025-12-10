Daha önce pod oluşturulduğu zaman neler oluyor sorusuna kısa da olsa bir cevap vermiştik.

Bu bölümde bu cevabı biraz daha açacak ve kodun yaşam döngüsünde nasıl bir yol izlediğini göreceğiz.

İlk olarak işin teorik kısmını halledeceğiz arkadaşlar.

Şimdi öncelikle ortamımızı bir çizelim ve hayali bir proje yaratalım.

Pod yaratmak için geçen bölümlerde gördüğümüz gibi ctrl ile imperative şekilde komutla oluşturuyor ya

da bir yama dosyası oluşturarak ve bunu ctrl.

Apply komutuyla Kubernetes cluster'a gönderiyoruz.

Bu aşamadan itibaren Kubernetes API Server bu yama dosyasını alır.

Burada bizim belirttiğimiz ayarların yanında varsayılan olarak set edilmiş ayarları harmanlar.

O da bir unique ID atar ve tüm bunları CD'ye kaydeder.

Bu noktadan itibaren pod oluşturulmuştur ve yaşam döngüsünün ilk aşaması olan pending aşamasına geçer.

Eğer sistemde bir kodun durumu pending ise bunun anlamı şudur.

Siz veya bir başka bileşen sistemde yeni bir pod oluşturdu.

Pod ile ilgili tüm gerekli tanımlar yapıldı ve veritabanına kaydedildi ama henüz herhangi bir node üstünde

oluşturulmadı.

Arkadaşlar kütüphaneler servisinden ve ne işe yaradığından daha önce bahsetmiştik.

Türkçe servisi API Server aracılığıyla sürekli gözler.

Eğer burada yeni yaratılmış, herhangi bir node ataması yapılmamış bir pod görürse çalışmaya başlar.

Algoritması ve seçme kriterlerine göre kodun çalışmasının en uygun olacağı node'u seçer ve veritabanındaki

pod objesini node bilgisine ekler.
=====================
Bu noktadan itibaren pod yaşam döngüsünde creating aşamasına geçer.

Eğer pod oluşturdunuz ve pod uzunca bir süre pending aşamasında takılı kalıyor ve create aşamasına geçmiyorsa,

bu kubescheledur'ın pod oluşturulması için uygun bir node bulamadığı anlamına gelir.

Bunun birçok nedeni olabilir.

Clusterımızda bu kodun gereksinimlerini karşılayacak herhangi bir node bulunmuyor olabilir ya da node'lar

üstünde kaynaklar tükenmiş.

Kısacası ne CPU ne de memory kaynakları pod oluşturmak için yeterli Olmayabilir.

Bunun gibi sebeplerden dolayı arkadaşlar bu aşamayı geçemeyebilir.

Şimdi bu bilgiyi de verdikten sonra Create aşamasında neler oluyor ona bir göz atalım.

Arkadaşlar Cluster içerisinde bulunan tüm notlarda Qled adında bir servis çalışır.

Bundan daha önce bahsetmiştik.

Kubernetes de aynı kütüphaneler gibi etc veritabanını gözler ve bulunduğu node atanmış portları tespit

eder.

Yeni yaratılmış pod görür ve hemen işlemlere başlar.

İlk olarak pod tanımında oluşturulması istenen containerlara bakar ve bu konteynerlerin oluşturulacağı

imajları sisteme indirmeye başlar.

Eğer bir şekilde imaj indirilmezse pod Öncelikle eğer image pool ve ardındanda image pool backup aşamasına

geçer.

Eğer pod statüsünde image pool backup görürseniz bu node imajı repositoryden çekemediği ve bunu tekrar

tekrar denemeye devam ettiği anlamına gelir.

Bunun birkaç nedeni olabilir.

En sık karşılaştığımız neden image resminin pod tanımında yanlış yazılmasıdır.

Misal.

X yerine x yazarsanız Yani iki tane n kullanılır, iki tane kullanırsanız yani bir tane yaparsanız böyle

bir repository olmadığı için image bulunamayacak ve sisteme çekilemeyecektir.

Ya da bir diğer sık rastlanan sebep imajı çekmek için registry'ye authentic olmanız gerekmesi.

Fakat kullanıcı adı, şifre gibi bilgilerde hata yapılmasıdır.

Bu durumda da imaj çekilemeyecek ve image rollback off aşamasında takılı kalacaktır.

Fakat bunların olmadığı ve imajın düzgün çekildiğini varsayalım.

İşte bu noktadan itibaren o notta bulunan Container Engine ile haberleşir ve ilgili konteynerlerin oluşturulmasını

sağlar.

Konteynerler çalışmaya başladığı anda da pod running durumuna geçer.

Bu noktada artık pod oluşturulmuş olur.

Şimdi bu noktada kodun yaşam döngüsüne kısa bir ara vererek küçük bir hatırlatma yapmak ve konteynırlarla

ilgili bilgimizi tazelemek istiyorum.

Sonra pod yaşam döngüsüne döneceğiz.

Arkadaşlar, bildiğiniz üzere konteynırlarla ilgili temel bir kural vardır konteyner içerisinde çalışması

istenilen uygulama çalışmaya devam ettikçe konteyner çalışır.

Uygulama çalışmayı bırakırsa konteyner durdurulur.

Uygulamanın kapanması da 3 şekilde olur.

Ya otomatik olarak işi bittiği için hata vermeden kapanır.

Ya siz ona kapanmasını söylersiniz ve hata vermeden kapanır ya da tahmin edebileceğiniz üzere bir hata

verir, çöker, sıkıntı çıkar ve hata kodu oluşturarak kapanır.

Ama ne olursa olsun konteyner içerisinde çalışan uygulama kapanırsa konteynır kapanır.

Birkaç örnek üstünden daha iyi anlatmak gerekirse.

Örneğin EngineX imajından bir konteyner yarattığınızı düşünelim.

Bu konteyner içerisinde EngineX'in zamanını çalıştırıyor.

Bu uygulama bir zaman bir servis.

Dolayısıyla çalışmaya başladıktan sonra siz onu durdurana ya da hata çıkıp çökene kadar çalışmaya devam

eder.

O çalıştığı sürece konteyner de çalışır.

Fakat diyelim ki siz bir imaj yarattınız ve bu imajın varsayılan uygulamasında bir script ya da basit

bir komut konteyner başlayınca bu script ya da komut çalışıyor, işini yapıyor ve işi bitince de otomatik

olarak kapanıyor.

Dolayısıyla o konteynır da kapatılıyor.

Yani kapanması için illa hata vermesine ya da dışarıdan müdahale edilmesine gerek yok.

Uygulama çalıştı, işini yaptı ve kapandı.

Peki şimdi ben bunu durup dururken yaşam döngüsünün ortasında neden anlattım?

Şundan dolayı arkadaşlar.

Kodun içerisinde oluşturulan konteynerlara pod tanımı içerisinde bir policy tanımı yapılır.
==========================
Restart ise 3 değer alabilir.

Always ve never always varsayılan değerdir ve siz aksini belirtmediğiniz sürece always olarak ayarlanır.

Always şu manaya gelir.

Kodun içerisinde yaratılan konteyner ister hata vererek isterse de hata vermeden hangi koşulda durdurulursa

durdurulsun o konteyneri yeniden başlat demektir.

Yani siz bir pod yarattınız.

O kodun tanımında bulunan konteyner yaratıldığı konteynerin içindeki uygulama çalışmaya başladı.

Ya işi bittiği için ya da hata verdiği için uygulama kapandı.

Dolayısıyla konteynır da kapandı.
==================
Fakat kodun restart policy tanımı always olarak set edildiyse ki siz özellikle failure ya da never seçmediyseniz

bu böyledir.

Bu konteyneri yeniden başlatır.

Eğer restart polisin never olarak set edildiyse, hiç bir durumda konteyner yeniden başlatılmaz.

10 failure seçildiyse de, tahmin edebileceğiniz üzere sadece hata alıp kapanırsa yeniden başlatılır.

Şimdi bu hatırlatmayı yaptıktan sonra Restart policy de öğrendikten sonra kod yaşam döngüsüne geri dönelim.

Nerede kalmıştık?

En son kodu Running State e getirmiştik arkadaşlar.

Bu noktadan itibaren kodun altında tanımlı konteynerlar çalışmaya devam ettikçe running olarak devam

eder.
=============================
Eğer konteynırların hepsi hata vermeden doğal olarak kapanırsa, restart polisi de never ya da on olarak

set edildiyse, kodun status u saksıda ya da diğer bir adıyla completed statüsüne döner ve kod başarılı

bir şekilde yaşam döngüsünü tanımlar.

Yine restart polisi never ya da failure olarak set edildiği durumda konteynerlardan birisi hata verip

kapanırsa bu sefer statusu taklit olarak işaretlenir ve yaşam döngüsünü tamamlar.

Fakat RestartPolicy always olarak set edildiyse işler biraz ilginçleşebilir.

Restart always olarak ayarlandığında konteynırların hatadan da kapansa normal de kapansa yeniden başlatılacağını

söylemiştik.

Dolayısıyla pod hiçbir zaman completed.

Ya da failed state'e geçmez.

Bunun yerine pod içerisinde konteynır yeniden başlatılır ve running state'e devam eder.
=================================
Fakat Kubernetes bu yeniden başlatma işlemini belirli bir sıklıkla yapıyorsa, bazı şeylerin ters gittiğini

kanaat getirir ve kodu Cashback adını verdiğimiz state'e sokar.

Crash Loopback'in anlamı şudur arkadaşlar.

Bak kardeşim sen bir pod oluşturdum ama bunun içindeki konteynır ikide bir kapanıp duruyor.

Ben bunu yeniden çalıştırıyorum ama gene kapanıyor.

Buna bir bak arkadaşlar.

Crash loopback off'a düşen pod da şunlar olur.

Kubernetes konteynır sık sık kapandığı ve yeniden başlatıldığı için bir şeylerin ters gittiğini anlar

ve crash loopback of çeker.

Sürekli restart etmek yerine restart eder.

Önce on saniye bekler.

Eğer on saniye içinde yeniden çökerse yirmi saniye bekler ve ondan sonra konteyneri yeniden başlatır.

Yine çökerse bu sefer 40 saniye bekler, yeniden başlatır, yine çökerse seksen saniye bekler, yeniden

başlatır.

Derken beş dakikalık aralığa çıkana kadar böyle devam eder ve ondan sonra da her beş dakikada bir bunu

sürdürür.

Eğer bu arada bir şekilde konteyner çökmeyi bırakırsa ve on dakika boyunca sorunsuz çalışırsa, konteyner

Crash Loopback of running e döndürür.

Bu olmazsa, artık siz müdahale edene kadar sonsuza dek her 5 dakikada bir konteynırı yeniden başlatır.

Uzun lafın kısası, Crash loop back görürseniz, bu konteynerin sürekli restart edildiğini ve bir şeylerin

yanlış gittiğini belirtir, müdahale edip düzeltmeniz gerekir diyelim ve burada bir mola verelim.

Teorisini ve neler olduğunu sanırım anladık.

Şimdi bir soluklanalım ve bir sonraki bölümde tüm bunları uygulamalı olarak görelim ve deneyelim.