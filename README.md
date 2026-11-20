# Kolay Fatura: Ön Muhasebe SaaS

Türkiye'deki küçük işletmeler için; Vergi Usul Kanunu ve GİB e-Belge düzenlemelerine uyumlu, abonelik modeliyle satılmak üzere tasarlanmış çok kiracılı (multi-tenant) ön muhasebe uygulaması.

> Bu depo bir proje vitrinidir. Kaynak kod paylaşılmamaktadır.

## Önce mimari

Kodlamaya başlamadan önce 11 mimari doküman hazırlandı: sistem mimarisi, modül listesi, ER diyagramı, tenant izolasyonu, belge yaşam döngüsü, e-Belge entegratör adaptörü, abonelik ve ödeme akışı, **güvenlik tehdit modeli**, fazlı geliştirme planı, riskler ve operasyon kılavuzu (yedekleme/DR, izleme, pentest hazırlığı).

## Tamamlanan fazlar

**Faz 1: Temel SaaS**
- Kayıt, e-posta doğrulama, refresh token rotasyonu ve **yeniden kullanım tespiti**, opsiyonel TOTP 2FA, oturum yönetimi
- **Üç katmanlı tenant izolasyonu:** PostgreSQL Row Level Security + ORM düzeyinde kapsam + uygulama kontrolleri
- Modül × işlem bazlı izin matrisi, hazır ve özel roller
- Plan, paket ve abonelik altyapısı; paket limitlerinin zorlanması
- Ödeme ve e-Belge sağlayıcıları için adaptör deseni, idempotent webhook işleme
- Değiştirilemez (immutable) denetim kaydı, Türkçe hata mesajı + referans kodu

**Faz 2: Temel ön muhasebe**
- Müşteri, tedarikçi ve ürün kartları
- Satış ve alış faturaları, teklif, sipariş, irsaliye
- Stok takibi ve düşük stok uyarıları

**Faz 3 (devam ediyor):** e-Fatura / e-Arşiv / e-İrsaliye kuyruk ve worker hattı

## Teknolojiler

`TypeScript` · `NestJS` · `Prisma` · `PostgreSQL (RLS)` · `Redis` · `BullMQ` · `React` · `TanStack Query` · `Zod` · `UBL-TR` · `S3` · `Docker` · monorepo (hesaplama motoru, e-Belge ve ödeme sağlayıcı paketleri ayrı)
