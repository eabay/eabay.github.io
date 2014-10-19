---
title: Bahar kokulu web uygulamaları
date: 2007-05-16 09:00:00
categories:
  - AJAX
  - Javascript
---
{% img right /images/posts/ajax-logo.jpg %}

'Bu siteyi AJAX'lasak da mı yapsak, AJAX'lamasak da mı yapsak?'. Eğer bu tekerlemeyi hızlı bir şekilde söyleyebiliyorsanız siz olayı çözmüşsünüz, bu sayfada vakit kaybetmenize gerek yok, hemen bir sonraki konuya geçebilirsiniz.

<!--more-->
  
## Nedir bu AJAX?  
Cruyff, Bergkamp, Davids, Kluivert, Laudrup kardeşler sizlere bir şeyler çağrıştırıyor mu? Bir zamanların fırtına takımı Ajax. Ya da beyazları daha beyaz, renklileri daha renkli yapa yapa yakında bizi ışıltıdan kör edecek, olmadı renk körü edecek temizlik kimyasallarından Ajax'ı bilmeyeniniz var mı? Yok mu? O zaman site ustabaşılarının yeni sayfa yapım tekniği olan AJAX'ı kesin duymuşsunuzdur.

AJAX, ecnebicede 'eyceks' diye okunan, açılımı 'Asynchronous JavaScript And XML (Eşzamanlı Olmayan JavaScript ve XML)' olan ve Web 2.0 akımıyla beraber yayılmaya başlayan, etkileşimli web uygulamaları geliştirebileceğiniz bir teknik. Biz yazımızın geri kalanında 'acaks' diye okuyacağız. :)

AJAX ile geliştireceğiniz web uygulamalarının kullanıcı ile daha etkileşimli olmasının temelinde yatan ve onu klasikten ayıran etken sunucu ve istemci arasında daha küçük miktarda veri iletimi. Bağlantılara tıklanmak suretiyle sunucudan bulunulan isteklerde sayfanın tamamı yerine sadece bir kısmı güncelleniyor ve böylece sayfanın aynı kalan bölümleri gereksiz yere trafikte yer işgal etmiyor. Böylece sayfanızın hızı ve kullanışlılığı artıyor ve ziyaretçilerinize daha rahat bir sürüş keyfi yaratıyor.

## AJAX nelerden ibaret?  
AJAX adı gibi JavaScript (JS) ve XML'in eşzamanlı olmayan paslaşmalarının bir karışımı (Tabii ki HTML (ya da XHTML), CSS vazgeçilmez diğer unsurlar ama bunlar olmadan sayfanız da var olamayacağından anlatımlarda fazladan belirtme gereği duymayacağız). Burada JS bizim istemci tarafındaki veri işleme dilimiz, XML de sunucudan istemciye veri iletiminde kullanacağımız dosya biçimidir. Son cümlenin üzerinde biraz düşündüğünüzde aklınıza 'O zaman bu sunucu-istemci iletişimde farklı dil ve dosya biçimi kullanılabiliyormuş.' gibi bir cümle gelebilir. Aslında evet. AJAX bir standart değil bir tekniktir. Her ne kadar adı bu şekilde konmuşsa da aynı işlevleri görebilecek farklı seçeneklere de sahipsiniz. Örneğin JS yerine JScript (ikisi farklı diller), XML yerine de HTML kullanılabilir. Genellersek de sunucudan gelen veriyi işleyebilmek için DOM (Document Object Model â€“ Döküman Nesne Modeli) erişimine sahip bir istemci taraflı dil ve sunucudan gelen verinin biçimi, konunun ana fikrini oluşturmakta.

Sürekli olarak sunucudan gelen veriden ve bu veriyi ne ile işleyeceğimizden bahsettik ama peki biz sunucuya ne istediğimizi nasıl söyleyeceğiz? Sonuçta yapmak istediğimiz sayfayı yenilemeden sunucuya istekte bulunup gelen veriyi de işleyerek sayfanın istediğimiz yerinde güncelleme ile görüntülemek. Sunucu ile eş zamanlı olmayan iletişim için taleplerimizi XMLHttpRequest nesnesi kullanarak gerçekleştireceğiz. Bu nesne şu anda piyasadaki bilinir tarayıcıların hepsinin son sürümlerinde desteklenmekte. Halen bazı AJAX çatıları tarafından kullanılmaya devam edilen sayfa içi çerçeve (IFRAME) ile de sayfa içeriğine müdahale yöntemleri de eskiden beri kullanılan â€“hatta AJAX'ın adının AJAX olmadığı zamanlardan :p- ve kabul gören yöntemlerden. IFRAME etiketi ile yüksekliği ve genişliği sıfır olan, yani görünmeyen, bir pencere içerisinden sayfa içeriği güncellenebilmekte. Bu da klasik web uygulamalarına biraz daha yakın bir yöntem olarak görülebilir.


{% img center /images/posts/ajax1.jpg %}

## Çok yeni bir teknik mi?  
Daha önce de söylediğimiz gibi, AJAX adı ile kendini her ne kadar kısıtlasa da benzer tekniklerin izlerine daha öncesinde internet aleminde rastlanıyordu. Yani AJAX sadece kullanım şeklini derleyip toparlayarak bu tekniğin adını koymuş oldu.

## Artıları, eksileri  
Sunucu ile istemci arasında gönderilip alınan verinin nispeten çok daha az olması ve dolayısıyla da artan hızı nedeniyle sayfalarınızın çekiciliği artıyor. Mesela bir veri tablosunda sildiğiniz satır için tüm tablo yeniden yüklenmek yerine sadece o satır tablodan kayboluyor. Bu sizin de bütçenize yansıyor. Çünkü bu memnuniyeti maddi çıkarlarınız için kullanabildiğiniz gibi bant genişliği için ödediğiniz parada da hissedilir bir düşüşe, yani kara neden oluyor.

Eksileri ise aşağı yukarı tamamen teknik nedenlerden kaynaklanıyor. En önemli sorun, istemci taraflı yanının ciddi bir yüzdeye sahip olmasından dolayı tarayıcı çeşitliliğine uyum sürecinin size kodlamada vakit ve çaba olarak geri dönmesidir. Bu aslında HTML ve CSS ile süregelen ortak bir sorun olmasına rağmen görselliğin biraz daha öne çıktığı AJAX uygulamalarında JS'nin de eklenmesiyle beraber artarak devam ediyor. Eğer ziyaretçileriniz AJAX desteği olmayan modellerdense onları gözden çıkarmak ya da onlara özel bir de AJAX'ı olmayan site yapmak zorundasınız. Yani olmak ya da olmamak gibi yapmak ya da yapmamak iki taraftan da size belli bir bedele mal oluyor.

## Sonuç  
İstediğiniz kadar kaçın, sonunda yüzleşmeniz gereken bir gerçek olan AJAX'ı öğrenmek zorundasınız! Tabii ki bu lafımız kendini site ustabaşı (ecnebice: webmaster) olarak tanımlayanlara. Bakın Google'ın yaptıklarına; GMail, Google Map. Aklın yolu bir.

{% img center /images/posts/ajax2.jpg %}

PC Tech size bu süreçte yardımcı olacak yazı dizisine bu yazıyla beraber başlamış oldu. Giriş niteliğindeki bilgilendirmenin ardından uygulama safhalarına bir sonraki sayı ile devam edeceğiz. Kalın sağlıcakla.


### Tarayıcı Desteği

#### AJAX desteği olan tarayıcılar
* Microsoft Internet Explorer 5.0 ve üstü (Mac OS sürümleri desteklenmiyor)
* Gecko tabanlı tarayıcılar (Mozilla, Mozilla Firefox, SeaMonkey, Camino, Flock, Epiphany, Galeon ve Netscape 7.1 ve üzeri)
* KHTML API 3.2 ve üzeri kullanan tarayıcılar (Konqueror 3.2 ve üstü, Apple Safari 1.2 ve üzeri
* Opera 8.0 ve üzeri (Opera Mobile Browser 8.0 ve üzeri dahil)

#### AJAX desteklemeyen tarayıcılar  
* Opera 7 ve altı
* Microsoft Internet Explorer 5.0 ve altı
* Metin tabanlı tarayıcılar (Lynx, Links gibi)
* Görme engeli olanlar için tasarlanmış tarayıcılar
* 1997 yılından önce geliştirilen tarayıcılar

> Bu yazı Mayıs 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
