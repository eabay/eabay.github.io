---
title: Zend Studio
date: 2007-05-18 09:00:00
categories:
  - PHP
  - Software
---

{% img right /images/posts/zend-studio.png %}

Web programlama dillerinden en popüleri PHP ile uygulama geliştirenlerin işini kolaylaştırmak için gerekli araçlardan en önemlisi olan Zend Studio'yu incelemeye çalıştık.

<!--more-->

PHP geliştiricilerin kod yazarken ihtiyaç duydukları araç tabiÃ® ki bir metin düzenleyicidir. En basit metin düzenleyici programın bile yetebileceği PHP'de daha üretken olabilmek ve zamanı iyi kullanabilmek için bir uygulama geliştirme ortamına (IDE, Integrated Development Environment) sahip olmak programcının daha hızlı çalışabilmesini sağlar.

Dreamweaver gibi araçların kodu renklendirmekten öteye gidememesinden rahatsız olmaya başladığınızda ve daha ciddi uygulama süreçlerinin içerisine sürüklendiğinizde size yardımcı olabilecek araçlardan biri ve en iyisi de Zend Studio. Fiyat konusunda sizleri zorlayacağını düşünüyorsanız da açık kaynak alternatif Maguma Open Studio ve Eclipse hemen yanınızda.

## Zend Studio

{% img center /images/posts/zend-ekran.png %}

Bir PHP uygulama geliştirme ortamından bekleyebileceğiniz her şey Zend Studio içersinde var dersek sanırız çok da abartmış olmayız. Ne de olsa sloganı `The php Company` olan bir şirketin ürünü ve bu şirket PHP'nin geliştirilmesi sürecinin tam da ortasında.

Zend Studio düzenleme, test etme ve hata ayıklama işlerinin tümünü tıpkı diğer uygulama geliştirme ortamlarında olduğu gibi aynı pencerede yürütebilmenizi sağlayan bir tasarıma sahip. Böylece kodunuzu da gözünüzden ayırmadan tüm kontrolü elinizde tutabiliyorsunuz.

{% img center /images/posts/zend-belge_tipi.png %}

PHP, HTML, Javascript, CSS, XML, JSP gibi web ile ilgili belgelerde renklendirme yapabiliyor. Eğer uzantısından tanınamayan bir belge açılmak istenirse hangi renklendirme şablonunun kullanılmadı gerektiğini siz seçebiliyorsunuz.

{% img center /images/posts/zend-snippet.png %}

Zend Studio sadece PHP konusunda yol almışların rahat etmesini sağlayan bir program değil. Sahip olduğu kod örnekleri bölümü zend.com sitesindeki veritabanından da güncellenebiliyor ve böylece daha az tecrübeli geliştiricilerin de programlama süreçlerini kolaylaştıran katkılar sağlamış oluyor.

{% img center /images/posts/zend-otomatik_tamamlama.png %}

Geliştiricinin en çok rahat edeceği özelliklerden bir tanesi de otomatik tamamlama. Tüm PHP fonksiyonlarının ve sizin tanımlamış olduğunuz sınıf ve fonksiyonların siz yazarken seçim listesi olarak gelmesi ve aldığı parametreleri de göstermesi sizi sürekli olarak belge ve kod incelemekten alıkoyuyor. Ayrıca hata olan satırın kelime işlemci programlardaki imla hatalarında olduğu gibi vurgulanması ve orta panelin sağında küçük kırmızı çizgiler ile satırın belirtilmesi yine hata yapılmaması için iyi bir önlem. Bu özellik çalıştığınız sayfaya dahil diğer sayfalarda yaptığınız tanımlamaları da içeriyor.

{% img center /images/posts/zend-inspectors.png %}

Eğer sayfanızdaki tüm sınıf ve fonksiyonları, eğer bir proje oluşturduysanız tüm projedekileri ya da tüm PHP fonksiyonlarını görüntülemek isterseniz sol taraftaki `Inspectors` paneli çok işinize yarayacak.

{% img center /images/posts/zend-gotodeclaration.png %}

Yine programcıyı hızlandıran özelliklerden biri de fonksiyonun tanımlı olduğu sayfaya kolay erişimi sağlayan akıllı yönlendirici. Ctrl tuşuna basılı tutarak fareyi bir fonksiyon veya sınıf üzerine getirdiğinizde ve tıkladığınızda sizi tanımlandığı yere yönlendirecek.

{% img center /images/posts/zend-sqlserver.png %}
{% img center /images/posts/zend-sql.png %}

Web uygulaması geliştiriyorsanız veritabanı işlemlerini göz ardı etmek olmaz. Zend Studio'nun sahip olduğu veritabanı desteği birçok türdeki veritabanına erişebilmenizi ve sorgulama yapabilmenizi sağlıyor. Sorgu geçmişi ve dönen verilerde düzenleme yapabilme gibi ayrıntılar da fazladan bir veritabanı yönetim aracı kullanma gereksinimini ortadan kaldırıyor.

{% img center /images/posts/zend-ftp.png %}

Bazen yerelde değil de doğrudan sunucu üzerinde değişikler yapmak isteyebilirsiniz. Böyle bir durumda FTP/SFTP desteğini kullanarak indir-düzenle-geri yükle zahmetinden kurtulabilir, değişiklikleri anında sunucunuzda görebilirsiniz. Yeni eklediğiniz FTP sunucuları `File Manager` panelindeki `File Sources` altında yeni bir disk olarak görünecek. Dosyaya çift tıklayıp açtıktan sonra kaydetme ile beraber dosya sunucuya yüklenecek.

### Kod Analizi  
Kodu yazdınız ve analiz etmesi için bir arkadaşınızın gözden geçirmesiniz istediğiniz. Ama arkadaşınızın da işi var. İşte bu noktada Zend Studio sizin çok daha yakın bir arkadaşınız olacak. Kodunuzu inceleyerek size önerilerde bulunabilir. Özellikle de güvenlik konularında çok hassas.

### Hata Ayıklama  
Zend Studio'nun en önemli özelliği diyebiliriz. Normalde derlenen diller için kullanılan hemen hemen tüm hata ayıklama süreçleri ve özellikleri yorumlanan bir dil olan PHP için de gerçek kılınmış. Adım adım ilerleme ile kodun tam olarak nasıl çalıştığını görme (step over), kırılma noktası (break point) ekleme, ortam değişkenlerini gözleme, kod çıktısını metin ya da HTML sayfası olarak anında görebilme gibi özellikler sayesinde işinizin sonucunu başka bir tarayıcı açmadan da kolaylıkla takip edebilirsiniz.

### CVS/SVN desteği  
Bir yazılım grubu olarak çalışanların (ya da düzenli olarak çalışmak isteyenlerin) kaynak kodu yönetimi ve sürüm kontrolü için kullandığı CVS ve onun biraz daha geliştirilmişi olan SVN sistemlerinin de Zend Studio tarafından desteklendiğini söylediğimizde sanırım bazılarınız sevinecek. En azından biz sevinmiştik :). Ayarlardan sunucu tipi ve bilgilerini girdikten sonra desteklenen birçok standart komut ile sürüm kontrollü çalışabilirsiniz.

### Belgeleme desteği  
Eğer belgelemeye önem veriyorsanız PHPDocumentor eklentisi sayesinde bu işi otomatik olarak yapabilirsiniz. Tabii ki bunun için PHPDoc formatına uygun bir kod yazmış olmalısınız. Yorum satırından kaçan programcılar için pek de önemli olmasa gerek :D.

### Web servis desteği  
Piyasanın yavaş yavaş servis tabanlı hizmetlere doğru kaydığını göz önüne alırsak web servislerini de destekleyen Zend Studio'ta iyi demek için bir neden daha bulabiliriz. WSDL belgelerinizi oluşturmak için sihirbaz ile işinizi kolaylaştırıyor ve web servislerinizi tanımlamanızı sağlıyor.

### Profil Çıkarma  
Zend Studio ile sayfalarınıza ait performans testleri yapabilir ve grafiksel sonuçlar ile kodunuzu tekrar değerlendirebilirsiniz. Sonuçlar size kodunuzun ne kadar zamanda çalıştırıldığı gibi bilgileri sunuyor.

Bazı özellikler Zend Studio'nun diğer Zend ürünleri ile ortak çalışmasına ait olduğundan bunlara yer vermedik. Ama ilgilenen okurlarımız için bunların Zend Studio Server ve Encode olduğunu söyleyebiliriz. Zend Encode ile kodunuzu şifreleyebilir ve iyileştirebilirsiniz.

> Bu yazı Aralık 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
