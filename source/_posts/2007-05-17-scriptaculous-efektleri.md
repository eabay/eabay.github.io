---
title: script.aculo.us Efektleri
date: 2007-05-17 11:00:00
categories:
  - AJAX
  - Javascript
---

{% img center /images/posts/scriptaculous_logo.png %}

[Geçen yazımızda]({% post_url 2007-05-17-scriptaculous %}) başladığımız script.aculo.us serüvenine bıraktığımız yerden devam ediyoruz. Bu hafta kütüphanenin efektler bölümünü ele alacağız ve temel efektlerden birer örnek yapmaya çalışacağız.

<!--more-->

script.aculo.us kütüphanesinin efektleri, sürükle-bırak, sıralama, otomatik tamamlama gibi işlerinizi kolaylaştıracak kontrolleri ve DOM öğelerini üretebilen özellikleri barındırdığından bahsetmiştik. Bu ay efekt kullanımına değineceğiz. Geçen ayki yazıya ulaşamayanlar pctech.com.tr adresini ziyaret edebilirler.

Geçen ay da değindiğimiz bir iki şeyin üzerinden yine geçelim. Efekt kullanımından standart söz dizimi

```javascript
new Effect.EffektAdi(element_id, gerekli-parametreler [, secenekler]);
```

şeklindedir. Her efekt için gerekli parametre olmayabilir. İleride efektlere tek tek değinirken kullanılıp kullanılmadığına da yer vereceğiz. Seçenekler de genel veya sadece efekte bağlı olabilir.

Seçenekler bölümünde tüm efektler için ortak parametreler şu şekildedir:

| İsim       | Açıklama   |
|------------|------------|
| duration   | Efektin saniye cinsinden uygulanma süresi (Varsayılan: 1.0) |
| fps        | Efekti bir film gibi düşünün. İşte bu ayar efektin saniye başına kaç kare olacağını belirler. Varsayılan `25`. En fazla `100` olabilir. *25'in üstünü zaten insan gözü algılamaz ;)* |
| transition | Geçişin nasıl olacağınız belirler. Kullanılabilecek değerler: `Effect.Transitions.sinoidal` (varsayılan), `Effect.Transitions.linear`, `Effect.Transitions.reverse`, `Effect.Transitions.wobble` ve `Effect.Transitions.flicker`. |
| from       | Geçişin (transition) başlangıç noktasını belirler. 0.0 ve 1.0 arasında bir değer olabilir (Varsayılan: 0.0). |
| to         | Geçişin bitiş noktasını belirler. 0.0 ve 1.0 arasında bir değer olabilir (Varsayılan: 0.0). |  
| sync       | Efektin kareleri otomatik olarak gösterip göstermeyeceğini belirler. `True` değeri verildiğinde efektin `render()` metodu çağırılarak kareler kontrol edilebilir. `Paralel` efektinde kullanılır. |
| queue      | Efektin hangi sırada olacağını belirler. Kullanımına daha sonra değineceğiz. |
| direction  | Geçişin yönünü belirler. `top-left`, `top-right`, `bottom-left`, `bottom-right` veya `center` (varsayılan) değerlerini alabilir ve sadece `Grow` ve `Shrink` efektlerinde kullanılabilir.

Bunlar dışında seçenekler içerisine parametre olarak kendi fonksiyonlarınızı da dahil edebilirsiniz. Böylece efekt çalıştırılmaya devam ederken belirtilen olaylara bağlı olarak sizin fonksiyonunuz da çalıştırılır. Efekt nesnesi fonksiyonunuza parametre olarak geçirilir. Bu sayede efekt nesnesine de erişerek kendi fonksiyonunuzda kullanabilirsiniz. Kullanabileceğiniz olaylar şunlardır:

| İsim         | Açıklama     |
|--------------|--------------|
| beforeStart  | Belirtilen fonksiyon efekt gösteriminin döngüsü başlamadan önce çağırılır. |
| beforeUpdate | Gösterim döngüsünün her bir tekrarında, değişim gerçekleşmeden önce çağırılır. |
| afterUpdate  | Gösterim döngüsünün her bir tekrarında, değişim gerçekleştekten sonra çağırılır. |
| afterFinish  | Efekt gösteriminin döngüsü bittikten sonra çağırılır. |

Kuru kuru bunların ne anlama geldiğini kavramada sorun olabilir o yüzden örneklere geçmeden bir kod örneği verelim.

```javascript
function baslamadanOnce(sayfaOgesi) {
    alert('Efektin uygulandığı sayfa elemanının id değeri: ' + sayfaOgesi.element.id)
}

function bittiktenSonra(sayfaOgesi) {
    alert('Efektin uygulandığı sayfa elemanı: ' + sayfaOgesi.element)
}

new Effect.Highlight(oge, {
    startcolor: '#ffffff',
    endcolor: '#ffffcc',
    duration: 0.5,
    beforeStart: baslamadanOnce,
    afterFinish: bittiktenSonra
});
```

Fonksiyonunuza parametre olarak geçirdiğiniz efekt nesnesinin erişebileceğiniz tüm özellikleri de şu şekilde:

| İsim                | Açıklama            |
|---------------------|---------------------|
| effect.element      | Efektin uygulandığı sayfa öğesi. |
| effect.options      | Efekte ait seçenekler. |
| effect.currentFrame | Gösterilen son karenin numarası. |
| effect.startOn      | Efektin başlatıldığı zamanın milisaniye cinsinden değeri. |
| effect.finishOn     | Efektin bitirildiği zamanın milisaniye cinsinden değeri. |
| effect.effects[]    | `Parallel` efektinde her bir alt efektin tutulduğu bir `effects[]` dizisi bulunur. Her bir alt efekte bu dizi içerisinden erişilebilir. |

## Efektler  
script.aculo.us kütüphanesi 5 esas efekte sahiptir. Bir de bunların üzerine kurulu çeşitli birleşim efektleri vardır. Bu sayımızda temel efektleri ele alacağız.

### Effect.Opacity  
Sayfa öğesinin saydamlığını değiştirir.

```javascript Genel söz dizimi
new Effekt.Opacity('element_id' [, secenekler]);
new Effekt.Opacity(element [, secenekler]);
```

```html Örnek
<div onclick="new Effekt.Opacity(this, {duration: 2.0, from: 1.0, to: 0.0});">
    Dikkat! Tıklarsanız kaybolur
</div>
```

Öğeye tıklandığında 2 saniye içerisinde (`duration: 2.0`) saydamlık %100'den (`from: 1.0`) %0'a (`to:0.0`) düşecek, yani kaybolacak.


### Effect.Scale  
Sayfa öğesinin boyutlarını değiştirir. En ve boy &#8216;em&#8217; birimine göre değiştirilir.

```javascript Genel söz dizimi
new Effekt.Scale('element_id', yüzde [, secenekler]);
new Effekt.Scale(element, yüzde [, secenekler]);
```

#### Efekte özel seçenekler
| İsim            | Varsayılan | Açıklama     |
|-----------------|------------|--------------|
| scaleX          | true       | Yatay olarak boyutlandırma |
| scaleY          | true       | Dikey olarak boyutlandırma |
| scaleContent    | true       | İçeriğin de boyutlandırılması |
| scaleFromCenter | false      | Öğenin merkez koordinatlarının sabitlenmesi |
| scaleMode       | box        | Öğenin görülebilen bölgesinin boyutlandırılmasını sağlayan `box`, öğenin tamamının boyutlandırılmasını sağlayan `contents` değerlerini alabilir. `originalHeight` ve `originalWidth` değişkenleri kullanılarak uygulanacak boyutun tam değerleri de verilebilir, `{originalHeight: 400, originalWidth: 200}` |
| scaleFrom       | 100.0      | Boyutlandırmanın başlangıç yüzdesi |

```html Örnek
<div>
    <a href="javascript:void()" onclick="new Effekt.Scale(this.parentNode, 120);">
    Biraz daha büyük olsun
    </a>
</div>
```

Bağlantıya tıklandığında yazı %120 oranında büyütülecek.

### Effect.MoveBy  
Öğe x ve y piksel kadar yer değiştirir.

```javascript Genel söz dizimi
new Effekt.MoveBy('element_id', y, x [, secenekler]);
new Effekt.MoveBy(element, y, x [, secenekler]);
```

```html Örnek
<div>
    <a href="javascript:void()" onclick="new Effekt.MoveBy(this.parentNode, -5, 20);">
    Biraz yukarı, biraz da sağa doğru
    </a>
</div>
```

Bağlantıya tıklandığında yazı 5 piksel yukarı, 20 piksel de sağa kayacak. Bu arada ekranın sol üst köşesinin (0,0) noktası olduğunu hatırlatalım.

## Effect.Highlight  
Öğenin arka plan rengini değiştirir, vurgu yapar.

```javascript Genel söz dizimi
new Effekt.Highlight('element_id' [, secenekler]);
new Effekt.Highlight(element [, secenekler]);
```

#### Efekte özel seçenekler
| İsim         | Varsayılan       | Açıklama     |
|--------------|------------------|--------------|
| startcolor   | #ffff99          | Efekt başlangıcındaki arka plan rengi |
| endcolor     | #ffffff          | Efekt bitişindeki arka plan rengi |
| restorecolor | background-color | Efekt bittikten sonraki arka plan rengi. `rgb(0, 255, 0)` şeklinde belirtilmeli. |

```html Örnek
<div onclick="new Effekt.Highlight(this, {startcolor: '#ff99ff', endcolor: '#999999'});">
    Pembeden griye...
</div>
````

Öğeye tıklandığında arka plan rengi pembeden griye dönüşecek.

### Effect.Parallel  
Birden fazla efektin aynı anda uygulanabilmesini sağlar.

```javascript Genel söz dizimi
new Effekt.Parallel([alt efektler] [, secenekler]);
```

```javascript Örnek
new Effect.Parallel([
    new Effect.MoveBy(öğe, 100, 0, {sync: true}),
    new Effect.Opacity(öğe, {from: 1.0, to: 0.0, sync: true})
], {
    duration: 0.5,
    afterFinish: function(effect) {
        Element.hide(effect.effects[0].element.parentNode)
    }
});
```

`MoveBy` ve `Opacity` efektleri aynı öğeye uygulanıyor ve efekt bittiğinde öğe gizleniyor.

> Bu yazı Aralık 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
