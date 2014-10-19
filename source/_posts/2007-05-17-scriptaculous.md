---
title: script.aculo.us
date: 2007-05-17 10:00:00
categories:
  - AJAX
  - Javascript
---

{% img center /images/posts/scriptaculous_logo.png %}

Geçen ayki prototype pencere sınıfı örneğinden sonra sıradaki prototype tabanlı kütüphanemiz script.aculo.us. script.aculo.us Web 2.0 uygulamaları geliştirenlerin projelerine hoş efektler ekleyebilecekleri bir javascript kütüphanesi.

<!--more-->

Uzun bir zamandır dergimizde sizlere AJAX konusunda çeşitli bilgiler vermeye, örnekler ile kütüphaneleri nasıl kullanabileceğinize dair örnekler vermeye çalışıyoruz. Türkçe olarak internette çok kısıtlı içeriğin yer aldığı bu konuda PC Tech olarak sizlere uzman düzeyinden ziyade başlangıç düzeyi bilgiler vererek en azından işin bir ucundan AJAX bulaşmanızı ve geleceğin web uygulamalarını geliştirenler arasında yer alabilmenizi sağlamak asıl amacımız. Balık tutmayı öğretmek balık vermekten iyidir. Eğer bu yeni akıma dahil olduysanız ve kendi uygulamalarınızı geliştirme süreci içerisindeyseniz size Türkçe bir AJAX grubuna yönlendirelim. *Ajax Nedir* adlı bu gruba [üye olabilirsiniz](http://groups.google.com/group/ajaxnedir). Emekleme aşamasındaki bu kullanıcı topluluğunun ilerlemesine katkıda bulunmak isteyenlere duyurulur. İngilizce içerik içinse ajaxian.com'u takip ederek gelişmelerden haberdar olabilirsiniz.

Şimdi gelelim asıl konumuza, script.aculo.us. Yine söylemekten kendimizi alamayacağız ama script.aculo.us prototype çatısı üzerine kurulmuş ve tabir-i caizse yanarlı dönerli sayfalar tasarlamak için birçok görsel efekti size sunan bir kütüphane. Kütüphane içerisinde efektler yanında sürükle-bırak, sıralama, otomatik tamamlama gibi işlerinizi kolaylaştıracak kontroller de yer alıyor. Ayrıca DOM elemanlarını (daha açık olmak gerekirse HTML tarzı kodları) üretebilen özelliğini de dinamik olarak sayfa içi güncelleme sırasında kullanabilirsiniz.

## Kullanım  
http://script.aculo.us adresinden indirebileceğiniz kütüphanenin arşiv dosyasında birçok JS dosyası yer alıyor. script.aculo.us kütüphanesinin doğru çalışması için gerekenlerden `prototype.js`, `scriptaculous.js`, `builder.js`, `effects.js`, `dragdrop.js`, `slider.js` and `controls.js` dosyalarını bir klasöre aktarın ve script.aculo.us kullanmak istediğiniz sayfanın `head` etiketi içerisinde bağlantı verin.

```html
<script type="text/javascript" src="js/prototype.js"></script>
<script type="text/javascript" src="js/scriptaculous.js"></script>
```

`scriptaculous.js` dosyası varsayılan olarak tüm diğer javascript dosyalarını yükler. Eğer sayfa içerisinde sadece kullanmak istediğiniz özelliğe ait dosyaları yüklemek isterseniz kodu aşağıdaki gibi düzenleyebilirsiniz.

```html
<script type="text/javascript" src="js/scriptaculous.js?load=effects,dragdrop"></script>
```

Burada virgüller ile ayrılmış değerler klasöre kopyaladığınız dosyaların isimlerinden ibaret. Örnekler vermeye başladıkça hangi dosyanın nerede kullanıldığını daha rahat anlayacaksınız. Ama dikkat edilmesi gereken nokta bu paketlerin (özelliklerin ayrı olarak dosyalanmasından dolayı bu kelimeyi tercih ettik) birbiri ile olan bağımlılık durumunun gözden kaçırılmaması.

Bir script.aculo.us efekti kullanmak istediğimizde bunun iki yolu var. Birincisi istediğimiz fonksiyonu çağırmak;

```javascript
Effect.Fade('element_id')
```

Diğeri de sayfa elemanı özelliklerinde istediğimiz efektin sınıfından birini kopyalayarak olaya bağlamak.

```html
<div onclick="Effect.Shake(this)">
    Salla beni
</div>
```

İlk yöntemde sayfa tarayıcı tarafından yorumlanırken bu kısma gelindiğinde javascript kodu da çalıştırılacak, ikinci de ise DIV ile sınırlandırılan bölgeye tıklandığında efekt bu etikete uygulanacak.

Uygulanabilecek tüm efektlerin listesi şu şekilde:

* Effect.Highlight  
* Effect.MoveBy  
* Effect.Opacity  
* Effect.Parallel  
* Effect.Scale  
* Effect.Appear  
* Effect.BlindDown  
* Effect.BlindUp  
* Effect.DropOut  
* Effect.Fade  
* Effect.Fold  
* Effect.Grow  
* Effect.Puff  
* Effect.Pulsate  
* Effect.Shake  
* Effect.Shrink  
* Effect.SlideDown  
* Effect.SlideUp  
* Effect.Squish  
* Effect.SwitchOff

Tüm efektlerin nasıl çalıştığını http://wiki.script.aculo.us/scriptaculous/show/CombinationEffectsDemo adresinden kontrol edebilirsiniz.

Bir efekte değiştirgen parametre ile değer geçirmediğiniz sürece varsayılan değerler ile işini yapacaktır. Dilerseniz bu parametrelerin neler olduğuna da bir bakalım.

Bir efektin genel kullanımı

```javascript
new Effect.EffektAdi(element_id, gerekli-parametreler [, secenekler]);
```

şeklindedir. Her efekt için gerekli parametre yok. Kullanılan parametreler ve seçenekleri örneklerde geçtiğinde açıklamaya çalışacağız.

Küçük bir örnek vermek gerekirse de

```javascript
new Effect.Opacity(this, {duration: 0.5, from: 1.0, to: 0.0});
```

Kodu bir olaya bağlamak olarak verdiğimiz 2 yöntemdeki gibi bir kullanımla sayfa elemanını (örneğin `div`) 0.5 saniye içinde görünmez hale getirecektir `0.0` değerini 0'la 1 arasında bir değer olarak belirlerseniz de şeffaf bir görünüm elde edebilirsiniz. Ya da `from` seçeneği sayısal değer olarak `to` seçeneğinden daha küçük olursa şeffaflığı azalan bir görünüm oluşacaktır.

Aslında bu sayı AJAX yazısı biraz kısa gibi oldu ama script.aculo.us ile en az 1-2 sayı daha uğraşacağımızı göz önünde bulundurduğumuzda biraz sindirerek gitmek gerektiğini düşündük. O yüzden efektlerin nasıl kullanıldığına dair ısınma turlarını içeren bu yazının ardından kontrolleri de katarak Web 2.0'a yakışır sayfaları tasarlamayı sonraya bırakmak istedik. Bu ay örnekler olmadığından size örnekleri test edebileceğiniz bir adres de veremiyoruz. Ama bir sürprizimiz var! Pctech.com.tr yenilendi. Aslında bu satırları yazarken son rötuşlar yapılmaya devam ediliyor bu yüzden aksilik çıkmazsa diye sonuna eklememiz gerek. Ama yeni haliyle beraber daha güncel ve dolu dolu bir pctech.com.tr'de de AJAX ile olan sohbetlerimize yer vermeyi düşünüyoruz. İçerik olarak iddialı olacağımızı şimdiden söylemek isterim. Ödev yok, paydos! :)

## Desteklenen Tarayıcılar  
* Microsoft Internet Explorer 6.0+ (Windows için)  
* Mozilla Firefox 1.0+/Mozilla 1.7+  
* Apple Safari 1.2+  
* Konqueror  
* Camino  
* Opera 7.54 (AJAX ve şeffaflık kullanan efektler desteklenmiyor)  
* Opera 8 (şeffaflık kullanan efektler desteklenmiyor)  
* Opera 9+

> Bu yazı Kasım 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
