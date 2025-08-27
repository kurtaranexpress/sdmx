# 07 – Postman ile Sorgulama ve Test

## Neden Postman?

Postman, API’leri test etmek için basit ama güçlü bir araçtır.  
SDMX servisleri RESTful uç noktalar olduğu için Postman ile:

- Kod yazmadan sorgular oluşturup gönderebilirsiniz  
- Yanıtları JSON, XML veya CSV formatında inceleyebilirsiniz  
- Parametreleri ve anahtarları, üretimde kullanmadan önce doğrulayabilirsiniz  
- Örnekleri meslektaşlarınız veya veri sağlayıcılarla paylaşabilirsiniz  

---

## Postman’de temel bir SDMX isteği

1. Postman’i açın  
2. Yeni bir `GET` isteği oluşturun  
3. Uç noktayı yapıştırın, örneğin:  (https://example.org/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP.F?startPeriod=2024)
4. **Send** butonuna tıklayın  
5. JSON yanıtını alt panelde inceleyin  

---

## Sorgu parametrelerini kullanmak

Yaygın SDMX sorgu parametreleri:

- `startPeriod` → dahil edilecek ilk dönem  
- `endPeriod` → dahil edilecek son dönem  
- `dimensionAtObservation` → boyutların seri ya da gözlem seviyesinde görünüp görünmeyeceğini belirler  
- `detail` → ne kadar metadata dahil edileceğini kontrol eder (örn. `full`, `dataonly`)  

Örnek:  GET (https://example.org/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP?startPeriod=2020&endPeriod=2024&detail=full)

---

## Postman ile doğrulama kontrolü

- Yanlış bir kodla sorgu gönderin (örn. `SEX=X`) → sunucu hata döndürmelidir.  
- `startPeriod` değerinin frekansla eşleştiğini kontrol edin (`YYYY` yıllık, `YYYY-MM` aylık için).  
- Yanıt başlıklarını inceleyin → içerik tipi `application/vnd.sdmx.data+json` olmalıdır.  

---

## Koleksiyonları paylaşmak

Postman, sorguları **Collection** olarak kaydetmenizi ve paylaşmanızı sağlar.  
- `SDMX Examples` adında bir koleksiyon oluşturun  
- Nüfus, TÜFE, GSYH vb. sorguları ekleyin  
- Koleksiyon JSON dosyasını ekibinizle paylaşın, onlar da içe aktararak aynı sorguları çalıştırabilir  

---

## 🔑 Pratik ipuçları

- Yeni Dataflow’ları duyurmadan önce her zaman Postman’de test edin.  
- “Altın örnekler” (her zaman çalışan sorgular) saklayın, gelecekte değişiklikleri doğrulamak için kullanın.  
- Postman’de ortam değişkenleri (`{{baseUrl}}`, `{{apiKey}}`) kullanarak sunucular arasında kolayca geçiş yapın.  
- Yanıt sürelerini kontrol edin — büyük sorgular filtreleme veya daha küçük kapsam gerektirebilir.  

---

## Kısaca (TL;DR)

- Postman, **SDMX API’lerini keşfetmek ve test etmek** için idealdir.  
- Basit başlayın, sonra parametrelerle sorguları daraltın.  
- Koleksiyonları ekibinizle paylaşarak tutarlı testler yapın.  
- Uygulamalara sorgu gömmeden önce Postman’i **ilk doğrulama adımı** olarak kullanın.  

---

[Sonraki Bölüm – Tablo Üzerinden Modelleme](https://github.com/kurtaranexpress/sdmx/blob/main/guides/tr/08-%20TablodanModelleme.md)

