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

## Android uygulaması oluşturma

Gerekenler: [Node.js](https://nodejs.org) ve [Android Studio](https://developer.android.com/studio).

```
npm install @capacitor/core @capacitor/cli @capacitor/android cordova-plugin-purchase
npx cap add android
npx cap sync
npx cap open android
```

Android Studio açılınca bir emülatörde veya USB ile bağlı telefonda **Run** ile dene. Telefonunda ilk testi yapmak için bu yeterli.

### Google Play için paket (AAB)

1. Android Studio'da **Build → Generate Signed App Bundle / APK → Android App Bundle** seç.
2. Yeni bir **keystore** oluştur. Bu dosyayı ve parolasını güvenli bir yerde sakla, kaybedersen uygulamayı güncelleyemezsin. Repoya yükleme (`.gitignore` zaten engelliyor).
3. Çıkan `.aab` dosyasını Play Console'a yükle.

## Google Play'e yükleme

1. [Play Console](https://play.google.com/console) geliştirici hesabı aç (tek seferlik kayıt ücreti ve kimlik doğrulaması var).
2. Yeni uygulama oluştur, mağaza sayfasını doldur (açıklama, ikon 512×512, ekran görüntüleri, öne çıkan görsel).
3. İçerik derecelendirmesi ve **Veri güvenliği** formlarını doldur. Oyun veri toplamıyor, bunu belirt.
4. Çoğu durumda bir gizlilik politikası bağlantısı istenir. Veri toplamadığını söyleyen basit bir sayfa (GitHub Pages ile yapılabilir) yeterlidir.
5. **Önemli:** Kişisel hesabın 13 Kasım 2023'ten sonra açıldıysa, üretime çıkmadan önce **en az 12 test kullanıcısıyla 14 gün kesintisiz kapalı test** yapman gerekir. Kurumsal hesaplar bundan muaftır. Sonra üretim erişimi için başvurursun.

Kurallar zamanla değişebilir, güncel hâli için [Play Console yardım sayfasına](https://support.google.com/googleplay/android-developer/answer/14151465) bak.

## Uygulama içi satın alma kurulumu

Oyun, Google Play Billing için [`cordova-plugin-purchase`](https://github.com/j3k0/cordova-plugin-purchase) eklentisini kullanır. Ürün kimlikleri koddaki `PACKS` listesindedir ve Play Console'daki kimliklerle **birebir aynı** olmalıdır.

| Ürün kimliği | Verdiği para |
|---|---|
| `para_8000` | 8.000 ₺ |
| `para_20000` | 20.000 ₺ |
| `para_60000` | 60.000 ₺ |

1. Play Console'da uygulamanı aç, **Monetize → Products → In-app products** bölümüne git (menü adları değişebilir).
2. Yukarıdaki üç kimlikle üç ürün oluştur, fiyatlarını ve açıklamalarını gir, **Active** yap. Oyun fiyatı mağazadan okuyup gösterir, koda fiyat yazmana gerek yok.
3. Ödeme alabilmek için Play Console'da **ödeme (merchant) profili** gerekir.
4. Test için Play Console'da **Settings → License testing** bölümüne test hesaplarını ekle ve uygulamayı USB ile değil, **Play'in test kanalından** yükle. Doğrudan yüklenen uygulamalarda satın alma çoğu zaman çalışmaz.
5. Mağaza sayfasında uygulama içi satın alma içerdiğini belirt.

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

> `www/index.html` dosyasını değiştirirsen aynı değişikliği `docs/index.html` içine de kopyala, yoksa yayındaki oyun eski kalır.
