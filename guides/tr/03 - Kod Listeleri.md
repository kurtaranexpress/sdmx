# 03 – Kod Listeleri (metadatanın okunabilir & işlenebilir olması)

## Neden kod listeleri?

Sayımızı metadata ile anlamlı hale getirdik (ülke, yıl, gösterge…).  
Peki **bu metadatayı herkesin anlayacağı ve makinelerin kullanabileceği hale nasıl getiririz?**

Renkleri düşünün: *“mavi”* veya *“kırmızı”* demek dile bağlıdır.  
Ama `BLU` veya `RED` gibi bir **kod**, dil bağımsızdır.  
**Kod listeleri**, kısa ve sabit **kodları** çok dilli, insan dostu etiketlerle eşleyen sözlüklerdir.

**Faydaları**
- **Açıklık:** bir kavram değeri → tek, net kod (Türkiye/Turkey/TR karmaşası yok)  
- **Makine dostu:** sorgular, join’ler, filtreler daha hızlı (kodlar anahtar gibi)  
- **Doğrulama:** geçersiz değerler otomatik reddedilir  
- **Çok dilli:** aynı kod, birçok dilde etiket  
- **Uyumluluk:** başkaları verinizi çeviri yapmadan kullanabilir  

Kavramlarda olduğu gibi yol şu: **küresel → alan → yerel**.

---

## Önce küresel: standart listeleri yeniden kullan

Mümkün olduğunda **alanlar arası / uluslararası** listeleri kullanın:

| Kavram         | Tipik küresel kod listesi         | Örnek kodlar                          |
|----------------|----------------------------------|---------------------------------------|
| `FREQ`         | `CL_FREQ`                        | `A` (Yıllık), `Q` (Çeyrek), `M` (Aylık) |
| `REF_AREA`     | ISO 3166 (ülke/bölgeler)         | `TR` (Türkiye), `FR` (Fransa)         |
| `TIME_PERIOD`* | SDMX zaman formatları (kod listesi değil) | `2025`, `2025-Q1`, `2025-01`          |
| `UNIT_MEASURE` | Küresel veya alan bazlı birim listeleri | `PERS` (Kişi), `EUR`, `INDEX`        |

\* Zaman, **formatlar** kullanır; sabit kodlar değil ama standartlaştırılmıştır.

Küresel listeleri yeniden kullanmak, İspanya’daki veya Fransa’daki bir analistin veri anahtarlarını hemen anlayabilmesi demektir.

---

## Sonra gerekirse yerelde genişletin

Alanınız daha fazla detay gerektiriyorsa **alan/yerel** kod listeleri oluşturun:

- `SEX` → `F` (Kadın), `M` (Erkek), `T` (Toplam)  
- `INDICATOR` → `POP` (Nüfus), `CPI`, `GDP`…  

Kodlarınızı **kısa, sabit, belgeli** ve versiyonlu tutun.

---

## Örnek: nüfus veri seti – minimal set

### Küresel / paylaşılan listeler

**`CL_FREQ`**
| Kod | Etiket (EN) | Açıklama              |
|-----|-------------|-----------------------|
| A   | Annual      | Yıllık gözlemler      |
| Q   | Quarterly   | Çeyreklik gözlemler   |
| M   | Monthly     | Aylık gözlemler       |

**`REF_AREA`** (ISO 3166’dan alıntı)
| Kod | Etiket      |
|-----|-------------|
| TR  | Türkiye     |
| FR  | Fransa      |

**`UNIT_MEASURE`**
| Kod  | Etiket          | Notlar                  |
|------|-----------------|--------------------------|
| PERS | Kişi            | Kişi sayısı             |
| MILP | Milyon kişi     | Kişi / 1.000.000        |

---

### Yerel / alan listeleri

**`CL_SEX`**
| Kod | Etiket  |
|-----|---------|
| F   | Kadın   |
| M   | Erkek   |
| T   | Toplam  |

**`CL_IND`**
| Kod | Etiket               | Notlar                 |
|-----|----------------------|-------------------------|
| POP | Nüfus (başlık)       | Yerleşik nüfus          |

---

## Kod listeleri modelle nasıl bağlanır?

- **Kavramlar** anlamı tanımlar (örn. `REF_AREA`, `SEX`).  
- **Kod listeleri** bu kavramlar için geçerli değerleri listeler.  
- DSD’de boyut veya öznitelikleri açıkça kod listesine bağlarsınız:  
  - `REF_AREA → CL_AREA`  
  - `FREQ → CL_FREQ`  
  - `SEX → CL_SEX`  
  - `INDICATOR → CL_IND`  

Bu sayede:  
- Sadece **geçerli anahtarlar** kullanılabilir.  
- Sorgular ve filtreler kesinleşir.  
- Veriler otomatik doğrulanabilir.  

---

## Yönetişim & versiyonlama

İyi uygulama kuralları:  
- **Sabit kodlar:** yayımlandıktan sonra kodları değiştirmeyin; etiketleri güncelleyin.  
- **Kısa ID’ler:** boşluk yok, `[A–Z0–9_]` kullanın.  
- **Versiyonlama:** `CL_IND (v1.0)` gibi sürümler tutun, değişiklikleri not edin.  
- **Eşleştirme:** eski kodlardan geçiş yapıyorsanız mapping tablosu yayınlayın.  
- **Kademeli kaldırma:** kodları “deprecated” işaretleyin ama hemen silmeyin.  

---

## Gelen verileri doğrulama

Verileri kod listelerine göre kontrol etmek için basit kurallar:  
- Her gözlem anahtarı bağlı olduğu kod listesinden kod kullanmalı.  
- Zaman formatı frekansa uymalı (örn. `M` → `YYYY-MM`).  
- Birimler, seri içinde tutarlı olmalı (veya öznitelik olarak açıkça verilmeli).  

Küçükten başlayın:  
- Önce `REF_AREA`, `FREQ`, `TIME_PERIOD` doğrulayın.  
- Sonra `SEX`, `INDICATOR`, `UNIT_MEASURE`’a genişletin.  

---

## Kısaca (TL;DR)

- **Kavram = ne demek?**  
- **Kod listesi = hangi değerler geçerli?**  
- Önce küresel kod listelerini kullanın, gerekirse yerelde genişletin.  
- Kod listelerini sürümleyin ve belgelendirin ki başkaları güvenle kullansın.  

---

👉 [Sonraki Bölüm – DSD](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/04%20-%20DSD.md)
