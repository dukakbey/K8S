ilk olarak şunu aktarmak istiyorum.Şu ana kadar hep Kubernetes Cluster ile ilgili bilgiler edindik. Nedir, ne işimize yarar, nasıl kurar, nasıl bağlanırız bunu gördük.

Kubernetes üstünde konteyner imajları haline getirdiğimiz iş yüklerimizi koşturmak istiyoruz.

Yani Kubernetes üzerine bir şeyler deploy etmek istiyoruz.İşte Kubernetes üzerinde deploy ettiğimiz, çalıştırdığımız, koşturduğumuz şeyler objelerdir,Kubernetes üzerinde çeşitli tiplerde objeler yaratır, siler modifiye ederiz.

Kubernetes üstünde her şey bir API objesidir ve bizler onun üstünde koşturmak istediğimiz işyüklerini bu objeler şeklinde oluşturup ayarlarız.

Kubernetes üzerinde oluşturabildiğimiz en temel objede pod pod, Kubernetes oluşturup yönetebileceğimiz en küçük ve temel birimdir.

Pod kavramını anlamak şu ana kadar hep klasik konteynırlarla uğraştığımız için biraz zor olacaktır. O nedenle dikkatli dinlemenizi rica ediyorum.

- Arkadaşlar bizler Kubernetes hayatımıza girmeden önce.İlk olarak Docker ile tanıştık.Docker ile uygulamalarımızı container imajları haline getirdik.Bunları docker engine üstünde konteynırları olarak çalıştırdık.Kubernetes de bir konteynır orkestrasyon aracı olduğuna göre bunu yapıyor. Konteynerları dağıtık bir yapıda çalıştırma işlemini yönetiyor olması lazım.
Evet Kubernetes ile bunu yapıyor fakat Kubernetes ile bizler direkt konteyner oluşturamayız.

Yani.
Git bana konteyner çalıştır diyemeyiz.Sonunda yine o ortamda çalışan şey konteynerdır ama Kubernetes tarafında bunu tanımlarken konteyner olarak tanımlayıp deploy etmeyiz.

- Kubernetes dünyasında oluşturabildiğimiz en küçük obje.Pod pod içerisinde bir ya da birden fazla konteynır barındırabilen En temel Kubernetes objemizdir.

Nasıl ki bizler docker container run diyerek. docker üzerinde bir konteyner oluşturabiliyorsa Kubernetes de kubectl run diyerek bir pod oluştururuz.
Şimdilik siz pod eşittir container olarak düşünün.Zaten %99'da biz bir pod içerisinde tek bir konteyner çalıştırırız.

Bizler Kubernetes API ile pc üzerinden haberleşerek ona bak kardeşim.

Bana içinde şu imajı kullanarak oluşturacağım bir konteyner bulunan pod yarat, özellikleri de şunlar

olsun, işte ismi şu olsun, şu etiketleri alsın vesaire deriz ve Kubernetes bunu oluşturmak için çalışmaya

başlar:
============
Öncelikle her pod bir unique identifier olması gerekir.

Bu nedenle bir unique identifier oluşturulur ve pod atanır.

Kubernetes altında her kodun bir IP adresi olması gerekir.

Sıradaki boş IP adresi seçilir ve pod atanır.

API Server Bu da bizim tanımladığımız bilgiler ve unique id, IP adresi gibi bilgileri harmanlayarak

bir pod tanımı yapar ve veritabanına kaydeder.

cube scheduler Komponenti sürekli buraya gözler ve herhangi bir worker node ataması yapılmamış pod tanımı Hanımı görürse,

o kodun çalışması için uygun bir worker seçer ve bu bilgiyi kod tanımına ekler.

Sonrasında worker node üstünde çalışan servisi de bu etc sürekli gözlediği için kod tanımını görür ve

bu tanımda belirtilen container worker node üzerinde oluşturulur.

Böylece kod oluşturulma aşamaları tamamlanır.
============

Şimdi şu ana kadar öğrendiklerimizi bir özetleyelim arkadaşlar.

Ne dedik?

Kubernetes üzerinde bizler objeler yaratırız.

Kubernetes üzerinde iş yükleri çeşitli objeler şeklinde tanımlanır ve ayarlanır.

Kubernetes üzerinde oluşturduğumuz en temel obje pod pod içerisinde bir ya da birden fazla container

çalışabilir.

Ama çoğu durumda pod içinde bir konteyner çalıştırırız.

Her kodun minik bir identifier vardır.

Kubernetes altında her koda bir IP adresi atanır.
