# 05 – Veri Akışı (Dataflow – Yayınlanmış Veri Seti)

## Veri Akışı nedir?

Bir DSD bize **planı** veya **şemayı** verir, ama tek başına yeterli değildir.  
Kullanıcıya *“işte sorgulayabileceğiniz veri seti bu”* demek için bir **Veri Akışı (Dataflow)** tanımlarız.  

Bir Dataflow şunları belirtir:
- Hangi DSD’ye dayandığı  
- Veri setinin ne amaçla yayınlandığı  
- Hangi zaman dönemlerini ve alanları kapsadığı  
- Ne sıklıkla güncellendiği  
- Açıklama, iletişim ve lisans bilgileri  

Kısaca:  
- **DSD → verinin nasıl yapılandığı**  
- **Dataflow → hangi verinin yayınlandığı**

---

## Neden Veri Akışı’na ihtiyaç var?

- Aynı DSD’den birden fazla ürün yayınlayabilirsiniz (örn. “Yıllık Nüfus” vs “Aylık Nüfus”).  
- Kapsamı açıkça tanımlar (örn. “2015’ten itibaren mevcut, şehir düzeyi dahil”).  
- **Yayın yaşam döngüsünü** DSD’yi bozmadan yönetmenizi sağlar (eski akışı kapat, yeni aç).  

---

## Bir Veri Akışı’nın asgari öğeleri

- **ID:** `DF_POP` (kısa ve sabit)  
- **Ad:** `Nüfus – Aylık`  
- **Açıklama:** `Yerleşik nüfus, aylık`  
- **DSD referansı:** `DSD_POP`  
- **Kapsam:** `2015–günümüz`, `ülkeler + seçili şehirler`  
- **Güncelleme sıklığı:** `Aylık, T+30`  
- **İletişim:** `population-team@example.org`  
- **Lisans:** `CC-BY 4.0`  

---

## Örnek

Nüfus DSD’si (FREQ, REF_AREA, TIME_PERIOD, INDICATOR, SEX → OBS_VALUE) şu şekilde yayınlanabilir:

**Dataflow:** `DF_POP_MONTHLY`  
- **DSD:** `DSD_POP`  
- **Açıklama:** Aylık nüfus verisi  
- **Kapsam:** `FREQ = M`, `INDICATOR = POP`  
- **Zaman:** `2015–günümüz`  
- **İletişim:** `population-team@example.org`  

---

## Kullanıcı için nasıl görünür?

```http
GET {baseUrl}/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP.F?startPeriod=2024
```
---

## Özet Noktalar

### Kullanıcıya Görünüm
- **DF_POP_MONTHLY** = Veri Akışı ID’si  
- **Altındaki yapı** = DSD_POP  
- **Anahtar sırası** = DSD’deki boyutların sırası  

---

### Yaşam Döngüsü Yönetimi
- Bir şey değiştiğinde DSD’yi bozmayın → gerekirse yeni bir **Veri Akışı** açın.  
- Eski akışları `deprecated` olarak işaretleyin ve yenilerine açıkça yönlendirin.  
- Eski notları ve kapsamları arşivleyin ki kullanıcılar geçmişi takip edebilsin.  

---

### Dokümantasyon Kontrol Listesi
- [ ] Basit dilde özet (ne dahil / ne değil)  
- [ ] Boyut sırası ve kod listesi referansları (kısa tablo veya açıklama)  
- [ ] Zaman kapsamı ve güncelleme sıklığı  
- [ ] Bilinen sorunlar (kesintiler, revizyonlar vb.)  
- [ ] İletişim ve lisans  
- [ ] Kopyala–yapıştır örnek sorgu  

---

### Basit Benzetme
- **DSD = tablo şeması**  
- **Dataflow = o şemaya dayalı yayınlanmış görünüm/ürün**  

Aynı şemadan farklı amaçlara yönelik birden fazla Veri Akışı oluşturabilirsiniz.  

---

### 🔑 Pratik İpuçları
- Yılları veya kapsamı ID’ye gömmeyin (`DF_POP_2025` kötü) → ID’leri sabit tutun, detayları açıklamaya yazın.  
- Kullanıcılar filtrelemekte zorlanıyorsa, daha küçük ve anlaşılır akışlara bölün.  
- Aynı kavram için tekrar tekrar DSD yaratmayın → tek DSD, çok Dataflow kullanın.  
- Veri Akışı sayfasında mutlaka **örnek sorgu** verin — bu, birçok destek talebini azaltır.  

---

### Kısaca (TL;DR)
- **DSD = yapı**, **Dataflow = yayın**.  
- Tek bir DSD’den birden fazla Dataflow çıkabilir.  
- Kapsamı net açıklayın, yaşam döngüsünü şeffaf yönetin, kullanıcıya örnek sorgular verin.  

[Gelecek Bölüm - Doğrulama](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/06%20-%20Dogrulama.md)
