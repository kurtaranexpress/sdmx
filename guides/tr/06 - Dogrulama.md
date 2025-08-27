# 06 – Doğrulama

## Neden doğrulamaya ihtiyaç var?

Bir Veri Yapısı Tanımı (DSD) oluşturup veri hazırlamaya başladığımızda her zaman tutarsızlık veya hata riski vardır.  
**Doğrulama (validation)** şu güveni sağlar:

- Her değer tanımlı olduğu kavram ve kod listesiyle tutarlıdır  
- Zorunlu boyutlar her zaman mevcuttur  
- Zaman serisi ve frekans bilgisi beklenen formatı takip eder  
- Değerler doğru veri tipine uyar (örn. tam sayı, ondalık, metin)  

Doğrulama olmadan, veriler gizli hatalarla yayınlanabilir ve bu da güveni ve kullanılabilirliği azaltır.

---

## Tipik doğrulama kontrolleri

1. **Kod listesi tutarlılığı**  
   Her boyut değeri, bağlı olduğu kod listesinde bulunmalıdır.  
   - Örnek: Eğer `SEX` boyutu sadece `M` (Erkek) ve `F` (Kadın) içeriyorsa, `X` geçersizdir.

2. **Zorunlu boyutlar**  
   Tüm gerekli boyutlar anahtar içinde bulunmalıdır.  
   - Örnek: Eğer `TIME_PERIOD` eksikse, gözlem işlenemez.

3. **Değer tipi kontrolleri**  
   Gözlemler DSD’de belirtilen veri tipine uymalıdır.  
   - Örnek: Nüfus değeri tam sayı olmalı, `"on milyon"` gibi metin olmamalı.

4. **Frekans uyumu**  
   Raporlanan dönem, bildirilen frekansa uygun olmalıdır.  
   - Örnek: Aylık bir veri seti (`M`) yıllık bir gözlem (`2025` yerine `2025-01`) içeremez.

---

## Örnek: Geçersiz vs. geçerli kayıt

### Geçersiz
| REF_AREA | SEX | TIME_PERIOD | VALUE   |
|----------|-----|-------------|---------|
| TR       | X   | 2025        | 82M     |

Sorunlar:  
- `X`, SEX kod listesinde yok.  
- `2025` doğru aylık formatta değil (`YYYY-MM` olmalı).  
- `82M` geçerli bir tam sayı değil.  

---

### Geçerli
| REF_AREA | SEX | TIME_PERIOD | VALUE    |
|----------|-----|-------------|----------|
| TR       | M   | 2025-01     | 82000000 |

---

## Doğrulama nasıl yapılır?

Doğrulama farklı seviyelerde yapılabilir:

- **Yerel doğrulama araçları**: Excel kontrolleri, script’ler, veritabanı kısıtları  
- **SDMX doğrulama servisleri**: SDMX Validator veya .Stat Suite’in doğrulama modülleri  
- **Registry tabanlı doğrulama**: Gönderilen verilerin DSD ve registry’deki metadata ile eşleşmesini sağlar  

---

## Pratik ipuçları

- Yayınlamadan önce doğrulamayı her zaman **küçük veri setleriyle** başlatın.  
- **Resmî SDMX doğrulayıcıları** kullanın (kurumlar arası uyumluluk için).  
- Doğrulamayı iş akışına entegre edin (örn. CI/CD pipeline veya ETL süreci).  
- **Hata raporlarını** takip edin ve düzeltme için veri sağlayıcılarla paylaşın.  

---

✅ Doğrulama sadece hataları bulmak değil, aynı zamanda verinizin kurumlar arası **güvenilir, yeniden kullanılabilir ve entegre edilebilir** olmasını garanti etmektir.  

---

[Sonraki Bölüm – Postman](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/07%20-%20Postman.md)
