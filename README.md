<h1 align="center">Yaşarlar 24 Manitou Kiralama</h1>

<p align="center">
  Gerçek bir işletme için sıfırdan tasarlayıp geliştirdiğim, canlıda çalışan web sitesi.<br>
  İnteraktif hizmet haritası, otomatik yorum moderasyonu, yönetim paneli ve teknik SEO.
</p>

<p align="center">
  <a href="https://yasarlar24manitoukiralama.com"><b>▶ Canlı siteyi aç</b></a>
</p>

---

## Proje hakkında

İstanbul Anadolu Yakası'nın tamamına hizmet veren bir Manitou teleskopik
yükleyici kiralama işletmesinin web sitesi. "Bir esnaf için basit bir tanıtım
sitesi" fikriyle başladı; işletme sahibinin geri bildirimleriyle, fiyat sorgusu,
müşteri yorumları, hizmet bölgesi bilgisi ve ziyaret analizini tek yerde sunan
bir siteye dönüştü.

> Bu depo kaynak kodu değil, projenin mimarisini ve özelliklerini tanıtır.
> Kaynak kod, müşteri verisi ve altyapı güvenliği nedeniyle özel bir depoda tutuluyor.

## Özellikler

| | |
|---|---|
| **İnteraktif hizmet haritası** | Gerçek ilçe sınırlarına dayalı SVG harita; ilçeye tıklayınca bölgeye özel fiyat bilgisi açılır |
| **İlçe sayfaları** | Pendik, Tuzla, Kartal, Maltepe ve diğer bölgeler için ayrı tanıtım sayfaları |
| **Otomatik yorum moderasyonu** | Yorumlar yayınlanmadan önce sunucuda küfür, bağlantı, telefon ve reklam filtresinden geçer |
| **Yönetim paneli** | Yalnız işletme sahibinin girebildiği panel: ziyaretçi ve yorum istatistikleri, günlük rapor |
| **Yapay zekâ destekli günlük rapor** | Seçilen günün trafiği özetlenir; gerçek ziyaretçiler botlardan ayrılır, Türkçe yorum üretilir |
| **Teknik SEO** | Yapılandırılmış veri, site haritası, Open Graph etiketleri, Search Console ve Business Profile bağlantısı |
| **Mobil uyumlu arayüz** | Framework kullanmadan yazıldı; özel menü, dokunmatik etkileşimler, ekran boyutuna göre düzen |

## Nasıl çalışıyor?

### Yorum moderasyonu

```
Ziyaretçi yorum gönderir
        ↓
Firestore'a "pending" durumunda kaydedilir
        ↓
Cloud Function kendiliğinden tetiklenir (onDocumentCreated)
        ↓
Anahtar kelime ve spam filtresi çalışır
        ↓
Durum güncellenir: approved / rejected
        ↓
Sitede yalnızca "approved" yorumlar listelenir
```

İşletme sahibi yorumları tek tek kontrol etmek zorunda kalmaz; filtreden geçen
yorum kendiliğinden yayınlanır.

### Hizmet bölgesi haritası

İstanbul ilçe sınırları elle sadeleştirilmiş bir SVG olarak çizildi. Anadolu
Yakası'nın tamamı hizmet bölgesi olarak işaretlidir; ilçeler tıklanabilir,
üzerine gelince ve tıklayınca animasyonlu geri bildirim verir, bölgeye özel
fiyat bilgisi bir kartta açılır. Resmî ilçe olmayan ama önemli bölgeler
(Kaynarca, Kurtköy) haritada ayrı işaretlerle gösterilir.

### Yönetim paneli ve günlük rapor

```
Sayfa açılır → ziyaret kaydedilir (Cloud Function)
        ↓
İşletme sahibi panele giriş yapar ve bir gün seçer
        ↓
O günün ziyaretleri üçe ayrılır: gerçek ziyaretçi / dış bot / altyapı botu
        ↓
Tekil ziyaretçi, bölge, sayfa ve saat dağılımı hesaplanır
        ↓
Google Gemini bu sayılardan Türkçe bir özet rapor yazar
```

Panelde bölgelere göre tekil ziyaretçi, bölgelere göre yorum yoğunluğu, sayfa
dağılımı ve saatlik ziyaret yoğunluğu görüntülenir.

## Kullanılan teknolojiler

| Katman | Teknoloji |
|---|---|
| Arayüz | HTML5, CSS3 ve JavaScript (ES Modules); framework yok |
| Veri ve sunucu | Firebase: Firestore, Cloud Functions v2, Hosting, Authentication |
| Güvenlik | Firestore Security Rules, Secret Manager |
| Yapay zekâ | Google Gemini (günlük trafik özeti) |
| Harita | Elle sadeleştirilmiş SVG (ilçe sınırları) |
| SEO | Schema.org (JSON-LD), robots.txt, sitemap.xml, canonical URL, Open Graph |
| Yayın ve yönetim | Firebase CLI, Google Cloud IAM, Google Cloud Console |

### Öne çıkan teknik işler

- **Moderasyon tamamen sunucuda.** Filtre Cloud Functions'ta çalışır; tarayıcıdan
  atlanamaz ya da değiştirilemez. Ziyaretçi bir yorumun onay durumunu
  değiştiremez, yalnızca "onay bekliyor" olarak yorum ekleyebilir.
- **Bot ayrımı.** Arama motoru tarayıcıları ve barındırma altyapısının kendi
  kontrolleri gerçek ziyaretçilerden ayrılır; istatistikler kirlenmez.
- **Gizli anahtar yönetimi.** Yapay zekâ servisinin anahtarı kodda durmaz;
  Secret Manager'da saklanır ve yalnız ilgili fonksiyona verilir.
- **Yetkili erişim.** Rapor yalnız işletme sahibinin hesabıyla istenebilir;
  kimlik sunucuda doğrulanır.
- **Maliyet kontrolü.** Fonksiyonlar `maxInstances` ile sınırlandı ve
  `europe-west1` bölgesinde çalışıyor.
- **Canlıya alma süreci.** Firebase Blaze planına geçiş, Cloud Functions için
  IAM ve Eventarc yapılandırması, alan adı ve DNS yönetimi.

## Durum

Site yayında ve işletme tarafından kullanılıyor; geliştirme sürüyor.

## İletişim

**osmnnuri** · [GitHub](https://github.com/osmnnuri) · osmannuriyasar57@gmail.com
