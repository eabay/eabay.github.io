---
title: Seçici-geçirgen yazılımlar (EBEVEYN KONTROLÜ)
date: 2007-05-18 10:00:00
categories:
  - Software
---
Yapılan araştırmalar, çocuk ve gençlerin internette uygunsuz içerikle karşı karşıya kalmasına yönelik kaygının, anne-babaların bilgisayar satın alma konusundaki kararlarını maliyetten sonra en çok etkileyen unsur olduğunu ortaya koyuyormuş. İşte anne-babaların imdadına yetişen programlar.

<!--more-->

Her anne ve baba çocuklarına karşı korumacı bir tutum içerisindedir. Bu doğanın bir konunu. Hemen hemen tüm canlılar doğumdan sonra belli bir süreye kadar çocuklarının bakımını üstlenir ve onları doğanın sert kurallarını öğrenene kadar korumaya devam eder. Bilgisayar da artık doğa şartlarına uyumda bir kıstassa ve ne onla ne de onsuz oluyorsa bilgisayar ve internet kaynaklı tehlikelerden çocuklarınızı korumak için gerekli önlemleri almalısınız. Bu koruma yöntemi çocuğunuzun bilgisayar kullanım süresi ve amacını düzenlemek ve onları zararlı içeriğe sahip alanlardan uzak tutmak olarak özetlenebilir. Bazı durumlarda onların aktivitelerini izlemek de isteyebilirsiniz. Ama bizim tavsiyemiz yasakçı olmaktan çok yol gösterici olursanız her iki tarafın da bu işten daha karlı çıkması daha olası olacaktır. El elden, akıl akıldan üstündür. Siz çocuğunuza yasaklar getirdikçe o da karşı çözüm için sürekli çaba içinde olacaktır.

Bahsettiğimiz koruma işini yapmak üzere geliştirilmiş bazı programları sizlere sunmak istedik. İhtiyacınıza göre içlerinden birini seçebileceğiniz bu yazılımlar tabiÃ® ki piyasadakilerin sadece bir kısmı. Ama en azından sizlere karar verme aşamasında faydalı olacağına inanıyoruz.

## Netron Gözcü
{% img center /images/posts/software-gozcu.jpg %}

Her zaman bizim için çalışan Microsoft sağ olsun yine bizi düşünerek ebeveynler için çözüm ortağı Netron'a Gözcü adlı bir ebeveyn kontrol yazılımı yaptırarak Microsoft ve TTNet işbirliği ile düzenlenen *Her Eve Son Sürat İnternet, Her Eve Bilgisayar* kampanyasıyla satılacak tüm bilgisayarlarda önceden yüklenmiş olarak dağıtacak. .NET 1.1 (dikkat 2.0 değil!) kurulması şartı olan program ayrıca internetten de [indirilebilmekte](http://www.netron.com.tr/gozcu/netrongozcusetup.msi).

Program, izinli, yasak siteler ve sakıncalı sözcüklere göre site erişimini engelleme ya da erişime izin verme, internet ve bilgisayar kullanımını belirli saatlerde kısıtlama, etkinlik kayıtları, belirlenen yazılımların kullanımını engelleme gibi sıradan tüm işlevler için gayet güzel tasarlanmış. En azından Türkçe ve kolay anlaşılır. Ama gel gelelim klasik Microsoft huyundan da vazgeçilmemiş. Gözcü, *dünyadaki tek tarayıcı Internet Explorer'dır, diğerleri de ne ola* anlayışı nedeniyle sade IE ile yapılan ziyaretlerde işlevini yerine getirebiliyor. Eğer makinenizde Firefox, Opera gibi başka tarayıcılar da yüklüyse veya çocuğunuz bu programları kurabilecek yetkilere sahip bir kullanıcı hesabıyla çalışıyorsa o zaman ancak çocuğunuzun bilgisayar kullanımını ya da bu uygulamaların kullanımını engelleyerek sonuca ulaşabilirsiniz. IE'nin dünya üzerinde güvenlik açığı en çok olan tarayıcı olduğunu hesaba katarsanız çocuğunuzu bazı şeylerden korumak isterken bir yandan da bilgisayarınızı, doğal olarak da onu kullananları savunmasız bıraktığınızın farkında olmalısınız.

Son olarak da programdaki bazı garipliklere dikkat çekmek istedik. Evet, engelli siteler açılmak istendiğinde ya istenilen adrese (varsayılan netron.com.tr) yönlendiriliyor ya da bir uyarı mesajı çıkıyor. Ama uyarı mesajının ardında site yine de görüntüleniyor. Sayfa yüklendikten sonra pencere kapatılıyor (Gözcü'nün herhangi bir yasakta seçtiği müdahale şekli). Bir diğeri de `Yasak site listesini indir` butonu ile indirilen siteler. Birkaç kere denedik ama her seferinde indirilen listede sadece *hepsiburada.com* ve *haberturk.com* yer aldı. Netron'un sadece bu iki siteyi zararlı içeriğe sahip birer site olarak görmesi ilginç. Halbuki ne kendilerine ne de Microsoft'a rakip bile değiller :). Aynı şey yasak kelime listesinin indirilmesinde de yaşandı. İndirilen listede tek mantıklı olabilecek kelime `şiddet` idi. Diğerleri ise her sitede olabilecek kelimelerdi. Mesela bu listedeki kelimeler yüzünden google.com'u bile açamadık!

Site adreslerinin tam olarak verilmesi gerekliliği ise sizi zor durumda bırakabilir. Örneğin `alanadi.com` gibi bir adresin tüm alt alan adlarını engellemek ama bu adresi erişilebilir olarak bırakmak isterseniz `*.alanadi.com` gibi bir ifade kullanamıyorsunuz. `alanadi.com` girdiğinizde de tüm site engellenmiş oluyor. Üstelik kontrol mekanizması sadece adres içinde alan adını aramaktan ibaret olduğu için `www.digersite.com/a/alanadi.com` gibi bir adres de otomatik olarak engellenmiş oluyor. Bir de `www` önekli adresler sorununa değinelim. Siteyi yasaklı listesine `www.site.com` olarak kaydetseniz dahi eğer DNS kaydı tanımlıysa- site `site.com` adresinden hala erişilebilir olmaya devam ediyor. Bizce yeterince test edilmemiş bu programı IE zorunluluğunu da hesaba katarak kullanmayı göze alabiliyorsanız çocuğunuza neden bilgisayar aldığınızı bir kere daha düşünün.

*Mademki tavsiye etmeyeceksiniz neden yazıyı bu kadar uzattınız* diye düşünenleriniz olabilir. Uzattık çünkü bir Türk ürünü (her şeyiyle Türk olmasına rağmen kurulum ekranının İngilizce olmasına ve kurulumda adının Netron Parental Control olarak geçmesine de takılmadık değil!) olan bu programın reklam değil de gerçekten hizmet anlayışıyla tekrar elden geçirilmesi gerekliliğini düşündük.

**Site:** http://www.microsoft.com/genuine/offers/default.aspx?displaylang=tr

## System Surveillance Pro

{% img center /images/posts/software-system_surveillance.png %}

System Surveillance Pro aslında bir sistem gözlemcisi ama aynı zamanda sitelerin içeriklerinin engellenmesi ve program kontrolü için de kullanılabilmekte. Arka planda çalıştığından fark edilmemesi sayesinde çocuğunuzun bilgisayar başında neler yaptığını da rahatlıkla gözlemleyebilirsiniz. Örneğin klavyede girilen karakterleri zaman bilgileriyle beraber tutan yazılım tüm bu aktiviteleri size raporlayabiliyor. Yani siz çocuğunuzun hangi program açıkken neler yazdığını görebilirsiniz. Üstelik aynı zaman diliminde program tarafından alınmış bir ekran görüntüsü varsa onu da görüntülüyor. Böylece tam o anda bilgisayarda neler yapıldığına dair ayrıntılı bilgiler edinebiliyorsunuz.

Bizi daha çok ilgilendiren bölümlerden biri olan web siteleriyle ilgili bölümde de ziyaret edilenler, şüpheli içeriğe sahip olanlar ve engellenenlere ait kayıtları görüntüleyebiliyorsunuz. Varsayılan ayarda şüpheli siteler engellenmiyor fakat ayarlardan engellemenin etkin olmasını sağlayabilirsiniz. İzinli, yasaklı siteler ve anahtar kelimeler listelerine göre programın işini yapmasına olanak tanımak mümkün. Ne yazık ki System Surveillance Pro da IE dışı tarayıcı özürlü programlardan. Çocuğunuzun Firefox ya da farklı bir tarayıcı ile istemediğiniz sitelerde cirit atmasını istemiyorsanız daha önce de belirttiğimiz gibi ya yeni program kurmasına izin vermeyeceksiniz -ki yeni bir tarayıcı kuramasın- ya da kendi kurduğunuz diğer tarayıcı yazılımları yasaklı programlar listesine eklemeniz gerekecek.

Tam bu noktada değinmek isteğimiz bazı noktalar olacak. Zeka her ne kadar çevre faktörlerinin de ağır bastığı bir kalıtsal özellik olsa da nihayetinde çocuklar özelliklerini anne ve babalarından alır. Yani demek istediğimiz şu: çocuğunuz sizin aldığınız önlemlere her zaman en az sizin kadar akıllıca hamlelerle karşı atak geliştirecektir. Hele bilgisayara ilgili bir kişiyle o zaman işiniz epey zor. Aynen 100% güvenliğin olmadığı gibi yasakların da 100% başarı güvencesi yoktur. Siz hiç istemeseniz de sonuca ulaşmayı hedeflemiş bir azmi bu programların hiç biri gerçek anlamda engelleyemeyecektir. Eğer siz de aynı azimde bir kişiyseniz size gerçek olan tek çözümü sunalım; *Bilgisayarı kaldırın, atın!*.

Neyse kaldığımız yerden devam edelim. System Surveillance Pro anlık ileti yazılımlarını özel olarak takip edebilen bir özelliğe de sahip ama Ülkemiz için en çok kullanılan olan MSN'in 8 sürümü için bu destek yok.

Program birden fazla makine için tek ara yüzden kontrol imkanı sağlıyor. Çocuğunuzun makinesi ayrıysa bile kontrol için o bilgisayarın başına gitmeniz gerekmiyor. Üstelik takip etmek istediğiniz Windows kullanıcılarını seçebiliyorsunuz. Bu şekilde sadece çocuğunuz için oluşturduğunuz hesabı gözlemleyebilirsiniz. Belirlenen aralıklarla ekran görüntülerinin alınması, gözlem etkinliğinin gerçekleştirileceği zaman aralıklarının seçimi, kayıtların, uyarıların ve ekran görüntülerinin e-posta adresine gönderilmesi, `Görev yöneticisi` aracılığı ile ulaşılamayan, `Program Ekle/Kaldır` menüsünde görünmeyen, komut satırından `sspro` şeklinde vereceğiniz komut ve şifre çalışması System Surveillance Pro'nun artılarından. Ama dikkatli olun, kendi silahınızla vurulmayın! ;).

**Site:** http://www.gpsoftdev.com

## WebSec Professional

{% img center /images/posts/software-websec.png %}

Yine Türk yapımı bir program olan WebSec Professional diğer programlarda olmayana sahip, tarayıcı bağımsızlığı. İşte çocuğunuz şimdi hapı yuttu! :).

WebSec Professional kurulumu ve kullanımı oldukça basit. Sahip olduğu filtreleme teknolojisi sayesinde sizi adresleri tek tek izinli ve yasaklı listesine eklemekten kurtarıyor. Böylece her yeni alan adını ziyaret ettikten sonra yasaklamaktansa tehlikeyle karşılaşma anında tedbirinizi otomatik olarak almış olmanızı sağlıyor. Alan adı veya içeriğinde zararlı bir site olma olasılığı bulunan siteler görüntülenmeden önce bir uyarı ekranı ile engelleniyor. Üstelik bunu da çok hızlı yapıyor. Yani internet gezintiniz sırasında her site ziyareti öncesi hissedilir derecede fazladan bir zamanınız alınmamış oluyor.

Programın iddiası 165 dilde de bu işi yapabilmesi. Bu kadar çok dil bilmediğimiz için test etme olanağımız olmadı ama en azından Türkçe ve İngilizce'de başarılı olduğunu söyleyebiliriz. Antivirüs programlarındaki sezgisel taramaya benzetebileceğimiz özelliğinin yanında dilerseniz güvenli ve yasaklı site listesi ile yasaklı kelime listesi oluşturabilirsiniz. Üstelik yasak kelimeler için `ve`, `veya` mantıksal operatörleri ile çeşitli kombinasyonlar da kullanılabiliyorsunuz. IP adresi ile site girişleri de size daha esnek bir filtreleme sistemi sunuyor. Örneğin IP girişi ile aynı IP adresine sahip tüm adreslerin yolunu açabilir veya engelleyebilirsiniz.

120 kategori ile çocuğunuzun hangi başlıktaki sitelere erişebileceğini de belirleyebildiğiniz WebSec Professional ile onların bilgisayar başında istemediğiniz sitelerde vakit geçirmesinin önüne geçebilirsiniz.

Raporlama bölümüne baktığımızda WebSec size biraz yetersiz gelebilir. Sadece engellemelerin tarihi ve türünün yer aldığı raporlar grafiksel olarak görüntülenebiliyor. Grafikler kural elemeleri ve yasak site girme sıklığından oluşuyor.

Şifre koyma sayesinde çocuğunuzun olası müdahalesinden uzak tutacağınız program, Windows ile beraber başlayarak görevini sessizce yerine getiriyor. *Önemli olan işlev, özellik sayısı değil* diye düşünüyorsanız WebSec'i denemenizi öneririz. Yalnız bunun için bir süre beklemeniz gerekecek. Çünkü program 2.0 sürümü için geliştirme sürecinde ve şu anda satışta değil. Eğer sistem gözleyici tarzı bir programla ilgileniyorsanız aynı firmanın Sentinel adlı ürününü gözden geçirmenizi öneririz.

**Site:** http://www.horizonum.com

## MY TR Filter Pro

{% img center /images/posts/software-mytrfilter.png %}

MYTR Filter, kendi kendine öğrenebilen ve sürekli veritabanını geliştiren bir altyapı ve çoklu dil desteğine sahip. Program, web sayfası içinde bulunan, metinlerden, başlığa, adrese ve veritabanına hazır olarak girilmiş 29.000'den fazla web adresine kadar çok geniş bir alanda koruma sağlayabiliyor. Porno, terör, müşterek bahis, kumar vb. sayfaları engellemenin yanında truva atı, reklam yazılımı gibi bilgisayarınıza zarar veren ve internet trafiğinizi gereksiz yere meşgul eden reklam sayfalarını da engelleyebiliyor. MSN ve ICQ gibi sohbet içerikli programları da istenildiğinde engelleme özelliğine sahip. Bunun yanında sadece kullanıcının istediği internet sayfalarına girilmesine imkan tanıyan seçenekler de mevcut. Diğer yandan Windows'un hosts dosyası filtrelemesi, görev yöneticisi şifrelemesi, gezilen sayfaların tarihçesini tutması gibi birçok özelliği bünyesinde barındırıyor.

MYTR Filter sayfa engelleme için e-posta filtreleme yazılımları tarzı bir yöntem kullanıyor. Yasaklı kelime listesindeki her kelimenin bir puanı bulunuyor. Eğer bir sitenin içeriğinden dolayı sahip olduğu yasaklı kelimelerin puan toplamı belirlenen puanı geçerse site açılmıyor. Bunun dışında kelimelerin kökü ve türetilmiş halleri, birleşik kelimeler (aslında `keli*` tarzı arama kastediliyor) için arama yapılırken ne kadar hassas olunabileceğini ayarlamak mümkün.

Programda diğer bir ilginç özellik de dosya indirme işlemlerinde indirilen dosyanın uzantısına göre engelleme yapabilme.

**Site:** http://www.myyazilim.com, http://www.bigsoft.com.tr

## Optenet PC

{% img center /images/posts/software-optenet.png %}

Ağzımıza sakız olan ama önemli olduğunu düşündüğümüz tarayıcı bağımsız bir program daha, Optenet PC. Şu ana kadar bahsettiğimiz standartları içermesinin yanı sıra Optenet filtreleme için kullandığı yasak listesini sürekli güncel tutarak tüm müşterilerine satış sonrası hizmetini vermeye devam ediyor.

Kategori temelli izinler ile tek tek adreslerle uğraşmıyorsunuz. Web erişimini günlük ve saat bazında ayarlayabiliyorsunuz. Size en fazla 3 zaman aralığı tanımlama şansı veren bu alanlar biraz anlamsız bir tasarım olmuş, bu yüzden programın kullanışlılığını doğal olarak da sizi biraz kısıtlıyor.

Çoklu profil tanımlaması sayesinde kullanıcı adı/şifre ikilileri oluşturup farklı kişilere farklı erişim yetkileri tanımlayabiliyorsunuz.

Optenet'te bağlantı noktası temelli engelleme özelliği de yer alıyor. Bu sayede dosya indirme ağları, anlık ileti, haber grupları, e-posta, sohbet gibi birçok farklı alanda da filtreleme yapılabiliyor. Dilerseniz izin verilecek ya da engellenecek bağlantı noktalarını da kendiniz belirleyebiliyorsunuz. Böylece standart bağlantı noktalarını kullanmayan program ve sitelerin görüntülenmesinin de önüne geçmiş oluyorsunuz. `Navigation history` ile geçmiş kaydı da tutan programı hız açısından başarılı bulduğumuzu söylemek isteriz.

**Site:** <a href="http://www.optenetpc.com" target="_blank">www.optenetpc.com</a>

## Safe Child

{% img center /images/posts/software-made_safe_child.png %}

Çocuklarınızı internetteki zararlı içerikten uzak tutabilmek için geliştirilen yazılımlardan madeSafe Child filtreleme yöntemini kullanır. Açılır penceler, sohbet odaları, haber gruplarını kolaylıkla kullanım dışı bırakabileceğiniz gibi anahtar kelimeler yoluyla siteleri engelleyebilir, güvenli siteleri süzme işlemi dışına bırakabilirsiniz ya da adres belirterek bir sitenin görüntülenmesini tümüyle durdurabilirsiniz. Sahip olduğu tarih geçmişi ekranı sayesinde de yapılan işlemleri tek tek kontrol edebilirsiniz.

Standartların çok altında olan Safe Child programını size sadece bir seçenek olarak sunmak istedik.

**Site:** http://www.eurosoft.com.tr

> Bu yazı Kasım 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
