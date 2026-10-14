# Google Maps Yorum Çekme

Google Maps işletme değerlendirmelerini ve işletme cevaplarını görünür Chrome oturumundan okuyup **Türkçe Excel raporuna** aktaran, Windows için tek Python dosyalı araç.

Normal çalıştırmada **ÖZET** ve **TÜM YORUMLAR** sayfaları üretilir. Google Maps API anahtarı gerekmez. Gerekli Google girişini kullanıcı tarayıcıda tamamlar; kod parola istemez.

## Özellikler

- İşletme adı, bağlantısı, ortalama puanı, değerlendirme sayısı ve 1–5 yıldız dağılımı.
- Müşterinin görünen adı, özgün yorumu, yıldızı, işletme cevabı, yorum zamanı, dil, çeviri durumu ve cevap zamanı.
- Uzun yorum ve cevaplarda **More / Daha fazla** kontrollerini açma; özgün metne dönme.
- Yorum kimliğiyle kopyaları birleştirme, toplam/yıldız/alan kontrolleri.
- Aynı işletmenin Excel'ini aynı dosya adıyla güncelleme.
- Ayrı teknik log, sonuç özeti, kurtarma JSON'u ve gerektiğinde hata ekran görüntüsü.

## Hızlı başlangıç

Gerekenler: **Windows**, **Python 3.10 veya üzeri**, kurulu **Google Chrome**, internet bağlantısı. Doğrulanan ortam Python 3.13.0'dır. Excel'i üretmek için Microsoft Excel kurulumu gerekmez.

1. **Code → Download ZIP** ile indirin ve ZIP'i bir klasöre çıkarın.
2. Bu klasörde PowerShell veya Komut İstemi açın.
3. Kurun ve çalıştırın:

```powershell
python -m pip install -r requirements.txt
python google_yorumlari_otomatik.py
```

`python` bulunmuyorsa `py` kullanabilirsiniz. Kurulu Chrome kullanılır; `playwright install` gerekmez. Kod eksik Playwright/openpyxl paketlerini otomatik kurmayı da dener. İlk kurulumdan sonra yalnızca ikinci komut yeterlidir.

4. Programın istediği Google Maps işletme bağlantısını yapıştırın.
5. Açılan Chrome'da giriş/çerez işlemlerini tamamlayıp hedef işletmeye dönün.
6. Konsolda **ENTER**'a basın; yorumlar yüklenir, ardından kapalı metinler açılır.
7. `Google_yorum/<İşletme>_Yorumlar.xlsx` dosyasını açın.

İlk defa kullananlar için adım adım anlatım: [Kullanım rehberi](KULLANIM_REHBERI.md).

## Excel

| Sayfa | İçerik |
| --- | --- |
| ÖZET | İşletme adı, Maps bağlantısı, ortalama puan, değerlendirme sayısı, yıldız dağılımı, rapor zamanı |
| TÜM YORUMLAR | Müşteri adı, yorum, yıldız, işletme cevabı, yorum zamanı, dil, Türkçe çeviri durumu, cevap zamanı |

Yanıt yazılmamışsa **“Yanıt yok”**, metin yoksa **“Yorum yazılmamış; yalnızca yıldız verilmiş”** gösterilir. Okunamayan/verisi doğrulanamayan alanlar gerçek yoklukla karıştırılmaz. Otomatik çeviri modeli kullanılmaz; doğrulanmış mevcut Türkçe çeviri yoksa **“Çeviri yapılmadı”** yazılır.

Fotoğraflı yorumun normal metni de alınır. Görsel içindeki yazılar, ayrı fotoğraf başlığı/açıklaması ve medya dosyaları kapsam dışıdır. Özgün metnin dili korunur. “2 ay önce” gibi tarihlerden kesin takvim günü üretilmez.

## Gerçek denemeler

Süre başlangıcı kullanıcının ENTER'a basması, bitiş Excel kaydının tamamlanmasıdır. Chrome açma, bağlantı yazma ve giriş beklemeleri hariçtir.

| Örnek | Değerlendirme | Metinli | Tespit edilen işletme cevabı | Süre |
| --- | ---: | ---: | ---: | --- |
| İşletme A | 107 | 86 | 66 | 30,27 sn |
| İşletme B | 1.445 | 958 | 0 | 13 dk 16,26 sn |

İşletme adları gizlenmiştir. Bu çalışmalarda görünen toplam ve yıldız dağılımı eşleşmiştir. Sıfır cevap, aracın bu çalışmada tespit ettiği durumdur; işletmenin hiçbir zaman cevap yazmadığının bağımsız kanıtı değildir.

Süreler gerçek denemelerden alınmıştır; başka bir işletmede aynı hız veya eksiksiz sonuç garantisi vermez. Aşamalar ve ölçüm sınırları: [Performans sonuçları](PERFORMANS_SONUCLARI.md).

## Nasıl çalışır ve sınırları

Playwright kurulu Chrome'a ayrı proje profili üzerinden bağlanır. Yorum listesi yüklenir; ardından özgün metin ve devam düğmeleri işlenir. Kayıtlar yorum kimliğiyle birleştirilir. Excel geçici dosyaya yazılır, tekrar açılarak doğrulanır ve son dosyayla değiştirilir.

- Maps arayüzü ve erişim koşulları değişebilir; kısmi sonuç oluşabilir. Konsoldaki son durumu ve `sonuc.json` dosyasını kontrol edin.
- CAPTCHA/erişim engeli aşılmaz; gerekli kullanıcı işlemleri tarayıcıda yapılır.
- Genel yüzde yaklaşık aşama ilerlemesidir; yükleme kayıt yüzdesi ayrı gösterilir. ETA mevcut aşamanın kalanıdır.
- Üç noktayla biten metin tek başına eksik metin sayılmaz.
- Büyük listelerde ağ bekleme ve büyüyen DOM yavaşlatabilir. Mevcut sınırlar 2 saat ve 10.000 kaydırma turudur; sınırda kısmi durum raporlanır.
- Excel açık/kilitliyse yeni kayıt başarısız olabilir; önceki dosya korunur. Excel'i kapatıp yeniden deneyin.

[Teknik açıklama](TEKNIK_ACIKLAMA.md) fonksiyonları ve kontrolleri anlatır. Kaynakta önceki geliştirmelerden kalan isteğe bağlı `--analyze` komutu vardır; kayıtlı veriden deneysel ilk dönem/yanıt göstergelerini üretir. Normal çalıştırmaya dahil değildir, kapsamlı metin/duygu analizi sunmaz. Bu yayının temel akışı yorum çekmedir.

## Dosyalar

```text
google_yorumlari_otomatik.py   Tek uygulama dosyası
requirements.txt               Doğrulanan bağımlılıklar
KULLANIM_REHBERI.md             Sıfırdan kurulum ve sorun çözme
TEKNIK_ACIKLAMA.md              Kod akışı ve teknik çıktılar
PERFORMANS_SONUCLARI.md         Ölçülen denemeler
CONTRIBUTING.md                Katkı ve hata bildirimi
LICENSE                        MIT lisansı
```

Çalıştırınca `Chrome_profili/`, `Google_yorum/` ve `Calisma_kayitlari/` oluşur. `.gitignore` bunları dışlar. Depo gerçek müşteri satırlarını, Excel'leri, Chrome oturumunu veya özel çalışma hafızasını içermez; deneme verileri yalnızca toplu sayılarla paylaşılmıştır.

## Geri bildirim ve iletişim

Olumlu/olumsuz görüşleriniz, hata bildirimleriniz ve geliştirme önerileriniz için **[emre.ozturk.2098@gmail.com](mailto:emre.ozturk.2098@gmail.com)** adresine yazabilir veya [GitHub Issues](https://github.com/emreozturk2098/google-maps-yorum-cekme/issues) üzerinden bildirim açabilirsiniz. Beklenen ve görülen davranışı, alınan kayıt sayısını ve süreyi belirtmeniz yardımcı olur. Oturum çerezleri, parolalar ve özel müşteri verileri göndermeyin.

Özgün kod **MIT lisansıyla** paylaşılmıştır. Bu lisans Google verilerine veya üçüncü taraf hizmetlere hak vermez. [Lisans](LICENSE).
