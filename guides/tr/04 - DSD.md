# 04 – Veri Yapısı Tanımı (DSD)

## DSD nedir?

**Data Structure Definition (DSD)** veri setinizin **mimari planıdır**.  
Bize şunları söyler:
- Hangi **kavramlar** boyut olarak kullanılır  
- Hangi kavram **ölçü (measure)** olarak alınır (asıl değer)  
- Hangi kavramlar **özelliktir** (ek bilgiler)  
- Her boyut/özellik hangi **kod listesi** ile bağlıdır  

Kısaca:  
**Kavram = dil → Kod listesi = kelime hazinesi → DSD = dil bilgisi**

---

## Boyutlar, Ölçü, özellikler

- **Boyutlar (Dimensions)**  
  Gözlemin *nerede, ne zaman, neye* ait olduğunu tanımlar.  
  Birlikte **seri anahtarını** oluştururlar.  
  Örnek: `REF_AREA`, `TIME_PERIOD`, `FREQ`, `INDICATOR`, `SEX`.

- **Ölçü (Measure)**  
  Asıl veri değeridir.  
  SDMX’te genellikle `OBS_VALUE` adını alır.  
  Örnek: `9.000.000` (2025 yılında İstanbul kadın nüfusu).

- **özellikler (Attributes)**  
  Gözlem veya seriye ek bilgi sağlar.  
  Örnek: `UNIT_MEASURE` = “Kişi”.

---

## Örnek DSD: Nüfus

### Boyutlar
| Pozisyon | Kavram ID    | Kod listesi | Örnek değerler                |
|----------|--------------|-------------|-------------------------------|
| 1        | FREQ         | CL_FREQ     | A, Q, M                       |
| 2        | REF_AREA     | CL_AREA     | TR, FR, IST (yerel kod ise)   |
| 3        | TIME_PERIOD  | (zaman formatı) | 2025, 2025-Q1, 2025-01     |
| 4        | INDICATOR    | CL_IND      | POP                           |
| 5        | SEX          | CL_SEX      | F, M, T                       |

### Ölçü
| Kavram ID | Açıklama                      |
|-----------|-------------------------------|
| OBS_VALUE | Sayısal değer (örn. 82.000.000) |

### özellikler
| Kavram ID     | Kod listesi | Örnek değerler |
|---------------|-------------|----------------|
| UNIT_MEASURE  | CL_UNIT     | PERS, MILP     |

---

## DSD nasıl doğrulama sağlar?

Her boyut/özellik bir kod listesiyle bağlı olduğu için:
- Sadece geçerli kodlar kullanılabilir.  
- Sistemler tutarlılığı kontrol edebilir (örn. `M` frekansı `YYYY-MM` formatı gerektirir).  
- `UNIT_MEASURE` gibi özellikler veri setleri arasında netlik sağlar.  

---

## Örnek seri anahtarı

Gözlem: “2025 yılında İstanbul’un kadın nüfusu = 9 milyon kişi”  

Seri anahtarı (sadece boyutlar):  
`FREQ=M • REF_AREA=IST • TIME_PERIOD=2025-01 • INDICATOR=POP • SEX=F`

Ölçü:  
`OBS_VALUE = 9.000.000`

özellik:  
`UNIT_MEASURE = PERS`

---

## İyi uygulama notları

- **Boyut sırası önemlidir** → DSD’de tanımlanır ve anahtarlarda kullanılır.  
- **DimensionAtObservation** parametresi boyutların sorgularda nasıl görüneceğini belirler (flat vs nested).  
- **DSD’leri sabit tutun** → boyut sırasını veya kod listesi bağlantılarını değiştirmek karşılaştırılabilirliği bozar.  
- **DSD’nizi belgeleyin** → herkesin anlayacağı kısa bir not yayınlayın.  

---

## 🔎 Basit benzetme: DSD = Excel tablosu

Veri setinizi bir Excel tablosu gibi düşünün:

| Ülke    | Yıl  | Cinsiyet | Gösterge | Değer     | Birim   |
|---------|------|----------|-----------|-----------|---------|
| Türkiye | 2025 | F        | POP       | 9.000.000 | Kişi    |

- **Boyutlar = gözlemi tanımlayan sütunlar** (Ülke, Yıl, Cinsiyet, Gösterge)  
- **Ölçü = asıl değer sütunu** (Değer)  
- **özellikler = ek bilgiler** (Birim)  

DSD, bu tablonun **resmî tanımıdır**.

---

## 💡 Yeni başlayanlar için SSS

**S: Neden “ölçü” ile “boyutları” ayırıyoruz?**  
C: Çünkü ölçü analiz etmek istediğimiz sayıdır. Boyutlar ise bu sayıyı açıklayan etiketlerdir.  

**S: Birden fazla ölçü olabilir mi?**  
C: Genelde SDMX’te hayır. Daha iyi yöntem: tek ölçü (`OBS_VALUE`), farklı değişkenleri (örn. nüfus & GSYH) **indikator** olarak modellemek.  

**S: Bir özellik (örn. Birim) unutulursa ne olur?**  
C: Kullanıcılar değeri yanlış yorumlar (örn. “9” → 9 kişi mi, 9 bin mi, 9 milyon mu?). Birimleri her zaman açık verin.  

---

## 🧩 Küçük egzersiz

Şu cümleyi DSD terimleriyle tanımlamaya çalışın:

**“Fransa’nın 2024 yılı GSYH’si (yıllık, cari fiyatlarla) 3.200 milyar EUR’dur.”**

- Boyutlar: `REF_AREA=FR`, `TIME_PERIOD=2024`, `FREQ=A`, `INDICATOR=GDP`  
- Ölçü: `OBS_VALUE=3.200.000.000.000`  
- özellikler: `UNIT_MEASURE=EUR`, `PRICE_TYPE=CURRENT`  

---

## Kısaca (TL;DR)

- DSD, verinin nasıl yapılandığının **resmî tanımıdır**.  
- Kavramları ve kod listelerini birleştirerek **boyut, ölçü, özellik** seti oluşturur.  
- Doğrulama sağlar, sorgulara imkân verir ve veri setinizi küresel ölçekte anlaşılır hale getirir.  

---

👉 [Sonraki Bölüm: Veri Akışı (Dataflow)](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/05%20-%20Veri%20Akışı.md)
