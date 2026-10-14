# Teknik açıklama

Uygulama tek `google_yorumlari_otomatik.py` dosyasındadır. `WORKSPACE` dosyanın klasöründen hesaplanır. Ana bağımlılıklar Playwright ve openpyxl; diğer kod standart Python kütüphanesidir.

## Bileşenler

| Bileşen | Görev |
| --- | --- |
| main / bootstrap | Kullanıcı akışı, paket kontrolü ve gerektiğinde PyPI kurulumu |
| validate_url / map_place_key | Google Maps HTTPS bağlantısı ve işletme eşleştirme |
| chrome | Kurulu Chrome, ayrı profil, yerel CDP bağlantısı |
| prepare_reviews | Panel, seçili yorum sekmesi ve ilk kart kurtarması |
| collect | Kaydırma, yeni ID bekleme, duraklama ve bitiş kontrolleri |
| READ_META | İşletme adı, toplam, puan ve yıldız dağılımı |
| READ_CARD / CARD_HELPERS | Yorum/cevap bölümleri, özgün metin ve devam kontrolleri |
| merge_raw_variants / normalize | Aynı ID temsillerini birleştirme ve alan durumları |
| expand_bulk / expand_remaining | Kapalı kontrolleri işleme ve tekrar doğrulama |
| report | Toplam, benzersiz kayıt, alan ve yıldız eşleşmesi |
| export / verify_excel | Excel üretimi, geri okuma doğrulaması, atomik değiştirme |
| Progress | Türkçe aşama, sayaç ve kalan süre |

## Akış

1. Hedef işletme ve erişim kontrol edilir. İlk kart yoksa panel sınırlı kez kaydırılır.
2. Görünen kaynaklar kurtarma kaydına alınır.
3. Kaydırılabilir alan `scrollTop = scrollHeight` ile o anda yüklenmiş listenin dibine gider. Yeni yorumlar Google tarafından parça parça gelir.
4. Yeni yorum ID'si DOM'a girince devam edilir; gelmezse en fazla 4 saniye beklenir. Kopya ID yeni kayıt sayılmaz.
5. Bitiş adayı tekrar kontrol edilir; bilinen toplamdan az kayıtta sınırlı yeniden tetikleme vardır.
6. Yükleme bittikten sonra özgün metin ve More kontrolleri işlenir. Yorum ve işletme cevabı ayrı doğrulanır.
7. Son toplam ve alanlar okunur. Excel yaklaşık yorum yaşına göre yeni–eski sıralanır; Maps toplama sırası değiştirilmez.
8. Excel geçici dosyaya yazılır, tekrar açılıp doğrulanır; son dosyanın yerine konur.

## Veri doğrulama

Kayıt anahtarı müşteri adı değil Google yorum ID'sidir. Aynı adlı kişiler karıştırılmaz. Kopya kartlarda yorum ve cevap bağımsız seçilir; açık, özgün, tam metin tercih edilir. Çelişkiler işaretlenir. Kısa kopyanın açık eşdeğeri doğrulanmadan kapalı düğmesi yok sayılmaz.

Başlangıç/son toplam ve benzersiz adet karşılaştırılır; beş yıldız sınıfı okunursa dağılım kontrol edilir. Puanla birleşmiş kapsayıcıların sahte toplam oluşturması önlenir; adaylar gerekirse histogramla çapraz kontrol edilir, kaynak kaydedilir.

Kapalı devam, etkin çeviri, okunamayan metin/cevap/tarih ve kimlik sorunları kalite alanlarına girer. “Yanıt yok” ve “yanıt bilgisi alınamadı” farklıdır. Üç nokta tek başına hata değildir. Bu kontroller görünmeyen içeriğin %100 doğruluğunu kanıtlamaz; UI değişiklikleri okuyucuyu etkileyebilir.

## Excel ve teknik dosyalar

Sekiz ana yorum sütunu: müşteri adı, metni, yıldız, işletme cevabı, yorum zamanı, dil, Türkçe çeviri durumu, cevap zamanı.

32.767 karakteri aşan hücreler devam sütunlarına bölünür. XML kontrol karakterleri açık kaçış metnine dönüştürülür. Formül gibi başlayan müşteri metni metin hücresi olarak kaydedilir. Sayfalar ve hücreler yeniden açılıp kontrol edilir; float değerlerde 1e-12 tolerans vardır, metin/tam sayılar birebir karşılaştırılır. Excel kilitliyse önceki dosya korunur.

| Teknik dosya | İçerik |
| --- | --- |
| calisma.log | Tur, düğme, hata ve süre bilgileri |
| yorum_kurtarma.json | Satırlar, ham görünümler, metadata, hata ve ilerleme |
| sonuc.json | Kontrol özeti, sıralı ID'ler, dosyalar ve performans sayaçları |
| Gerektiğinde PNG | İlk yorum/erişim/metin düğmesi hatası kanıtı |

Snapshot bütün yüklenmiş kartları tekrar okur; artımlı okuma uygulanmamıştır. DOM okuma, Python birleştirme ve JSON yazım süreleri ayrı ölçülür. Kurtarma verisi her snapshot'ta güncellenir. Yerel dosya yolları teknik çıktıda bulunur, depoya yüklenmez.

Genel yüzde yaklaşık aşama ağırlığıdır. ETA son yaklaşık 60 saniyelik kayıt hızını kullanır; mevcut aşamanın kalanı tahmin edilir. Kısa bekleme yüzdeyi yüksek aşamaya sıçratmaz. 2 saat/10.000 tur sınırları vardır.

## Kapsam

Kod işletmeye yorum/yanıt göndermez ve korumaları aşmaz. Belgelenmemiş endpoint tekrar oynatma, ağ yanıtından yorum çıkarma, çok sekmeli paralel toplama, OCR veya ücretli çeviri kullanılmaz. Windows dışı ortam test edilmemiştir.

Önceki süreçten kalan `analyze_saved / deep_analysis / add_analysis_sheet` fonksiyonları isteğe bağlı `--analyze` ile kullanılır. Doğrulanmış kayıtlı JSON'dan yaklaşık dönem/yıldız/yanıt göstergeleri ve DERİN ANALİZ sayfası üretir; kaynak JSON'u değiştirmez, aynı işletmenin Excel'ini günceller. Bu deneysel komut kapsamlı NLP veya personel değerlendirmesi değildir; varsayılan iki sayfalı akışa dahil değildir.
