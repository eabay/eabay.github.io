---
title: Prototype kullanımı
date: 2007-05-16 12:00:00
categories:
  - AJAX
  - Javascript
---

{% img right /images/posts/prototype.png %}

[Geçen yazımızda]({% post_url 2007-05-16-60lik-mi-70lik-mi %}) AJAX kütüphanesi olarak büyük ihtimal dojo kullanacağımızı söylemiştik. Ama küçük ihtimallerden birini seçerek devam etmeyi daha uygun gördük. Prototype adlı kütüphaneden biraz bahsetmiştik. Bakalım fikrimiz neden değişmiş?

<!--more-->

Prototype kütüphanesi aslen AJAX'a hizmet etmek anlayışı ile oluşturulmamış. Onu bir javascript kütüphanesi olarak adlandırmak çok daha doğru olur. Çünkü AJAX fonksiyonları onun sadece bir kısmını oluşturuyor. Yanlış anlaşılmasın, AJAX için öyle çok da fonksiyonu yok. Ama bazı çatıların (open rico, script.aculo.us) temelini oluşturduğu ve işin genel işleyişini pekiştirmemiz için diğerlerinden çok daha iyi bir başlangıç noktası. Bazı okurlarımızın geri dönüşleri de bu kararı vermemizdeki etkenlerden bir tanesi. Şimdi hem biraz prorotype kütüphanesinden bahsedelim hem de küçük bir örnekle devam edelim. Bu arada projenin internet adresi prototype.conio.net. En son sürümünü (şu anda 1.4.0) buradan indirebilirsiniz.

## Bazı faydalı fonksiyonlar  
Kodlama ile uğraştığımızda sürekli olarak tekrarlanan kısımlar yazılımcıyı sıkar. Prototype içerisinde bu rahatsızlığı çözen birkaç ön tanımlı fonksiyon bulunuyor.

### $()
`document.getElementById()` fonksiyonu için bir kısa yol diyebiliriz. Sayfa içerisinde `id` özelliği eşleşen elemanı döndürür. Birden fazla `id` verilerek eşleşen elemanlara ait bir dizi oluşturulabilir.

```html
<script>
    function ilkBolum() {
        var bolum = $('bolum1');
        alert(bolum.innerHTML);
    }

    function butunBolumler() {
        var bolumler = $('bolum1','bolum2');
        for(i=0; i<bolumler.length; i++) {
            alert(bolumler[i].innerHTML);
        }
    }
</script>

<div id="bolum1">1. bölüm</div>
<div id="bolum2">2. bölüm</div>

<input type="button" value="1. bölümde ne var?" onClick="ilkBolum();"><br />
<input type="button" value="Tüm bölümlerde ne var?" onClick="butunBolumler();">
```

Kod içerisinde ne yapıldığının üzerinden kısaca geçelim. `ilkBolum()` fonksiyonu sayfada `id` özelliği `bolum1` olan elemanı alıyor özelliğini ekrana uyarı olarak bastırıyor. `butunBölümler()` fonksiyonu `id` özellikleri `bolum1` ve `bolum2` olan elemanlardan bir dizi oluşturuyor ve bunları bir döngü içerisinde kullanarak aynı işi yapıyor. Bu fonksiyonların kullanımını tetikleyen de sayfadaki butonların tıklanması.

### $A()  
`$A()` fonksiyonu gönderilen değeri diziye çevirir. Sahip olduğu çeşitli metodlar sayesinde dizi işlemlerinde işinizi kolaylaştırır. Sayfadaki elemanları dizi nesnelerine çevirip daha kolay işlemenizi sağlar.

```html
<script>
    function secenekleriGoster(){
        var liste = $('ajaxCatilari').getElementsByTagName('option');
        var secenekler = $A(liste);
    
        secenekler.each(function(secenek){
            alert(secenek.nodeName + ': ' + secenek.innerHTML);
        });
    }
</script>

<select id="ajaxCatilari" size="3">
    <option value="5">Prototype</option>
    <option value="8">dojo</option>
    <option value="1">Backbase</option>
</select>

<input type="button" value="Seçenekleri Göster" onclick="secenekleriGoster();" > 
```

### $F()  
Bu fonksiyon da bir önceki gibi kısa yol niteliğinde. &#8216;id&#8217; özelliği eşleşen form elemanının değerini döndürür.

```html
<script>
    function degerGoster() {
        alert($F('bilgiGirisi'));
    }
</script>

<input type="text" id="bilgiGirisi" value="Prototype işi biliyor..."><br />
<input type="button" value="Yukarıda ne yazıyor?" onclick="degerGoster();">
```

### $H()  
Nesneleri dizilere benzeyen sayılabilir kargaşa (hash) nesnelerine dönüştürür. Cümle biraz anlaşılmaz duruyor ama örneğe baktığınızda anlaşılır olacaktır.

```html
<script>
    function kargasaCikar() {
        var nesne = {
            anahtar1: "deger1",
            anahtar2: "deger2",
        };

        var kargasa = $H(nesne);
        alert(kargasa.toQueryString());
    }

</script>

<input type="button" value="Kargaşa Çıkar" onclick="kargasaCikar();">
```

### $R()  
`new ObjectRange(altSınır, üstSınır, sınırlarHariç)` tarzı yazımın kısaltılmış hali diyebiliriz. Örnekteki kullanımda `each()` metodu yine prototype kütüphanesindeki sayılabilir nesnesinden bir metottur.

```html
<sript>
    function say(){
        var aralik = $R(10, 20, false);
        aralik.each(function(deger, index){
            alert(deger);
        });
    }

</script>

<input type="button" value="10'dan 20'ye kadar say" onclick="say();" >
```

### Try.these()  
Denediğiniz fonksiyonlardan biri çalışana kadar sırayla tümünü dener ve çalışan fonksiyonun değerini döndürür. Örneğin tarayıcılar arasındaki farklılık durumlarında veya farklı js sürümlerinde kullanışlı olabilir.

```html
<script>
    function hangiTarayici(){
        if (window.XMLHttpRequest) { // Mozilla, Safari, ...
            tarayici1 = "Mozilla, Safari";
        } else if (window.ActiveXObject) { // IE
            tarayici2 = "IE";
        }
        
        alert(Try.these(
            function() {return tarayici1;},
            function() {return tarayici2;}
        ));
    }
</script>

<input type="button" value="Hangi tarayıcıyı kullanıyorum" onclick="hangiTarayici();" >
```

## AJAX nesnesi  
Prototype kütüphanesinin buraya kadarki kısmı sadece işimizi kolaylaştırabilecek bazı fonksiyonlardan ibaretti. Halbuki bizim ilgi alanımız AJAX. O zaman kütüphanenin AJAX nesnesini mercek altına alabiliriz.

Prototype içerisinde AJAX mantığını işletebileceğiniz aynı isimli nesneye ait bir kısım sınıflar yer alıyor. Bunların nasıl kullanıldığına bir bakalım.

### Ajax.Request  
`Request` sınıfı `XMLHttpRequest` nesnesini oluşturma ve bağlantının başarılı olup olmadığını kontrol edip gelen cevabı işleme sürecini tarayıcı bağımsız olarak kontrol edebilmenizi sağlıyor.

Örneğin bir sayfa tasarlıyorsunuz ve sayfada yer alan bir seçim listesinde yapılan değişiklik sonucu farklı bir form elemanını güncellemek istiyorsunuz. Güncelleme için de dinamik bir sayfadan gelen cevabı kullanacaksınız. Şimdi bu senaryoyu uygulayacağımız örneği hayata geçirelim ve ardından konuya devam edelim.

```html
<script>
    function ajaxCatiAdresi() {
        var ajaxCati = $F('AJAXCati');
        var url = 'ajax_cevap.php';
        var degistirgenler = 'AJAXCati=' + ajaxCati;
        
        var ajaxla = new Ajax.Request(
                url,
                {
                    method: 'get',
                    parameters: degistirgenler,
                    onComplete: cevapGoster
                });

    }

    function cevapGoster(istek)
    {
        //put returned XML in the textarea
        $('sonuc').value = istek.responseText;
    }
</script>

<select name="AJAXCati" size="3" id="AJAXCati" onchange="ajaxCatiAdresi()">
  <option value="Prototype">Prototype</option>
  <option value="dojo">dojo</option>
  <option value="Backbase">Backbase</option>
</select>

<input name="sonuc" type="text" id="sonuc" value="" size="60" />
```

İstek gönderdiğimiz dinamik sayfa için PHP ile yazdığımız aşağıdaki kodları kullandık. Hangi dilin kullanıldığı vs. gibi şeyler şu anda konumuz dışı ve bunlar sadece birer örnek niteliğinde.

```php ajax_cevap.php
switch ($_GET["AJAXCati"]) {
    case "Prototype":
       echo "http://prototype.conio.net/";
       break;
    case "dojo":
       echo "http://dojotoolkit.org/";
       break;
    case "Backbase":
       echo "http://www.backbase.com/";
       break;
    default:
       echo "Lütfen listeden bir seçim yapın";
}
```

Gördüğünüz gibi listeden yapılan AJAX çatısı seçimi bize alttaki alanda adresini görüntülemekte. Bunun için öncelikli olarak `$F('AJAXCati')` ile seçimin değerini aldık. Daha sonra isteğimizi göndereceğimiz adresi tanımladık. Ardından göndereceğimiz değiştirgeni (Birden fazla olabilir. Bu durumda `&#8220;+ &#8216;&degistirgen2=&#8217; + deger2&#8243;` şeklinde devam edecektik.) belirledik. `Ajax.Request` nesnemizden bir tane ajaxla değişkenine kopyaladık ve gerekli değiştirgenleri de aynı anda tanımladık. Talebi dinamik sayfaya iletmek için `GET` metodunu kullandık. Cevabın döndüğünden emin olmamızı sağlayan `onComplete` değiştirgeni için de `cevapGoster()` fonksiyonunu çağırılacak fonksiyon olarak belirledik. Bu fonksiyon içerisinde de gelen cevabı `id` özelliği `sonuc` olan kutunun değeri yapan satırı yazdık.

`Request` nesnesi içerisinde tanımlanabilecek bir iki özellik daha bulunuyor. Örneğin işlemin eş zamanlı olup olmayacağının belirlendiği `asynchronous` gibi (Değer olarak `true` veya `false` alabilir. Varsayılan değer `true`).

> Bu yazı Ağustos 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
