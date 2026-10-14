# Performans ve doğrulama

14.10.2026. Kullanıcının gerçek Maps çalışmalarından toplu sonuçlar. Süre ENTER sonrası “İşletme bilgileri okunuyor” satırından Excel kaydının bitişine kadar; Chrome açma, URL yazma ve giriş beklemesi hariçtir.

| İşletme / sürüm | Değerlendirme | Metinli | Yalnızca yıldız | Tespit edilen cevap | Toplam süre |
| --- | ---: | ---: | ---: | ---: | --- |
| FAMİ / 4.1 | 107 | 86 | 21 | 66 | 30,27 sn |
| Honda / 4.3 | 1.445 | 958 | 487 | 0 | 13 dk 37,81 sn |
| Honda / **4.4** | **1.445** | **958** | **487** | **0** | **13 dk 16,26 sn** |
| Honda / 4.5 | 1.445 | 958 | 487 | 0 | 13 dk 22,73 sn |
| Honda / 4.6 | 1.445 | 958 | 487 | 0 | 14 dk 31,51 sn |

Honda işletmesi Honda Plaza Damla'dır. Bu çalışmalarda toplam/yıldız dağılımı eşleşmiş, alan eksikliği/hata kaydedilmemiştir. Honda çalışmalarının ID kümesi ve bütün ad/yıldız/özgün metin/cevap alanları karşılaştırılmış; fark bulunmamıştır. FAMİ Excel'inin 107 satırı kaynak gösterimle; Honda 4.3 Excel'inin 1.445 temel ad/metin/yıldız/cevap alanı kaynakla eşleşmiştir.

Sıfır cevap okuyucunun bu çalışmalarda tespit ettiği durumdur; işletmenin hiçbir zaman cevap yazmadığı bağımsız kanıt değildir. Kullanıcı tarafından durdurulan denemeler başarı tablosuna eklenmedi. Gerçek müşteri kayıtları ve oturum dosyaları paylaşılmadı.

## Sürüm seçimi ve aşamalar

4.4 ölçülen Honda denemelerinde en kısa toplam süreyi verdi; kullanıcı isteğiyle kaynak byte düzeyinde 4.4'e döndürüldü. Her işletmede kesin en hızlı olduğu anlamına gelmez.

| Honda sürümü | Yükleme | Yükleme sonrası metin/kontrol/Excel |
| --- | ---: | ---: |
| 4.3 | 723,657 sn | 92,292 sn |
| 4.4 | 720,053 sn | 74,172 sn |
| 4.5 | 781,134 sn | 19,691 sn |
| 4.6 | 821,163 sn | 50,202 sn |

4.5 yüklerken More açarak sondaki işi azalttı; yükleme uzadı, toplam iyileşmedi. 4.6 erişim kontrolünü yaklaşık 95'ten 43 saniyeye indirdi; DOM/bekleme arttığı için toplam yine uzadı. Yerel maliyet azalması toplam hız artışı olarak sunulmadı.

4.4'te yeni kayıt bekleme yaklaşık 487 sn, DOM okuma 160 sn, birleştirme 5,7 sn, JSON yazma 10,2 sn; 447 snapshot/451 checkpoint vardı. Bekleme sırasında tarayıcı iş yapabileceği için bunlar yalnızca sunucu süresi demek değildir.

## Ölçüm sınırları

- Windows, Python 3.13.0, Playwright 1.61.0, openpyxl 3.1.5 ve kurulu Chrome kullanıldı.
- CPU/RAM, ağ hızı, Chrome sürümü ve Google sunucu koşulları kaydedilmedi.
- Her sürüm için burada tek tamamlanmış karşılaştırma var; kontrollü laboratuvar/çoklu tekrar ortalaması değildir.
- Küçük FAMİ sonucu ile Honda sonucu doğrusal hız modeli oluşturmaz; 20 bin yorumun süresi kesin çıkarılamaz.
- Toplam/yıldız/alan eşleşmesi bütün görünmeyen içeriğin %100 doğruluğunu kanıtlamaz.

Yeni ölçümde işletme, sürüm/hash, ortam, görünen/son/toplanan adet, metin/cevap adedi, hata ve süre başlangıcı birlikte belirtilmeli. Kalite eşleşmeden hızlı süre başarı sayılmamalı.
