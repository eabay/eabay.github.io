---
title: Prototype ile form gönderimi
date: 2007-05-16 13:00:00
categories:
  - AJAX
  - Javascript
---

{% img right /images/posts/prototype.png %}

[Geçen ay]({% post_url 2007-05-16-prototype-kullanimi %}) Prototype kütüphanesi hakkında giriş niteliğinde bir yazı ile karşınıza çıkmıştık. Bazı temel özelliklerinden söz ettiğimiz ve küçük örnekler yaptığımız Javascript kütüphanesiyle bu ay bir kullanıcı kayıt formu yapacağız.

<!--more-->

Klasik web uygulamalarında form kullanıcı tarafından doldurulur ve sunucuya gönderilir. Eğer uygulamayı yazan kişi sunucu tarafında gelen verinin doğruluğunu kontrol ediyorsa istenmeyen bilginin düzenlenmesi için sayfa tekrar kullanıcıya iletilir. Bu sunucu-istemci paslaşması istenen bilgi elde edilene kadar sürer. En azından bir kere de olsa girdiğiniz kullanıcı adı kullanıldığı için farklı bir ad seçmenizi isteyen uyarıyla karşılaşmış, hatta bu yüzden doğru da olsa güvenlik nedeniyle tarayıcıya geri gönderilmeyen şifre ve şifre tekrar alanlarını defalarca doldurma durumuyla karşı karşıya gelmiş olmalısınız. Her defasında sunucu ve istemci arasındaki bu paslaşmada veri iletimini ve sinir krizini azaltacak AJAX&#8217;ın kullanımını bir örnek ile göstermeye çalıştık.

Kütüphane olarak kullandığımız Prototype projesinin internet adresi [prototype.conio.net](http://prototype.conio.net). En son sürümünü (şu anda 1.4.0) buradan indirebilirsiniz.

Uygulamamızın senaryosunda kullanıcı kayıt olabilmek için kullanıcı adı, şifre ve e-posta adresi bilgilerini doldurup `Gönder` butonuna tıklamalı. Butona tıklandıktan sonra veriler Ajax nesnesi ile sunucuya gönderiliyor ve hatalar ve başarılı gönderim bilgisi form bölümünün üstünde görüntüleniyor. Bu sırada form sürekli olarak değişmeden kalıyor. Uygulamamızın sadece fikir verici bir niteliği olduğunu tekrar hatırlatalım. Yani aynen alıp sitenizde kullanabileceğiniz bir uygulama değil.

## Formu yapılandıralım  
Senaryomuza uygun şekilde 3 giriş alanı ve bir butona sahip formu oluşturduk. Yazdığımızı görebilmek için şifre girişinde `input` öğesinin `type` özelliği için `password` yerine `text` kullandık. Ayrıca `Gönder` butonumuz da `type` özelliği `submit` yerine `button` değerine sahip. Fark ettiyseniz `form` öğesinin `action` özelliği `formGonder()` fonksiyonumuzu çağırıyor. Bunun nedeni ise `Enter` ile formun gönderilmesini istememize rağmen Opera 9'da bunun çalışması. IE 6 ve Firefox 1.5&#8217;te ise herhangi bir işlevi yok. Form öğesinin üst kısmında içi boş olan ve &#8216;id&#8217; özelliği &#8216;kayitSonucUyari&#8217; olan ve bizim sunucudan gelen mesajları görüntüleyeceğimiz bölüm yer alıyor. `body` öğesinin bitiminden hemen önce gördüğünüz `İşlem yapılıyor` mesajı alanı ise çok sık karşılaştığımız işlemin devam ettiğini gösteren bir uyarı. Sayfayı ilk açtığınızda butona tıklayana kadar bu mesajı göreceksiniz. Bu sorunun varlığından haberdarız ama Prototype örneklerinden almamıza rağmen çözüm üretemediğimizi itiraf etmek zorundayız :D. Ama ilk form gönderiminden sonra normal çalışıyor.

## Javascript fonksiyonlarımızı oluşturalım  
`formGonder()` ve `cevap()` adlı iki adet fonksiyonumuz bulunuyor. İsimlerinde anlaşıldığı üzere biri formun gönderiminden diğeri de dönen cevaptan sorumlu. `formGonder()` fonksiyonunda öncelikle `kayitSonucUyari` değerli `id` özelliğine sahip bölümün herhangi bir içeriğe sahip olsa bile yeni bir gönderim talebinde görüntülenmemesi için CSS sınıfını `uyariGizli` olarak değiştiriyoruz (satır 39). Ardından da bir istek tamamlanmadan diğerinin gönderilmesini engellemek için `Gönder` butonumuzu kullanıma kapatıyoruz (satır 40). Devam eden satırlarda da geçen ay örneklerle açıkladığımız Ajax nesnesini kullanarak `kayit.php` sayfasina talebimizi gönderiyoruz.

`cevap()` fonksiyonu istek-cevap süreci tamamlandıktan sonra çağırılan yordam. İstek başlangıcında görünmez kıldığımız alanı bu kez `uyariKutu` CSS sınıfı ile şekillendirip içini de gelen yanıtla doldurup görüntülenmesini sağlıyoruz. Ardından da gönderim butonunu tekrar etkinleştirip yeni istek taleplerine açıyoruz.

İşlem yapılıyor alanının nasıl kontrol edildiğini, yani `onCreate` olayı ile `Ajax` nesnesinin `Request` metodunun oluşturulmasında görüntülenip `onComplete` ile cevabın geldiğinde ve herhangi bir etkin bağlantının kalmadığından emin olunarak tekrar gizlenmesini 23. ve 35. satırlar arasındaki kod parçasından kontrol edebilirsiniz.

```html kayit.html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
		<title>Kayıt Formu</title>
		
		<style type="text/css">
			.uyariKutu {
				border:1px solid #FF0000;
				color:#000000;
				background-color:#FF3333
			}

			.uyariGizli {
				visibility:hidden
			}
		</style>
		
		<script src="prototype-1.4.0.js"></script>
	
		<script type="text/javascript">

			var islemYapiliyorUyarisi = {
				onCreate: function(){
					Element.show('islemYapiliyor');
				},
		
				onComplete: function() {
					if(Ajax.activeRequestCount == 0){
						Element.hide('islemYapiliyor');
					}
				}
			};
		
			Ajax.Responders.register(islemYapiliyorUyarisi);

			function formGonder()
			{
				$('kayitSonucUyari').className = "uyariGizli";
				$('gonder').disabled = true;
				
				var kullaniciAdiDeger = $F('kullaniciAdi');
				var sifreDeger = $F('sifre');
				var epostaDeger = $F('eposta');

				var url = 'kayit.php';
				var degistirgen = 'kullaniciAdi=' + kullaniciAdiDeger + '&sifre=' + sifreDeger + '&eposta=' + epostaDeger;
				
				var ajaxla = new Ajax.Request(
							url,
							{
								method: 'get',
								parameters: degistirgen,
								onComplete: cevap
							});
			}

			function cevap(istek)
			{
				
				$('kayitSonucUyari').innerHTML = istek.responseText;
				$('kayitSonucUyari').className = 'uyariKutu';
				
				$('gonder').disabled = false;
			}
		</script>

	</head>
	
	<body>
		<div id="kayitSonucUyari"></div>
		<form id="kayit_formu" name="kayit_formu" method="post" action="javascript:formGonder()">
			<fieldset>
				<legend>Kullanıcı Adı</legend>
		
				<input name="kullaniciAdi" type="text" id="kullaniciAdi" size="30" maxlength="10" />
			</fieldset>
			
			<br />
			
			<fieldset>
				<legend>Şifre</legend>
		
				<input name="sifre" type="text" id="sifre" size="30" maxlength="10" />
			</fieldset>
		
			<br />
			
			<fieldset>
				<legend>E-posta</legend>
		
				<input name="eposta" type="text" id="eposta" size="30" maxlength="10" />
			</fieldset>
		
			<br />
			<input name="gonder" type="button" id="gonder" value="Gönder" onclick="formGonder()" />
		</form>
		<div id='islemYapiliyor' align="center"><img src='yukleniyor.gif' align="absmiddle"> İşlem yapılıyor...</div>
	</body>
</html>
```

## PHP ile sunucudan yanıt  
Sunucu tarafından formun işlenmesi ve yanıtın verilmesi sürecini kayit.php sayfası ile gerçekleştirdik. Bu kod çok özentili olmamakla birlikte kesinlikle gerçek anlamda sitelerde kullanılmamalıdır. Gelen veri kontrolleri istenilen verinin türüne ve güvenlik seviyesine göre çok daha özenli ve dikkatli yazılmalı ve defalarca test edilmelidir. Ayrıca klasik bir kayıt işleminde veritabanı ile ilgili de bir dizi işlemin gerçekleştirilmesi gerekiyor. Bizim asıl odaklandığımız Ajax olduğundan bu konuları yüzeysel geçmeyi tercih edeceğiz.

```php kayit.php
<?php
$kullaniciAdi = $_GET["kullaniciAdi"];
$sifre = $_GET["sifre"];
$eposta = $_GET["eposta"];

$hata = "";

if($kullaniciAdi == "pctech") {
    $hata = "<li>Bu kullanıcı adı başka biri tarafından alınmış. Lütfen farklı bir tane deneyin.";
}
elseif($kullaniciAdi == "") {
    $hata = $hata . "<li>Kullanıcı adı boş bırakılamaz";
}


if("pctech" == $sifre) {
    $hata = $hata . "<li>Hatalı şifre";
}
elseif($sifre == "") {
    $hata = $hata . "<li>Şifre boş bırakılamaz";
}


if($eposta == "pctech") {
    $hata =  $hata . "<li>Hatalı eposta adresi";
}
elseif($eposta == "") {
    $hata = $hata . "<li>E-posta boş bırakılamaz";
}


if($hata != "") {
    echo("Aşağıdaki hatalar bulundu:<ul>".$hata."</ul>");
}
else {
    echo("Bilgileriniz bize ulaşmıştır...");
}
```
> Bu yazı Eylül 2006 tarihinde PC Tech dergisinde yayınlanmıştır.
