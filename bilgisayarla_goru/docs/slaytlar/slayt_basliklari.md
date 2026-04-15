# Bilgisayarlı Görü
### Makineler Dünyayı Nasıl Görür?

---

# Bugün Ne Öğreneceğiz?

- Bilgisayarlı görü nedir?
- Görüntü işlemenin temelleri
- Özellik çıkarımı ve nesne tanıma
- CNN'den Vision Transformer'a
- Çağdaş modeller ve mimariler (SOTA 2026)
- OCR: Belgeleri anlamlandırma
- Gerçek hayat uygulama alanları

---

# Bilgisayarlı Görü Nedir?

> Makinelerin dijital görüntü ve videolardan anlamlı bilgi çıkarmasını sağlayan yapay zeka dalı

- Görüntü işleme → pikselleri dönüştürür (Girdi: Görsel, Çıktı: Görsel)
- Bilgisayarlı görü → pikselleri **anlar** (Girdi: Görsel, Çıktı: Anlam/Veri)
- Çok modlu (multimodal) yapay zeka ile metin ve sesi birleştirir

---

# Kısa Tarihçe

| Yıl | Olay |
|-----|------|
| 1960'lar | İlk görüntü işleme deneyleri |
| 2012 | AlexNet → Derin öğrenme devrimi |
| 2020 | ViT → Transformer dönemi |
| 2023 | SAM → "Segment Anything" (Her şeyi bölütle) |
| 2025 | DeepSeek-VL2 / GPT-5-V → Multimodal zeka |
| **2026** | **YOLO26 & SAM 3** → Uç cihazlarda SOTA performans |

---

# Görüntü Nedir? (Makine Gözüyle)

- Her görüntü bir **sayı matrisi**dir
- Her piksel: 0–255 arası değer
- Renkli görüntü: 3 kanal (R, G, B)
- 4K Görüntü = ~25 milyon sayı (makine için devasa bir veri kümesi)

---

# Görüntü İşlemenin Temelleri



**Filtreleme**
- Gaussian Blur → gürültü azaltma
- Bilateral Filter → kenarları koruyarak yumuşatma

**Kenar Tespiti**
- Sobel → gradyan bazlı kenarlar
- Canny → modern standart, hassas kenar haritası

**Renk Uzayları**
- RGB / HSV / Grayscale
- LAB → insan gözüne en yakın algısal renk uzayı

---

# Temel Görevler

| Görev | Ne Yapar? | Örnek |
|-------|-----------|-------|
| Sınıflandırma | "Bu nedir?" | Röntgen bulgusu: Zatürre |
| Nesne Tespiti | "Nerede?" | Otonom sürüş: Yaya tespiti |
| Segmentasyon | "Hangi piksel?" | SAM 3 ile tıbbi görüntü bölütleme |

---

# Geleneksel → Derin Öğrenme

**Geleneksel Yöntemler** (SIFT, HOG)
- Elle tasarlanmış özellikler (Hand-crafted)
- Sınırlı genelleme, düşük işlem gücü

**Modern Yaklaşım** (Foundation Models)
- Özellikler milyarlarca veriyle kendi kendine öğrenilir
- **Sıfır-atış (zero-shot)** yeteneği: Hiç görmediği nesneyi tanıyabilir

---

# CNN ve Transformer Mimarileri

| Model | Öne Çıkan Özellik |
|-------|-------------------|
| **ResNet** | Skip connections (Derin ağların temel taşı) |
| **YOLO26** | 2026'nın en hızlısı; NMS-free ve CPU üzerinde %43 daha hızlı (YOLO11-N'a göre) |
| **DINOv2** | Kendi kendine öğrenen (Self-supervised) güçlü görsel özellikler |
| **Swin-T** | Hiyerarşik Transformer; pikselleri gruplandırarak işler |

---

# Vision Transformer (ViT) ve Ötesi

- Görüntü küçük **patch**'lere bölünür (ör. 14×14 piksel)
- **Self-attention** mekanizması ile pikseller arası uzun mesafe ilişkileri kurulur
- CNN'den farkı: Görüntünün bir köşesindeki bilgiyle diğer köşesini aynı anda ilişkilendirir (**Global Bağlam**)

| Özellik | CNN | ViT (2026 Standartları) |
|---------|-----|-----|
| Bağlam | Yerel (Piksel komşuluğu) | Global (Tüm görüntü) |
| Veri | Orta düzey veriyle verimli | Dev veri setleriyle (JFT-4B) kusursuz |
| Uygulama | Mobil ve hafif cihazlar | Bulut tabanlı ağır analizler |

---

# Çağdaş Mimariler (2024–2026)

| Model | Yıl | Katkısı |
|-------|-----|---------|
| **SAM 3** | 2026 | Video ve 3D sahnelerde anlık "prompt" ile bölütleme |
| **GPT-5-V** | 2025 | Görsel akıl yürütmede insan seviyesi |
| **Gemini 3** | 2026 | 10+ saatlik videoyu saniyeler içinde analiz etme |
| **YOLO26** | 2026 | MuSGD optimizasyonu ile uç cihazlarda milisaniye hızında tespit |
| **RF-DETR** | 2025 | Transformer tabanlı gerçek zamanlı nesne tespiti (SOTA) |

---

# CLIP ve Çok Modlu Öğrenme

- Görüntü ve metni aynı uzayda birleştirir
- "Karda oynayan altın retriever" metniyle ilgili pikselleri eşleştirir
- **Zero-shot** sınıflandırma: Hiç eğitilmediği bir sınıfı (ör. "nadir bir çiçek") sadece ismini bilerek bulabilir

---

# SAM 3: Segment Anything

- Meta AI tarafından 2026 başında güncellendi
- **Video desteği:** Hareketli nesneleri video boyunca takip ederek segmente eder
- **Cihaz üzerinde (On-device):** Artık mobil işlemcilerde bile çalışabiliyor
- Tıbbi analizlerden AR/VR dünyasına kadar temel altyapı haline geldi

---

# OCR: DeepSeek-OCR-2 & Gemini 3

Artık sadece harf okumuyoruz, **anlam çıkarıyoruz**.

- **DeepSeek-OCR-2 (2025):** Görsel veriyi doğrudan Markdown/LaTeX'e çevirir.
- **Yetenekler:** Karmaşık tablolar, 3D grafikler ve el yazısı formüller.
---

# Uygulama Alanları (2026 Vizyonu)

- 🚗 **Otonom Sistemler** — End-to-end sürüş (direkt görüntüden direksiyon hamlesine)
- 🏥 **Hassas Tıp** — AI tabanlı anlık cerrahi asistanlık ve kanser erken teşhisi
- 👓 **Spatial Computing** — Karma gerçeklik (Apple Vision Pro/Quest 4) ortam algılama
- 🤖 **İnsansı Robotlar** — Nesneleri tanıma, kavrama ve çevresel navigasyon (Physical AI)
- 🏭 **Akıllı Üretim** — Sıfır hata ile üretim bantlarının 7/24 görsel denetimi

---