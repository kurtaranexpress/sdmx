# 08 – Tablodan Modelleme

## Neden önemli?

Pratikte veriler çoğunlukla temiz bir SDMX veri seti olarak başlamaz.  
Genellikle elinizde bir Excel tablosu, CSV dosyası veya veritabanı tablosu olur.  
Mesele şu: **Bu tabloyu geçerli bir SDMX modeline nasıl dönüştürürüz?**

Bu, *tümdengelim yaklaşımıdır*: Mevcut bir veri setinden başlayıp onu kavramlara, kod listelerine, bir DSD’ye ve en sonunda bir Veri Akışı’na eşlemek.

---

## Adım 1 – Tabloya bak

Örnek tabloyu bu sefer şu linkten alalım: [OECD Data Explorer - Historical Population Data](https://sdmx.oecd.org/public/rest/data/OECD.ELS.SAE,DSD_POPULATION@DF_POP_HIST,1.0/CZE+EST+DNK+FIN+FRA+DEU+GRC+HUN+ISL+IRL+ISR+ITA+JPN+KOR+LVA+LTU+LUX+MEX+NLD+NZL+NOR+POL+PRT+SVK+SVN+ESP+SWE+CHE+TUR+GBR+USA+COL+CHL+CAN+BEL+AUT+AUS..PS._T._T.?startPeriod=2022&endPeriod=2022&dimensionAtObservation=AllDimensions)

<img width="1009" height="867" alt="image" src="https://github.com/user-attachments/assets/f513e24f-54e3-45c3-8683-23293ba0dd93" />


İlk bakışta basit görünüyor, ama bunu biçimselleştirmemiz gerekiyor.

---

## Adım 2 – Kavramları belirle

- `Country` → REF_AREA  
- `Year` → TIME_PERIOD  
- `Sex` → SEX  
- `Value` → OBS_VALUE  

Artık hangi parçaların **boyut**, hangisinin **ölçü** olduğunu biliyoruz.

---

## Adım 3 – Küresel kavramlarla kontrol et

- `REF_AREA` → zaten alanlar arası (cross-domain) bir kavram  
- `TIME_PERIOD` → alanlar arası, format frekansa uygun olmalı  
- `SEX` → küresel değil, ama demografi alanına özgü  
- `OBS_VALUE` → standart ölçü kavramı  

İpucu: Her zaman **küresel kavramlardan başla**; yoksa yerel tanımla.

---

## Adım 4 – Kod listelerini ata

- `REF_AREA` → ISO 3166 (TR, FR, vb.)  
- `TIME_PERIOD` → YYYY, YYYY-Qn, YYYY-MM (frekansa göre)  
- `SEX` → CL_SEX (F, M, T) – bunu yerel tanımlamamız gerekiyor  
- `OBS_VALUE` → kod listesi yok (sayısal değer)

---

## Adım 5 – DSD’yi oluştur

Eşlemeden:

- **Boyutlar:** REF_AREA, TIME_PERIOD, SEX  
- **Ölçü:** OBS_VALUE  
- **Öznitelikler:** UNIT_MEASURE (örn. Kişi)  

Artık yapıyı resmî olarak tanımlayabiliriz.

---

## Adım 6 – Veri Akışını tanımla

Son olarak, DSD’yi bir Dataflow içine saralım, örneğin:

- **ID:** DF_POP_SIMPLE  
- **Açıklama:** Ülke, cinsiyet ve yıla göre yerleşik nüfus  
- **Kapsam:** 2015–günümüz  
- **Güncelleme:** Yıllık  

---

## Örnek: Tam eşleme

| Tablo Sütunu | Kavram ID    | Tür        | Kod Listesi      |
|--------------|--------------|------------|------------------|
| Country      | REF_AREA     | Boyut      | CL_AREA (ISO)    |
| Year         | TIME_PERIOD  | Boyut      | Zaman formatları |
| Sex          | SEX          | Boyut      | CL_SEX           |
| Value        | OBS_VALUE    | Ölçü       | –                |
| –            | UNIT_MEASURE | Öznitelik  | CL_UNIT          |

---

## Uygulamalı Örnek: Historical Population Data

Aşağıdaki tabloyu düşünelim (2022 nüfus değerleri, “Persons” biriminde):

| Reference area | Population (2022) |
|----------------|-------------------|
| Australia      | 26 014 399        |
| Austria        | 9 058 407         |
| Belgium        | 11 640 788        |
| Canada         | 38 935 934        |
| …              | …                 |

### 1. Kavramlar
- `Reference area` → REF_AREA  
- `Time period` → TIME_PERIOD (2022)  
- `Indicator` → INDICATOR (Population)  
- `Unit` → UNIT_MEASURE (Persons)  
- `Value` → OBS_VALUE  

### 2. Global kontrol
- REF_AREA → CL_AREA (ISO kodları: AU, AT, BE, …)  
- TIME_PERIOD → YYYY = 2022  
- UNIT_MEASURE → CL_UNIT (PERS)  
- INDICATOR → CL_IND (POP)  
- OBS_VALUE → sayısal değer  

### 3. DSD Taslağı
- **Boyutlar:** REF_AREA, TIME_PERIOD, INDICATOR  
- **Ölçü:** OBS_VALUE  
- **Öznitelikler:** UNIT_MEASURE  

### 4. Dataflow
- **ID:** DF_POP_HIST  
- **Açıklama:** Ülkelere göre 2022 tarihi nüfus verisi  
- **DSD:** DSD_POP  
- **Kapsam:** 2022, tüm ülkeler  
- **Güncelleme:** Tek seferlik (historical snapshot)  

---

## 🔑 Pratik ipuçları

- **Fazla modelleme yapmayın.** Kaynak tablodaki her sütun boyut olmak zorunda değil. Sadece analiz için anlamlı olanları tutun.  
- **Küçük başlayın.** Önce birkaç satırla eşlemeyi test edin.  
- **Eski kodlar mı var?** Her zaman küresel kodlara eşleme sağlayın.  
- **Yeniden kullanılabilirliği düşünün.** Başka bir veri seti aynı “Cinsiyet” ayrımını kullanıyorsa, aynı CL_SEX’i yeniden kullanın.  
- **Varsayımları belgeleyin.** Gelecekte mutlaka “neden böyle modellediniz?” diye sorulacaktır.  

---

## Kısaca (TL;DR)

- Ham tablonuzla başlayın.  
- Her sütunu bir SDMX kavramına eşleyin (önce küresel, gerekirse yerel).  
- Kod listelerini ekleyin.  
- DSD’yi kurun.  
- Veri Akışı olarak yayınlayın.  

Bu sayede, ister karmaşık ister dağınık olsun, herhangi bir tabloyu SDMX uyumlu bir modele dönüştürebilirsiniz.
