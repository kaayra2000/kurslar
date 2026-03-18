# Bilgisayarlı Görü
### Makineler Dünyayı Nasıl Görür?

---

# Bugün Ne Öğreneceğiz?

- Bilgisayarlı görü nedir?
- Görüntü işlemenin temelleri
- Özellik çıkarımı ve nesne tanıma
- CNN'den Vision Transformer'a
- Çağdaş modeller ve mimariler
- OCR: Belgelerden metin çıkarma
- Gerçek hayat uygulama alanları

---

# Bilgisayarlı Görü Nedir?

> Makinelerin dijital görüntü ve videolardan anlamlı bilgi çıkarmasını sağlayan yapay zeka dalı

- Görüntü işleme → pikselleri dönüştürür
- Bilgisayarlı görü → pikselleri **anlar**
- Makine öğrenimi ile birlikte çalışır

---

# Kısa Tarihçe

| Yıl | Olay |
|-----|------|
| 1960'lar | İlk görüntü işleme deneyleri |
| 1980'ler | Kenar tespiti algoritmaları |
| 2012 | AlexNet → Derin öğrenme devrimi |
| 2016 | YOLO → Gerçek zamanlı tespit |
| Günümüz | Otonom araçlar, tıbbi AI |

---

# Görüntü Nedir? (Makine Gözüyle)

- Her görüntü bir **sayı matrisi**dir
- Her piksel: 0–255 arası değer
- Renkli görüntü: 3 kanal (R, G, B)
- 1920×1080 görüntü = ~6 milyon sayı

---

# Görüntü İşlemenin Temelleri

**Filtreleme**
- Gaussian Blur → gürültü azaltma
- Keskinleştirme → detay artırma

**Kenar Tespiti**
- Sobel → yatay/dikey kenarlar
- Canny → hassas kenar haritası

**Renk Uzayları**
- RGB → ekran gösterimi
- HSV → renk bazlı filtreleme
- Grayscale → hesaplama kolaylığı

---

# Temel Görevler

| Görev | Ne Yapar? | Örnek |
|-------|-----------|-------|
| Sınıflandırma | "Bu nedir?" | Kedi mi, köpek mi? |
| Nesne Tespiti | "Nerede?" | Arabalar nerede? |
| Segmentasyon | "Hangi piksel?" | Yol / bina / insan |

---

# Geleneksel → Derin Öğrenme

**Geleneksel Yöntemler**
- SIFT, SURF, HOG
- Elle tasarlanmış özellikler
- Sınırlı genelleme

**CNN Tabanlı Yaklaşım**
- Özellikler otomatik öğrenilir
- Çok daha yüksek doğruluk
- Büyük veri gerektirir

---

# CNN Mimarileri (2012–2017)

| Model | Yıl | Katkısı |
|-------|-----|---------|
| AlexNet | 2012 | CNN devriminin başlangıcı |
| VGGNet | 2014 | Derin ve sade mimari |
| ResNet | 2015 | Skip connection ile çok derin ağlar |
| YOLO | 2016 | Gerçek zamanlı nesne tespiti |
| Mask R-CNN | 2017 | Instance segmentation |

---

# Transformer Nedir?

- 2017'de NLP için geliştirildi ("Attention is All You Need")
- **Self-attention** mekanizması: her token diğerleriyle ilişki kurar
- CNN'den farkı: yerel değil **global bağlam** görür
- Görüntüye uyarlanması → **Vision Transformer (ViT)**

---

# Vision Transformer (ViT)

- Görüntü küçük **patch**'lere bölünür (ör. 16×16 piksel)
- Her patch bir token gibi işlenir
- Transformer encoder ile işlenir
- Yeterli veriyle CNN'i geçer

| Özellik | CNN | ViT |
|---------|-----|-----|
| Bağlam | Yerel | Global |
| Az veri | ✅ İyi | ❌ Zayıf |
| Çok veri | ✅ İyi | ✅ Daha iyi |
| Yorumlanabilirlik | Zor | Attention map ile kolay |

---

# Çağdaş Mimariler (2020+)

| Model | Yıl | Katkısı |
|-------|-----|---------|
| ViT | 2020 | Transformer'ı görüntüye uyarladı |
| Swin Transformer | 2021 | Hiyerarşik ViT, daha verimli |
| CLIP | 2021 | Görüntü + metin birlikte öğrenir |
| SAM | 2023 | Her şeyi segmente eder |
| YOLOv8/v11 | 2023+ | Gerçek zamanlı SOTA tespit |
| DeepSeek-OCR-2 | 2025 | Belge OCR, formül ve tablo desteği |

---

# CLIP: Görüntü + Dil

- OpenAI tarafından geliştirildi (2021)
- 400 milyon görüntü-metin çiftiyle eğitildi
- "Bir kedi fotoğrafı" yazınca doğru görseli bulur
- **Sıfır-atış (zero-shot)** sınıflandırma yapabilir
- Stable Diffusion, DALL-E gibi modellerin temeli

---

# SAM: Segment Anything Model

- Meta AI tarafından geliştirildi (2023)
- Herhangi bir nesneyi, herhangi bir görüntüde segmente eder
- Nokta, kutu veya metin ile yönlendirilebilir
- 1 milyar+ maske ile eğitildi
- Tıbbi görüntü, uydu fotoğrafı, video analizinde kullanılıyor

---

# DeepSeek-OCR-2

- DeepSeek tarafından geliştirildi (2025)
- Belge görüntülerini **düz metin veya Markdown**'a dönüştürür
- **Visual Causal Flow** adlı insan benzeri görsel kodlama kullanır
- Çok dilli destek (multilingual)

**Öne Çıkan Yetenekler**
- 📐 Matematiksel formüller
- 📊 Tablolar
- 📄 Çok sütunlu karmaşık belgeler

**olmOCR-bench Sonuçları**

| Test | Skor |
|------|------|
| Genel | 76.30 |
| Uzun/Küçük Metin | 90.70 |
| Arxiv Matematik | 82.00 |
| Çok Sütunlu | 79.00 |
| Tablo | 77.40 |
| Eski Tarama Matematik | 72.00 |
| Düşük Kalite Eski Tarama | 33.80 |

---

# Uygulama Alanları

- 🚗 **Otonom Araçlar** — şerit takibi, nesne algılama
- 🏥 **Tıbbi Görüntü** — X-ray, MRI analizi
- 🎭 **Artırılmış Gerçeklik** — yüz filtreleri
- 🏭 **Kalite Kontrol** — üretim hattı hata tespiti
- 🔒 **Güvenlik** — yüz tanıma, hareket algılama

---

