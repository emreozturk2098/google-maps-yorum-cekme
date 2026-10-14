# Sıfırdan kullanım rehberi

## 1. Python ve Chrome

Windows bilgisayarınızda Google Chrome ve Python 3.10 veya üzeri kurulu olmalı. Python kurulumunda komut satırı/PATH seçeneğini etkinleştirin. Proje Python 3.13.0 ile denenmiştir.

PowerShell veya Komut İstemi'nde:

```powershell
python --version
```

Komut bulunmuyorsa `py --version` deneyin. İkisi de bulunmuyorsa Python kurulumunu/PATH ayarını kontrol edin. Dosyayı çift tıklamak yerine terminalde çalıştırın.

## 2. İndirme ve klasör

GitHub'da **Code → Download ZIP** seçin. ZIP'i örneğin `C:\Projeler\Google_Maps` klasörüne çıkarın. Python dosyasını ZIP'in içinden çalıştırmayın. `google_yorumlari_otomatik.py` ve `requirements.txt` bulunmalı.

Dosya Gezgini'nde klasöre girip adres çubuğuna `powershell` yazın ve ENTER'a basın. Terminal bu klasörde açılır.

## 3. Kurulum

```powershell
python -m pip install -r requirements.txt
```

Playwright 1.61.0 tarayıcıyı kontrol eder, openpyxl 3.1.5 Excel yazar. Microsoft Excel uygulaması gerekmez. Kurulu Chrome kullanılır; ayrıca Playwright tarayıcısı indirmek gerekmez.

İsteğe bağlı sanal ortam:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe google_yorumlari_otomatik.py
```

Bu yöntem ortamı etkinleştirmeden onun Python'ını kullanır; PowerShell çalıştırma politikasını değiştirmeniz gerekmez. Aşağıdaki `python` komutlarını sanal ortamın tam yoluyla değiştirebilirsiniz.

## 4. Çalıştırma

```powershell
python google_yorumlari_otomatik.py
```

Başka klasördeyseniz:

```powershell
python "C:\Projeler\Google_Maps\google_yorumlari_otomatik.py"
```

Çıktılar terminalin mevcut klasörüne değil Python dosyasının klasörüne kaydedilir. Normal çalışma ek argüman gerektirmez.

## 5. Bağlantı ve giriş

1. Maps'te işletmenin sayfasını açın, HTTPS bağlantısını adres çubuğundan kopyalayın.
2. Program istediğinde yapıştırıp ENTER'a basın. Kısaltılmış Maps bağlantıları desteklenir; sorun varsa açılmış tam adresi kullanın.
3. Açılan Chrome'da gerekli Google girişini ve çerez tercihini tamamlayın. Parolayı konsola yazmayın.
4. Girilen bağlantının işletme sayfasına dönün. Konsol hazır olmasını istediğinde ENTER'a basın.

Program ayrı `Chrome_profili` oluşturur. Sonraki run'da oturum korunabilir. Dosyayı başka klasöre taşırsanız farklı profil oluşur. Önceki proje Chrome'u açık kaldıysa kapatıp yeniden deneyin; günlük kişisel Chrome profiliniz kullanılmaz.

## 6. İlerlemeyi okuma

Konsol hazırlık, yükleme, metin açma ve Excel aşamalarını gösterir. Genel yüzde yaklaşık aşama ağırlığıdır. Yükleme sayacı benzersiz yorum sayısıdır; metin açma sayacı düğme işlerini gösterebilir. ETA aynı aşamanın ölçülen hızına göre değişir, başta “hesaplanıyor” yazabilir.

**More/Daha fazla ve özgün metin kontrolleri liste yüklendikten sonra** işlenir. İşletme cevabı da ayrı kontrol edilir. Bir tıklama kesin başarı sayılmaz; son durum tekrar okunur. Kısmi çıktı varsa %100 dosya üretiminin bitişini ifade edebilir; tamlık garantisi değildir.

## 7. Excel

`Google_yorum/<İşletme>_Yorumlar.xlsx` dosyasını açın. ÖZET kısa işletme bilgileri; TÜM YORUMLAR müşteri metni, yıldız, cevap, tarihler ve dil alanlarıdır. Aynı işletmede yeni run aynı dosyayı günceller; önce Excel'i kapatın. Farklı işletmeler ayrı dosyalarda kalır.

Tamamen kurgu bir örnek:

| Yorum yapan kişi | Müşteri yorumu | Yıldız | İşletmenin cevabı | Yorum zamanı | Dil |
| --- | --- | ---: | --- | --- | --- |
| Örnek Müşteri A | Hizmetten memnun kaldım. | 5 | Teşekkür ederiz. | 2 ay önce | Türkçe |

Gerçek dosyada ayrıca Türkçe çeviri durumu ve cevap zamanı vardır. Otomatik çeviri yapılmaz. Yalnızca yıldız verilmesi eksik metin hatası değildir. Fotoğraflı yorumların normal metni alınır; fotoğraf içi yazı/ayrı açıklama alınmaz.

## 8. Sorun çözme

| Sorun | Kontrol |
| --- | --- |
| Python bulunamadı | Kurulum/PATH, `py` veya Python'ın tam yolu |
| Chrome açılmıyor | Chrome kurulumu, aynı proje profiline ait açık oturum |
| Giriş takılıyor | Giriş tarayıcıda tamamlandı mı; hedef işletmeye dönüldü mü? |
| İlk yorum gelmiyor | Kod kontrollü kaydırmayı dener; log ve varsa ekran görüntüsünü inceleyin |
| CAPTCHA/erişim kısıtı | Kullanıcı tarayıcıda gereken işlemi yapar; kod korumayı aşmaz |
| Excel kaydedilmiyor | Dosya açık/kilitli mi; klasöre yazma izni var mı? |
| Yükleme yavaş | Ağ/Maps ve büyüyen DOM maliyetleri; teknik log süreleri |
| Sayı eksik | Başlangıç/son toplam değişimi, erişim, filtre ve hata aşaması |

`Calisma_kayitlari/<zaman>/` içinde `sonuc.json`, `calisma.log`, `yorum_kurtarma.json` ve gerekirse PNG bulunur. Eksik/hatalı çalışma tam başarı sayılmaz. Ctrl+C durdurabilir; kurtarma kaydı korunmaya çalışılır. Yazım sırasında tekrar zorla kapatmak kaydı etkileyebilir. Yarım JSON'dan kaldığı kaydırma noktasına otomatik devam yoktur.

## 9. İsteğe bağlı komutlar

`python google_yorumlari_otomatik.py --self-test` tarayıcı açmadan saf fonksiyon kontrolleri yapar; gerçek Maps erişimi/tamamlık testi değildir.

`--analyze [yorum_kurtarma.json]` önceki geliştirmelerden kalan deneysel komuttur. Tamlığı doğrulanmış kayıttan basit dönem/yanıt göstergeleri ve üçüncü sayfa üretir; normal toplama açmaz. Derin duygu/konu/personel analizi değildir. Normal yorum çekme için gerekmiyor.

Görüş, hata veya öneri için [emre.ozturk.2098@gmail.com](mailto:emre.ozturk.2098@gmail.com) adresine yazabilirsiniz.
