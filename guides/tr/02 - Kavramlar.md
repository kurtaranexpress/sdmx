# 02 – Kavram Şeması

## Sayılardan kavramlara

Şunu söylediğimizde:  
**“Türkiye’nin 2025 yılı nüfusu 82 milyondur”**,  

şu **kavramları** ayırt edebiliriz:  
- Ülke (Türkiye)  
- Yıl (2025)  
- Gösterge (Nüfus)  
- Değer (82.000.000)  
- Birim (Kişi)  

Her gözlem bu tür kavramların bir kombinasyonudur.  
Bu ayrıntıları tanımlama faaliyetine **modelleme** denir.  

---

## Sorun: herkes kendi etiketini icat ediyor

Üç ülkenin nüfus verisi yayımladığını hayal edin:  
- Türkiye → “Türkiye”  
- İspanya → “TR”  
- Fransa → “TUR”  

Hangisi doğru? Herkes kendi etiketini tanımlarsa, **veriler karşılaştırılamaz ve entegre edilemez**.  

---

## Çözüm: kayıtlar (registries)

Bunu çözmek için SDMX **kayıtları (registry)** kullanır.  
Bir registry, herkesin aynı kelimeleri kullanması için hazırlanmış **resmî kavramlar ve kodların sözlüğü** gibidir.  

Registry seviyeleri vardır:  
1. **Küresel registry** → tüm alanlarda geçerli kavramlar (cross-domain concepts).  
2. **Alan registry’leri** → konuya özel (ör. demografi, ulusal hesaplar).  
3. **Yerel registry’ler** → kurum içi kavramlar.  

**Altın kural:** Önce küresel registry’ye bakın, sonra alan ya da yerel seviyeye inin.  

---

## Alanlar arası kavramlar (CDC)

Bunlar istatistiğin “ortak sözlüğüdür” — tüm veri setlerinde tekrar kullanılabilir kavramlar:  
- `REF_AREA` → ülke veya bölge (ISO kodları, örn. TR, FR)  
- `TIME_PERIOD` → gözlem zamanı (YYYY, YYYY-Qn, YYYY-MM)  
- `FREQ` → sıklık (A/Yıllık, Q/Çeyrek, M/Aylık)  
- `UNIT_MEASURE` → ölçü birimi (kişi, EUR, endeks)  
- `OBS_VALUE` → sayısal değer  

---

## Yerel kavramlarla genişletme

Küresel registry ihtiyacınızı karşılamıyorsa, alan veya yerel kavramlarla genişletirsiniz.  
Örnek:  
**“İstanbul’un 2025 yılı kadın nüfusu 9 milyondur.”**  
Burada `SEX` gerekir → bu bir **alana özgü** kavramdır.  

---

## Örnek Kavram Şeması

| Kavram ID     | Adı              | Açıklama                                              | Seviye         |
|---------------|------------------|-------------------------------------------------------|----------------|
| `REF_AREA`    | Referans alanı   | Ülke/bölge (TR, FR, İstanbul)                         | Küresel (CDC)  |
| `TIME_PERIOD` | Zaman dönemi     | Gözlemin yılı, çeyreği, ayı                           | Küresel (CDC)  |
| `FREQ`        | Sıklık           | Periyodiklik (A/Q/M)                                  | Küresel (CDC)  |
| `UNIT_MEASURE`| Ölçü birimi      | Birim (kişi, endeks, EUR)                             | Küresel (CDC)  |
| `OBS_VALUE`   | Gözlem           | Sayısal değer                                         | Küresel (CDC)  |
| `INDICATOR`   | Gösterge         | Ne ölçülüyor (Nüfus, TÜFE, GSYH)                      | Alan/yerel     |
| `SEX`         | Cinsiyet         | Kadın, Erkek, Toplam                                  | Alan/yerel     |

---

## Ana mesaj

- Kavramlar verinizin **dilidir**.  
- Registry’ler herkesin aynı dili konuşmasını sağlar.  
- Önce küresel kavramları yeniden kullanın, sadece gerekirse genişletin.  

👉 [Sonraki Bölüm – Kod Listeleri](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/03%20-%20Kod%20Listeleri.md)
