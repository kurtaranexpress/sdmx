# 01 – Giriş: Neden Metadata Önemlidir?

## Anlamsız bir sayı

Şu sayıyı düşünün:

**82.000.000**

Tek başına bu sayı anlamsızdır. Ne ifade ediyor? Hangi yıla ait? Hangi ülke için?

---

## Veriyi bilgiye dönüştürmek

Şunu söylediğimizde:

**“Türkiye’nin 2025 yılı nüfusu 82 milyondur.”**

Artık bu değerin *metadatası* vardır:
- **Gösterge (Indicator):** Nüfus
- **Referans alanı (REF_AREA):** Türkiye
- **Zaman dönemi (TIME_PERIOD):** 2025
- **Değer (OBS_VALUE):** 82.000.000
- **Birim (Unit):** Kişi

---

## Daha fazla detay eklemek

Şu ifadeyi düşünün:

**“İstanbul’un 2025 yılı kadın nüfusu 9 milyondur.”**

Yeni bir boyuta ihtiyaç duyuldu:
- **Gösterge (Indicator):** Nüfus
- **Referans alanı (REF_AREA):** İstanbul
- **Zaman dönemi (TIME_PERIOD):** 2025
- **Cinsiyet (SEX):** Kadın
- **Değer (OBS_VALUE):** 9.000.000
- **Birim (Unit):** Kişi

---

## Çıkarılan ders

- Aynı değer, **farklı ayrıntı seviyelerinde** tanımlanabilir.  
- İstatistik ofisi hangi boyutlara ihtiyaç olduğuna karar verir.  
- **Modeller** bu karardan **sonra** devreye girer ve kavramları, kod listelerini, yapıları tasarlar.  

---

## 🔑 Ek İpuçları & Tuzaklar

- Her zaman işe **değişim ihtiyacını netleştirerek** başlayın: Hangi veri setleri paylaşılacak? Gönderen ve alan kim?  
- Kapsam içindeki veri akışlarını (raporlama vs yayım) göstermek için **basit bir akış diyagramı** kullanın.  
- Unutmayın: **metadata bağlamdır.** Metadata olmadan bir sayı değersizdir. Metadata ile veri, karşılaştırılabilir, yeniden kullanılabilir ve güvenilir hale gelir.  
- Yapılara hemen atlamayın — önce **amaç ve kapsam** konusunda anlaşın.  

---

👉 [Sonraki Bölüm: Kavramlar](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/02%20-%20Kavramlar.md)
