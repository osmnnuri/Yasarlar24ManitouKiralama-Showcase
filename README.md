# Yaşarlar 24 Manitou Kiralama

**Üretimde çalışan, gerçek bir işletme için geliştirilmiş tam kapsamlı ticari web platformu.**

İstanbul Anadolu Yakası'nda (Pendik, Tuzla, Sultanbeyli, Kaynarca, Kurtköy, Maltepe, Kartal, Ümraniye, Ataşehir, Sancaktepe, Çekmeköy) hizmet veren gerçek bir Manitou teleskopik yükleyici kiralama işletmesi için sıfırdan tasarlayıp geliştirdiğim, halihazırda canlı ortamda çalışan bir web sitesi.

> Bu repo, projenin kaynak kodunu değil, teknik mimarisini ve özelliklerini tanıtan bir **showcase** (tanıtım) reposudur. Kaynak kod, müşteri verisi ve altyapı güvenliği nedeniyle özel (private) bir depoda tutulmaktadır.

🔗 **Canlı site:** https://yasarlar24manitoukiralama.com

---

## Proje Hakkında

Bu proje, "bir esnaf için basit bir tanıtım sitesi" fikrinden başlayıp, gerçek bir işletmenin ihtiyaçlarına göre üretim ortamında çalışan bir platforma dönüştü. Amaç sadece bir web sitesi değil, işletme sahibinin günlük operasyonunu (fiyat sorgusu, müşteri yorumları, hizmet bölgesi bilgisi) kolaylaştıran uçtan uca bir sistem kurmaktı.

## Öne Çıkan Özellikler

### 🗺️ İnteraktif Hizmet Bölgesi Haritası
Gerçek İstanbul ilçe sınırlarına dayalı, elle optimize edilmiş bir SVG harita. Hizmet verilen ilçeler tıklanabilir, hover ve tıklama anında animasyonlu geri bildirim veriyor, bölgeye özel fiyatlandırma bilgisini anlık açılan bir kart üzerinden gösteriyor. Resmî ilçe sayılmayan ama önemli bir bölge olan mahalleler için harita üzerinde ayrı "pin" işaretleri kullanıldı.

### 🛡️ Otomatik İçerik Moderasyonu
Kullanıcıların bıraktığı yorumlar, yayınlanmadan önce sunucu tarafında (Cloud Functions) çalışan bir **anahtar kelime ve spam filtresinden** geçiyor: küfür/argo içeren kelimeler, link/telefon numarası paylaşımı ve tanıtım/reklam kalıpları (indirim, kampanya vb.) otomatik olarak tespit edilip filtreleniyor. Filtreden geçen yorumlar `approved`, geçemeyenler `rejected` durumuna otomatik olarak güncelleniyor.

Bu sayede site sahibi, gelen her yorumu manuel kontrol etmek zorunda kalmadan, sadece uygun içeriğin otomatik olarak yayınlandığı bir sistemle çalışıyor.

### 🔐 Güvenlik Odaklı Mimari
- Firestore Security Rules ile katı veri erişim kontrolü: istemci tarafı asla bir yorumun onay durumunu doğrudan değiştiremiyor, sadece "onay bekliyor" durumunda veri ekleyebiliyor
- Moderasyon mantığı tamamen sunucu tarafında (Cloud Functions) çalışıyor, istemciden manipüle edilemiyor
- Maliyet kontrolü için `maxInstances` sınırlaması ve konum bazlı (europe-west1) fonksiyon dağıtımı

### 🔍 Teknik SEO
- Schema.org (JSON-LD) yapılandırılmış veri: işletme türü, hizmet bölgeleri, çalışma saatleri, fiyat aralığı
- `robots.txt` ve `sitemap.xml`
- Open Graph meta etiketleri ve canonical URL yönetimi
- Google Search Console ve Google Business Profile entegrasyonu

### 📱 Duyarlı (Responsive) Tasarım
Sıfırdan yazılmış, framework kullanmayan (vanilla) mobil uyumlu arayüz; özel hamburger menü, dokunmatik etkileşimler ve farklı ekran boyutlarına göre optimize edilmiş grid yapıları.

---

## Kullanılan Teknolojiler

| Katman | Teknoloji |
|---|---|
| Frontend | HTML5, CSS3 (vanilla, framework yok), JavaScript (ES Modules) |
| Backend / Altyapı | Firebase (Firestore, Cloud Functions v2, Hosting) |
| Güvenlik | Firestore Security Rules |
| Grafik / Harita | Elle optimize edilmiş SVG (ilçe sınırları) |
| DevOps | Firebase CLI, Google Cloud IAM, Google Cloud Console |
| SEO | Schema.org (JSON-LD), Google Search Console |

## Mimari Akış (Yorum Moderasyonu)

```
Kullanıcı yorum gönderir
        ↓
Firestore'a "pending" durumunda kaydedilir
        ↓
Cloud Function otomatik tetiklenir (onDocumentCreated)
        ↓
Anahtar kelime / spam filtresi kontrolü
        ↓
status güncellenir: approved / rejected
        ↓
Yalnızca "approved" yorumlar sitede listelenir
```

---

## Geliştirme Sürecinden Notlar

- Proje, gerçek bir müşterinin (işletme sahibinin) geri bildirimleriyle iteratif olarak şekillendi
- Firebase Blaze planına geçiş, Cloud Functions IAM/Eventarc yapılandırması, Secret Manager entegrasyonu gibi production-grade DevOps adımları uçtan uca deneyimlendi
- `.com.tr` alan adı entegrasyonu ve DNS yönetimi (Natro) süreci yürütüldü

---

*Bu proje aktif olarak geliştirilmeye devam ediyor — sıradaki adımlar arasında yorum moderasyonunu manuel override edebilen, bölgesel talep analizini görselleştiren bir admin paneli bulunuyor.*
