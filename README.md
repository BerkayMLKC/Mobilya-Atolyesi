# Mobilya Atölyesi 🪚

Küçük bir mobilya atölyesini yöneten, ihalelere teklif veren, sipariş üreten ve kâr ya da zarar eden bir simülasyon oyunu. Telefonda ve tarayıcıda çalışır, Android uygulamasına dönüştürülebilir (Capacitor).

**Oyna:** https://BerkayMLKC.github.io/Mobilya-Atolyesi/

## Oyun

Kasa 12.000 ₺ ile başlar. Amacın kasayı hedefe çıkarmak (varsayılan **150.000 ₺**, Rapor sekmesinden 20.000 ₺ ile 5.000.000 ₺ arasında kendin belirlersin), kasa **-3.000 ₺**'nin altına inerse iflas edersin.

- **İhaleler:** Her 3 günde 4 yeni ihale gelir. Müşterinin bütçe sınırını aşmadan fiyat teklif edersin. Üç rakip de teklif verir. Fiyatı düşük olan kazanır, yüksek itibarın teklifini avantajlı yapar.
- **Maliyet:** Malzeme parası ihaleyi kazandığın anda peşin ödenir. Kereste fiyatı gün gün dalgalanır.
- **Üretim:** Ustalar günlük iş günü üretir, siparişler en yakın teslim tarihine göre sıralanır.
- **Teslimat:** Zamanında teslim edersen para ve +2 itibar, geç teslimde günlük %5 ceza (en çok %50) ve -3 itibar alırsın. Teslim tarihinden 5 gün sonra sipariş iptal olur, %20 ceza kesilir.
- **Giderler:** Her gün usta maaşları (250 ₺ / usta) ve kira (150 ₺).
- **Atölye:** Usta işe al, makine al (+%25 hız), reklam ver (+5 itibar). İtibar yükseldikçe daha büyük ihaleler gelir.
- **Olaylar:** Ustalardan biri hastalanabilir (üretim düşer, 400 ₺ ile doktora götürebilirsin), makine bozulabilir (hız bonusu gider, 800 ₺ ile tamir ettirirsin).
- **Teslimat kutlaması:** İş bitince konfeti, yıldız (zamanında 3, gecikmeli 1-2) ve kazanç ekranı çıkar. Üst üste zamanında teslim **seri bonusu** verir (en çok +%15).
- **Profil:** Adını yaz, avatarını özelleştir (ten, saç, gömlek, zemin, saç stili, gözlük) ya da galeriden fotoğraf seç. Fotoğraf yalnızca cihazında saklanır.
- **Ses efektleri:** Tarayıcıda sentezlenir (ses dosyası yok), sağ üstteki düğmeyle kapatılır.
- **Kasa desteği (uygulama içi satın alma):** İflas edince oyuncu yeni oyuna başlayabilir (ücretsiz) ya da kaldığı yerden devam etmek için bir destek paketi alabilir (+8.000 / +20.000 / +60.000 ₺). Kasa 2.000 ₺'nin altındayken Atölye sekmesinde de görünür. Satın alınan para **hedefe sayılmaz**, yani zafer paraya değil beceriye bağlı kalır.
- Oyun tarayıcıda otomatik kaydedilir.

Strateji: çok düşük fiyat zarar ettirir, çok yüksek fiyat ihaleyi kaybettirir ve maaşlar yine de her gün çıkar.

## Dosya yapısı

```
assets/                   Android ikonları (kaynak görseller)
store/                    Google Play ikonu, kapak görseli ve mağaza metinleri
www/index.html            Oyunun tamamı (HTML + CSS + JS), Android uygulaması bunu kullanır
docs/index.html           www/index.html'in kopyası, GitHub Pages bunu yayınlar
capacitor.config.json     Android sarmalayıcı ayarı
package.json
```

Oyun mantığı `index.html` içinde `//#LOGIC` ve `//#END` işaretleri arasında, arayüzden bağımsızdır, bu yüzden Node ile simüle edilebilir.

## Tarayıcıda çalıştırma

`www/index.html` dosyasına çift tıkla.



Notlar:
- Tarayıcı sürümünde (GitHub Pages) gerçek ödeme yoktur, paketler "Ücretsiz dene" olarak görünür.
- Dijital ürünlerde Google Play'in kendi ödeme sistemi zorunludur, başka ödeme yöntemi eklenmemelidir.
- Satın alma doğrulaması cihazda yapılır, sunucu doğrulaması yoktur. Tek kişilik çevrimdışı bir oyun için kabul edilebilir, ama kötü niyetli biri kayıt verisini değiştirip para ekleyebilir. İleride sunucu doğrulaması eklenebilir (ör. Iaptic).

## Fikirler

- [ ] Daha fazla olay türü (kampanya, vergi denetimi)
- [ ] Atölye yükseltmeleri ve yeni mobilya türleri
- [ ] Ses efektleri ve grafikler
- [ ] Skor tablosu

## Lisans

MIT, bkz. [LICENSE](LICENSE).


