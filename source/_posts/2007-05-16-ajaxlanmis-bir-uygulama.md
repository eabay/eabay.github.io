---
title: "AJAX'lanmış bir uygulama"
date: 2007-05-16 10:00:00
categories:
  - AJAX
  - Javascript
---
{% img right /images/posts/ajax-logo.jpg %}

[Geçen ay]({% post_url 2007-05-16-bahar-kokulu-web-uygulamalari %}) yaptığımız laf salatasının ardından icraat dönemine geçmiş bulunuyoruz, hepimize hayırlı uğurlu olsun. Bu ay şöyle basitinden bir uygulama ile öğrendiklerimizi pekiştirelim.

<!--more-->

## Adım 1: Sunucuya isteğimizi gönderme
Sunucuya isteğimizi gönderebilmek için istemci tarafında -tarayıcıda- çalışan bir dile ihtiyacımız olduğundan bahsetmiştik. Bunu gerçekleştirebilmek için XMLHTTP olarak bilinen ve Internet Explorer'da ActiveX nesnesi olarak bulunan bir sınıf kullanacağız. 'Peki ya diğer tarayıcılar?' sorusunu merak edenlere de hemen cevap verelim: aynı sınıf XMLHttpRequest adıyla Mozilla, Safari ve Opera'da da kullanılabilmekte. Ve kodumuzun ilk ayrıntılarına geçiyoruz.

```javascript
if (window.XMLHttpRequest) { // Mozilla, Safari, ... 
  http_istegi = new XMLHttpRequest();  
} else if (window.ActiveXObject) { // IE  
  http_istegi = new ActiveXObject('Microsoft.XMLHTTP')  
}
```

Bazı Mozilla tarayıcıları sunucudan dönen bilgi XML üstbilgisini içermiyorsa hata verir. Eğer açık kaynağa saygılı gençlersek biz de Mozilla'ya saygı duyanlardanız demektir ve o yüzden de bu ayrıntıya dikkatlice yaklaşaraktan gerekli düzenlemeyi hemen yapmalıyız. Nesneyi kendi değişkenimize kopyaladıktan sonra sayfa üstbilgisini XML olarak değiştirelim.


```javascript
http_istegi = new XMLHttpRequest();  
http_istegi.overrideMimeType('text/xml');
```

Bir sonrai aşama HTTP isteğini oluşturan nesnemize sunucudan gelen cevabı işleyecek JS fonksiyonunu söylemek. Bunu da kullanacağımız fonksiyonun adını nesnenin onreadystatechange özelliğine atayarak yapacağız.

```javascript
http_istegi.onreadystatechange = fonksiyonunAdi;
```

Dikkat etmeniz gereken nokta fonksiyon adından sonra parantez kullanılmadığı ve hiçbir değiştirgen gönderilmediği. Bu söz diziminin yanı sıra işinizi biraz daha kolaylaştırabilecek olanı da şöyle kullanabilirsiniz:

```javascript
http_istegi.onreadystatechange = function() {  
  // işi yapacak kodlar  
};
```

Snucu cevabının nasıl işleneceğini belirledikten sonra şimdi ise sıra gerçekten talepte bulunmada. HTTP isteği sınıfımızın *open()* ve *send()* metodları bu işimizi görecek.

```javascript
http_istegi.open('GET', 'http://www.ornek.org/bir.dosya', true);  
http_istegi.send(null);
```

Gördüğünüz gibi *open()* metodundaki ilk değiştirgen *GET*. Sunucunuz tarafından desteklenen POST, HEAD, TRACE gibi diğer tüm metodlar da kullanılabilir. İkinci değiştirgen ise isteğimizi gönderdiğimiz sayfanın adresi. Güvenlik nedeniyle sadece kendi alan adınızdan sayfaları çağırabilirsiniz. Unutmamanız gereken nokta ise adresi yazarken iletişim kuralını yazmak (`http://`). Üçüncü değiştirgen isteğimizin eşzamanlı olup olmadığını belirliyor. *True* olarak atanan değer AJAX kısaltmasının 'A'sını oluşturuyor. Eşzamanlı olmayan bu taleple sunucudan yanıt beklenirken de JS fonksiyonu çalışmaya devam edecek.

`send()` metodu sunucuya bilgileri göndermemizi sağlıyor. Eğer gönderim türü *GET *yerine *POST *olarak belirlenirse o zaman gönderilen veri sorgu dizisi şeklinde yazılmalı.

> anahtar=deger&digeranahtar=digerdeger

Ayrıca sayfa üstbilgisi de

```javascript
http_istegi.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

şeklinde atanmalı. Aksi takdirde gönderdiğinizi düşündüğünüz veriler aslında gönderilmemiş olacak.

## Adım 2: Sunucudan gelen yanıtı işleme
İsteğimizi sunucuya sağ salim gönderdikten sonra sıra gelen veriyi düzgün bir biçimde ele almak. onreadystatechange özelliğine atadığımız fonksiyon içeriğini kabaca şöyle yazabiliriz:

```javascript
if (http_istegi.readyState == 4) {  
  // yanıt alındı, herşey yolunda  
} else {  
  // henüz hazır değil  
}
```

Öncelikle isteğimizin durumunu gözden geçirelim. Eğer durum değeri 4 ise bu sunucudan yanıt dönüşünün tamamlandığı anlamına geldiğinden işimize devam edebiliriz demektir. Diğer durum değerleri de aşağıdaki gibi:

* 0 (başlatılmadı)
* 1 (yükleniyor)
* 2 (yüklendi)
* 3 (etkileşimli)
* 4 (tamamlandı)

Sıradaki kontrol ise HTTP sunucu yanıtının durum kodu. Sağlıklı bir yanıtta â€“ki bu bir internet sayfasını da görüntülediğinizde gönderilen- kod 200'dür.

```javascript
if (http_istegi.status == 200) {  
  // mükemmel!  
} else {  
  // istekle ilgili bir sorun var,  
  // örneğin yanıt 404 (Sayfa bulunamadı)  
  // ya da 500 (Sunucu hatası) kodlarına sahip olabilir  
}
```

İsteği gönderdik, yanıtı aldık ve her şey yolundaysa veri elimize ulaştı. Şimdi elimizdeki veriye erişim için elimizde 2 seçenek var.

* `http_istegi.responseText` sunucu yanıtını metin dizisi olarak döndürür.
* `http_istegi.responseXML` yanıtı XML biçiminde döndürerek DOM fonksiyonları ile işlenebilmesine olanak sağlar.

## Adım 3: Örnek uygulama  
Şu ana kadarki tüm kodları bir araya getirerek örneğimizi oluşturalım. Aşağıdaki kodlar test.html adlı sayfanın içeriğini ekrana getirecek.

```html http_icerigi.html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
   "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <script type="text/javascript" language="javascript">

            var http_istegi = false;

            function istekYap(url) {

                http_istegi = false;

                if (window.XMLHttpRequest) { // Mozilla, Safari,...
                    http_istegi = new XMLHttpRequest();
                    if (http_istegi.overrideMimeType) {
                        http_istegi.overrideMimeType('text/xml');
                    }
                } else if (window.ActiveXObject) { // IE
                    try {
                        http_istegi = new ActiveXObject("Msxml2.XMLHTTP");
                    } catch (e) {
                        try {
                        http_istegi = new ActiveXObject("Microsoft.XMLHTTP");
                        } catch (e) {}
                    }
                }

                if (!http_istegi) {
                    alert('XMLHTTP nesnesi kopyalanamadı');
                    return false;
                }
                http_istegi.onreadystatechange = icerigiGoster;
                http_istegi.open('GET', url, true);
                http_istegi.send(null);

            }

            function icerigiGoster() {

                if (http_istegi.readyState == 4) {
                    if (http_istegi.status == 200) {
                        alert(http_istegi.responseText);
                    } else {
                        alert('İstekle ilgili bir sorun var.');
                    }
                }

            }
        </script>
    </head>
    <body>
        <span
            style="cursor: pointer; text-decoration: underline"
            onclick="istekYap('test.txt')">
                İstek yap
        </span>
    </body>
</html>
```

```text test.txt
test içeriği...
```

Örnekte ziyaretçi `İstek yap` bağlantısına tıklayarak test.html değiştirgenine sahip `istekYap()` fonksiyonunu tetikler. Ardından istek `alertContents()` fonksiyonuna gönderilir. Bu fonksiyon da yanıtı kontrol eder ve sorunsuz bir yanıtta test.html içeriğini `alert()` fonksiyonuna aktarır. Ve böylece işlem tamamlanmış içerik ekranda görüntülenmiş olur.

> Bu yazı Haziran 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
