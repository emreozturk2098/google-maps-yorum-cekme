# Gerçek deneme sonuçları

İşletme adları gizlenmiştir. Süre, kullanıcının ENTER tuşuna basmasından Excel kaydının tamamlanmasına kadar ölçülmüştür. Chrome açılışı, bağlantı yazma ve Google girişini bekleme bu süreye dahil değildir.

| Örnek | Değerlendirme | Metinli | Yalnızca yıldız | Tespit edilen işletme cevabı | Toplam süre |
| --- | ---: | ---: | ---: | ---: | --- |
| İşletme A | 107 | 86 | 21 | 66 | 30,27 sn |
| İşletme B | 1.445 | 958 | 487 | 0 | 13 dk 16,26 sn |

## İşin aşamaları

Araç yorum listesini kaydırarak yeni kayıtların yüklenmesini bekler. Ardından uzun yorumları ve işletme cevaplarını açar, kayıtları kontrol eder ve Excel'i kaydeder.

1.445 değerlendirmeli örnekte listeyi yükleme yaklaşık **12 dakika**, metinleri açma, son kontroller ve Excel kaydı yaklaşık **1 dakika 14 saniye** sürmüştür. Başlangıç/bitiş işlemleri nedeniyle aşama sürelerinin toplamı toplam süreyle birebir aynı değildir. En fazla zamanı liste yükleme ve yeni kayıt bekleme almıştır.

## Sonuçların kontrolü

- Bu çalışmalarda Maps'te görünen toplam ile alınan kayıt sayısı ve yıldız dağılımı eşleşmiştir; alan eksikliği veya çalışma hatası kaydedilmemiştir.
- Kayıt kimlikleri, müşteri adları, yıldızlar, özgün yorum metinleri ve işletme cevapları tekrar edilen çalışmalarda karşılaştırılmıştır; karşılaştırılan alanlarda fark bulunmamıştır.
- Sıfır cevap, aracın bu çalışmada tespit ettiği durumdur; işletmenin hiçbir zaman cevap yazmadığına dair bağımsız kanıt değildir.
- Gerçek müşteri satırları, Excel dosyaları ve oturum dosyaları bu depoda paylaşılmaz.

## Süreleri nasıl yorumlamalı?

Ölçümler Windows, Python ve kurulu Chrome ile yapılan gerçek kullanıcı denemeleridir. CPU/RAM, ağ hızı ve Google sunucu koşulları kaydedilmemiştir. Bunlar kontrollü laboratuvar ortalamaları değildir.

Küçük ve büyük örneğin süresi doğrusal artmak zorunda değildir. Bu iki sonuçtan 20 bin yorumun süresi kesin hesaplanamaz. Maps arayüzünün değişmesi, ağ ve büyüyen sayfa içeriği süreyi etkileyebilir. Toplam ve yıldız eşleşmesi görünmeyen bütün içeriğin eksiksiz olduğunu tek başına kanıtlamaz.

Yeni ölçüm paylaşırken görünen/alınan kayıt sayısını, metin ve cevap adetlerini, süre başlangıcı/bitişini ve varsa hata durumunu belirtin. Kalite kontrolü tamamlanmadan yalnızca kısa süreyi başarı ölçütü olarak kullanmayın.
