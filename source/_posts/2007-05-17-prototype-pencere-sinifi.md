---
title: Prototype pencere sınıfı
date: 2007-05-17 09:00:00
categories:
  - AJAX
  - Javascript
---
{% img right /images/posts/proto.png %}

Prototype aşağı, prototype yukarı! Aslında tüm özelliklerini örneklendiremesek bile öğrenmek isteyenlere önayak olduğumuzu düşünüyoruz. Bu aydan itibaren yine prototype için mevcut eklentiler ile kütüphanenin nasıl daha kullanışlı hale getirilebileceğini görelim.

<!--more-->

Yazımıza Prototype çatısı ile devam ettiğimizden beri bunun temel bir kütüphane olduğuna ve bazı çatıların da temelini oluşturduğuna değinmiştik. Javascript ile kod yazmayı daha pratik hale getiren temelin üzerine kurulmuş bu eklentilerden biri olan pencere sınıfı ile sayfalarınızda ziyaretçilerinizin gözüne hoş gelebilecek, tabir-i caizse, sözde pencereler oluşturmak gerçekten çok kolay. Üstelik bu pencereler açılır pencere engelleyiciler tarafından da engellenmiyor ;)

## Pencere sınıfını nasıl kullanabiliriz?  
Öncelikle http://prototype-window.xilinus.com/download.html adresinden en son sürümü (şu anki sürüm 0.96.2) indirmekle başlayabiliriz. Arşiv dosyasını açtığınızda birçok dosya göreceksiniz. Bizim ilgilendiklerimiz ise `javascripts` klasöründeki `window.js`, `effects.js` ve tabii ki `prototype.js`. Bunlar dışında da pencerelerin biçimlendirilmesinde kullanılan `themes` klasörüne ihtiyacımız olacak.

Daha sonra ki işlemimiz de sayfamızın `head` etiketi içerisine javascript ve css dosyalarını aşağıdaki gibi eklemek.

CSS dosyalarının tümünü eklemek zorunda değiliz. `default.css`, dışında sadece kullanacaklarınızı ekleyip diğerlerini göz ardı edebilirsiniz.

> Örnekler içerisinde göreceğiniz uyarı ve onay pencereleri için `alert.css` dosyası da eklenmelidir.

Şimdi ilk pencere örneğimize geçebiliriz.

```html
200x150 boyutlarında sade bir <a href="javascript:pencereGoster1()">pencere aç</a>.

<script type="text/javascript">
    function pencereGoster1()
    {
        pencere1 = new Window('pencere1', {
            className: "darkX",
            title: "Örnek 1",
            width:200,
            height:150
        });
        pencere1.getContent().innerHTML = "İlk örneğimiz";
        pencere1.setDestroyOnClose();
        pencere1.showCenter(); 
    }
</script>
```

Örnekte öncelikle `Window` adlı nesneden `pencere1` adıyla kendimize de bir tane kopyaladık ve özelliklerini de parantez içindeki kısımda belirledik. Buradaki değerler içerisinde `pencere1`, pencere oluşturulurken kullanılan katmanın `id` özelliği olacak. Böylece müdahale etmek istediğimizde `getElementById` ile bu sayfa öğesine erişim gerçekleştirilebilir. `className` için de yukarıda eklediğimiz CSS dosyalarının isimlerini dosya türü olmadan (yani .css olmadan) kullanıyoruz. `title` penceremizin başlığı, `width` genişliği, `height` da yüksekliği belirler. `.getContent().innerHTML` ile pencere içeriğini oluşturduktan sonra `.setDestroyOnClose()` ile pencereyi kapattığımızda kopyaladığımız nesnenin ortadan kaldırılmasını sağlıyoruz. Eğer bunu yapmazsak pencere sayfada görüntülenmese dahi bellekten silinmediyse tekrar açılmasını istediğimizde aşağıdaki hatayı alacağız. İçerikte HTML kodlarını da kullanabilirsiniz.


{% img center data:image/png;base64,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 %}


En son satırdaki `.showCenter()`la da penceremizi sayfada ortalıyoruz. Tüm bu işlemleri `pencereGoster1()` adlı fonksiyonumuzun içerisine yerleştirdiğimiz için tıklandığında açılması için bir bağlantı içerisinde çağırıyoruz. İşte örneğimiz!

{% img center data:image/png;base64,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 %}

## Pencerede farklı bir adresi görüntüleme

```javascript
pencere2 = new Window('pencere2', {
    className: "mac_os_x",
    url: "http://pctech.com.tr/",
    title: "Örnek 2",
    width:800,
    height:600
});
pencere2.setDestroyOnClose();
pencere2.showCenter();
```

Eğer pencere özelliklerinde `url` ile bir adres tanımlarsak pencere içerisinde bu adres görüntülenecektir. Bu durumda `.getContent().innerHTML`i kullanmamıza gerek kalmıyor.

## Uyarı
```javascript
Dialog.alert("Aşağıdaki buton ile bu uyarı penceresini kapatabilirsiniz.", {
    windowParameters: {
        width:300,
        height:100
    },
    okLabel: "Kapat"
});
```

Uyarı pencereleri için `Dialog.alert()`i kullanacağız. Parantez içerisinde yapacağımız ile tanımlama pencere içeriğini, `windowsParameters` kısmı `Window` nesnesindeki tüm özellik tanımlamalarını yapmamızı sağlıyor. `okLabel` da pencereyi kapatmamızı sağlayan butonun değerini belirliyor. `Dialog` modülünün özelliği, pencerenin diğer tüm sayfanın üzerine bir katman olarak gelip sayfadaki bağlantı, buton gibi kullanıcı etkileşimli öğeleri etkinsizleştirmesidir.

{% img center data:image/png;base64,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" %}

## İçerik olarak sayfadan bir bölümü kullanma

```html
<script type="text/javascript">
    function pencereGoster4()
    {
        pencere4 = new Window('pencere4', {
            className: "spread",
            resizable: false,
            hideEffect:Element.hide,
            showEffect:Element.show,
            minWidth: 10,
            maxWidth: 300
        });
        pencere4.setContent('pencere_icerigi', true, true);
        pencere4.toFront();
        pencere4.setDestroyOnClose();
        pencere4.show();
    }
</script>
<div id="pencere_icerigi" style="float:right">4. örnekteki pencere içeriğini bu bölüm oluşturuyor.</div>
```

En alttaki `pencere_icerigi` `id` özelliğine sahip alanı fark etmiş olmalısınız. Şimdi bu alanı penceremizin içeriği olarak görüntüleyeceğiz. Bunun için `.setContent()` özelliğini kullanıyoruz. `.setContent()` içerisinde öncelikle sayfa elemanının `id`sini tanımlayıp daha sonra da boyut ve yerleşim özelliklerini `true` ile otomatik hale getiriyoruz. Ardından `.toFront()` ile de sayfadaki tüm pencerelerden önde görünmesini sağlıyoruz. Kod içerisinde `Windows` nesnesinde kullanılan bazı yeni özelliklerine de yer verdik. Örneğin `resizable: false` ile yeniden boyutlandırılamaz, `minWidth: 10&#8242; ile en az 10px genişliğinde, `maxWidth: 300&#8242; ile de en fazla 300px genişliğinde bir pencere tanımlaması yapmış oluyoruz. Değişiklikleri pencere büyültme ve küçültme butonlarını kullanarak görebilirsiniz.

## Onay penceresi

```javascript
Dilog.confirm("Değişiklikleri onaylıyor musunuz?", {
    id: "onayPenceresi",
    okLabel: "Evet", 
    cancelLabel: "Hayır", 
    windowParameters: {
        width:300
    },
    ok: function(pencere) {alert("Onaylandı"); return true;},
    cancel: function(pencere) {alert("İptal edildi")}
});
```

`Dialog` için `confirm` özelliğini kullanarak şimdi de bir onay penceresi oluşturacağız. `alert özelliğinden farkı onaylama dışında iptal etme için de bir seçeneğimizin olması. Seçime bağlı olarak da istediğimiz fonksiyonu çağırarak uygun işlemin yapılmasını sağlayabiliriz. `(ok|cancel)Label` özellikleri ile onay ve iptal butonlarımızın değerlerini belirlerken tıklanan butona göre `ok|cancel` iş bitirici fonksiyonumuzu devreye sokuyor.

## İletişim penceresi

```javascript
var zamanAsimi;
function iletisimKutusuAc() {
    Dialog.info("Bu pencere 5 saniye içerisinde kapanacak", {windowParameters: {width:250, height:100}, showProgress: true});
    zamanAsimi = 5;
    setTimeout(zamanBilgisi, 1000)
}

function zamanBilgisi() {
    zamanAsimi--;
    if (zamanAsimi >0) {
        Dialog.setInfoMessage("Bu pencere " + zamanAsimi + " saniye içerisinde kapanacak")
        setTimeout(zamanBilgisi, 1000)
 }
 else
    Dialog.closeInfo()
}
iletisimKutusuAc();
```

Yine bir `Dialog` fakat bu kez `info`. 5'ten geri sayarak açılan pencereyi otomatik kapatan, bunun dışında farklı bir kapatma seçeneği olmayan bir pencere. Elimizde `iletisimKutusuAc()` ve `zamanBilgisi()` olarak 2 fonksiyon bulunuyor. Birinci fonksiyon iletişim kutusunu oluşturuyor; diğeri ise geri sayım ve pencere içeriğinde buna bağlı güncellemeyi gerçekleştiriyor.  
Pencere özellikleri içerisinde `showProgress: true` dikkatinizi çekmiş olabilir. Bu, pencere içerisinde bir `işlem yapılıyor` anlamına gelen resmin görüntülenmesini sağlıyor. `setTimeout(zamanBilgisi, 1000)` satırları ile `zamanBilgisi()` fonksiyonu 1'er saniyelik gecikmelerle çağırılarak çalıştırılıyor.

`zamanBilgisi()` fonksiyonuna bakarsanız da öncelikle başlangıçta `5` olarak belirlenen süre 1 saniye azaltılıyor. Daha sonra da saniyenin 0 olmaması koşulu ile pencere içeriği `.setInfoMessage()` ile güncelleniyor. 0 olduğu takdirde de `.closeInfo()` ile kapatılıyor.

## AJAX iş başında!

```javascript
pencere7 = new Window('pencere7', {
    className: "alphacube",
    title: "Örnek 7",
    width:300,
    height:100
});
pencere7.setAjaxContent("ajax_cevap.php", {
    method: 'get',
    parameters: 'kullaniciAdi=erhan&sifre=yok&eposta=eposta@adres.com'
}, true, false)
pencere7.setDestroyOnClose();
```

```php ajax_cevap.php
<?php
	echo("Kullanıcı adı: ".$_GET["kullaniciAdi"]."<br />");
	echo("Şifre: ".$_GET["sifre"]."<br />");
	echo("E-posta: ".$_GET["eposta"]."<br />");
?>
```

Penceremizin içeriğini AJAX ile yapacağımız istek sayesinde belirlememizi sağlayan kodumuz son örnek olarak karşımızda. `.setAjaxContent()` ile gerçekleştirdiğimiz bu işlem aslında geçen haftalarda anlattığımız `Ajax.Request`tin ta kendisi. `ajax_cevap.php` sayfasına `GET` metodu ile gönderdiğimiz veri pencere içerisinde biçimlendirilerek görüntüleniyor.

Bu ay ki örneklerimizi de burada sonlandırdık. Önümüzdeki sayıda yine prototype temelli bir kütüphane olan script.aculo.us ile devam edeceğiz.

## Efektler  
Kullandığımız sınıf, pencerelerin açılıp kapanması sırasında efektler kullanabilmemize olarak sağlıyor. Prototype temelli bir kütüphane olan script.aculo.us içerisindeki efektlerin dahil edildiği sınıfta pencere özelliklerinde showEffect ve hideEffect ile pencerelerin nasıl açılıp nasıl kapanacağını belirleyebilirsiniz. Örneğin,
 
```javascript
showEffect: Effect.Appear
hideEffect: Effect.Fade
```
 
Daha fazla örnek için http://wiki.script.aculo.us/scriptaculous/show/CombinationEffectsDemo adresini kontrol edebilirsiniz.

> Bu yazı Ekim 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
