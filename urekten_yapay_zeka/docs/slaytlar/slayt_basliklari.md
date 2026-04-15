# Üretken Yapay Zeka
### Makineler Nasıl Üretken Olur?

---

# Bugün Ne Öğreneceğiz?

- Üretken vs ayırt edici modeller
- Temel mimariler: GAN, VAE, Diffusion
- LLM ve LVM: Dil ve görüntü modelleri
- Metinden görüntü üretme
- Prompt mühendisliği
- Uygulama alanları

---

# Üretken vs Ayırt edici Modeller

| Özellik | Ayırt Edici | Üretken |
|---------|-------------|---------|
| **Amaç** | Sınıflandırma, tahmin | Yeni veri üretme |
| **Öğrendiği** | $P(y|x)$ - Koşullu olasılık | $P(x)$ veya $P(x,y)$ - Birleşik olasılık |
| **Örnek** | CNN, SVM, Logistic Regression | GAN, VAE, Diffusion, Flow |
| **Çıktı** | Etiket, sınıf | Yeni görüntü, metin, ses, video |

---

# GAN: Generative Adversarial Networks

**Yapı:** Generator (Üretici) vs Discriminator (Ayırt Edici)

- İki ağın **rekabetçi eğitimi**
- Generator: sahte veri üretir
- Discriminator: gerçek/sahte ayırt eder
- Denge noktasında: ayırt edilemez kalitede üretim

**Avantajlar:** Keskin, gerçekçi görüntüler  
**Dezavantajlar:** Eğitim zorluğu, mode collapse (mod çökmesi)

---

# VAE: Variational Autoencoders

**Yapı:** Encoder → Latent Space → Decoder

- **Olasılıksal latent uzay** öğrenimi
- Encoder: görüntüyü düşük boyutlu temsile sıkıştırır
- Decoder: latent koddan görüntü yeniden oluşturur
- Latent space'de gezinerek yeni varyasyonlar üretme

**Avantajlar:** Kararlı eğitim, latent manipülasyonu  
**Dezavantajlar:** Bulanık çıktılar

---

# Diffusion Modelleri

**Yapı:** Forward (gürültü ekleme) → Reverse (gürültü çıkarma)

- Adım adım **gürültü temizleme** süreci
- Forward: görüntüye kademeli gürültü ekle
- Reverse: gürültüyü kademeli temizle
- Metin koşullandırması ile yönlendirme (CLIP/T5)

**Avantajlar:** Çok yüksek kalite, yüksek çeşitlilik  
**Dezavantajlar:** Yüksek hesaplama maliyeti (eğitim aşamasında)

**Örnekler:** Stable Diffusion 3.5, Flux.1, DALL-E 3

---

# Diffusion Modelleri: Tarihçe

| Model | Yıl | Katkısı |
|-------|-----|---------|
| DDPM | 2020 | Diffusion temellerini attı |
| DALL-E 2 | 2022 | Yaygın metinden görüntü devrimi |
| SDXL | 2023 | Yüksek çözünürlük, açık kaynak SOTA |
| Flux.1 | 2024 | Rectified Flow, metin yazma başarısı |
| Sora 2 | 2025 | 1 saatlik video üretimi, fizik kurallarına uygun |
| Flux.2 | 2026 | Gerçek zamanlı video-to-video ve 8K fotorealizm |

---

# LLM: Large Language Models

**Büyük Dil Modelleri** — trilyonlarca parametre ile akıl yürütme ve metin üretimi

| Model | Geliştirici | Parametre | Özellik |
|-------|-------------|-----------|----------|
| **GPT-5.4** | OpenAI | ~10T+ | AGI eşiği, üst düzey akıl yürütme |
| **Claude 4.6 Opus** | Anthropic | Bilinmiyor | Duygusal zeka ve en güvenli kodlama |
| **Gemini 3.1 Pro** | Google | ~5T+ | 10M+ token bağlam, yerleşik multimodal |
| **Llama 4** | Meta | 400B | En güçlü açık kaynak, yerleşik tool-use |
| **DeepSeek-V4** | DeepSeek | 800B+ | İleri düzey matematik ve verimlilik (MoE) |

**Çalışma Prensibi:** Transformer + Next-Token Prediction (Sıradaki kelime tahmini)

---

# LVM: Large Vision Models

**Büyük Görüntü Modelleri** — görüntü anlama, analiz ve video üretimi

**Multimodal LVM'ler (Anlama + Üretim)**

| Model | Geliştirici | Yetenek |
|-------|-------------|----------|
| **GPT-4o** | OpenAI | Gecikmesiz ses/video/görüntü etkileşimi |
| **Claude 4.6 Sonnet** | Anthropic | Karmaşık şema analizi ve teknik UI üretimi |
| **Gemini 3.1 Pro** | Google | 10 saate kadar videoları saniyeler içinde anlama |
| **Sora / Veo 2** | OpenAI/Google | Dakikalarca süren, fizik kurallarına uygun video üretimi |

---

# Transformer Tabanlı Üretken Modeller

**GPT Ailesi (Metin)**
- GPT-5 serisi: Karmaşık planlama ve otonom görevler.
- Autoregressive: kelime kelime üretim.

**Claude Ailesi (Anthropic)**
- Claude 4.6 Opus, Sonnet, Haiku.
- "Constitutional AI" ile insan değerlerine en yakın modeller.
- Çok düşük halüsinasyon oranı.

**Vision Transformer Üretken Modelleri**
- **GPT-5**: OpenAI'ın en gelişmiş multimodal modeli.
- **Imagen 3**: Google'ın en gelişmiş metin-görüntü modeli.
- **Stable Diffusion 3.5**: Çoklu konu (multi-subject) yönetiminde devrim.

---

# CLIP: Görüntü-Metin Köprüsü

- OpenAI tarafından geliştirildi, modern modellerde evrildi.
- Milyarlarca görüntü-metin çiftiyle eğitildi.
- Görüntü ve metni **aynı embedding uzayına** taşır.
- Diffusion modellerinin "gözü" ve "kulağı"dır.

**Kullanım Alanları**
- Sıfır örnekli (Zero-shot) sınıflandırma.
- Metinle görsel arama ve filtreleme.
- Üretken modellerde prompt'un içeriğe dönüştürülmesi.

---

# Stable Diffusion / Flux Mimarisi

**3 Ana Bileşen**

1. **Text Encoder (T5-XXL / CLIP)** — karmaşık promptları anlar.
2. **U-Net / Transformer Backbone** — gürültüyü temizler (Denoiser).
3. **VAE Decoder** — matematiksel kodu görsele dönüştürür.

**Rectified Flow Avantajı**
- Akış eşleştirme tekniği ile çok daha az adımda (4-8 adım) ultra kaliteli sonuçlar.
- Parmak, el ve yazı detaylarında kusursuzluk.

---

# Prompt Mühendisliği

**Temel Prompt**
```
gelecekteki bir şehir
```

**Detaylı Prompt**
```
2077'de bir cyberpunk metropol, kanji işaretli neon tabelalar,
ışıkları yansıtan yağmurlu sokaklar, hiper-gerçekçi
```

**Stil Belirtilmiş**
```
gelecekteki bir şehir, Studio Ghibli tarzı,
gökdelenlerde yemyeşil bitkiler, yumuşak güneş ışığı
```

**Fotografik**
```
gelecekteki bir şehir, sinematik çekim, IMAX ile çekilmiş,
8k çözünürlük, hacimsel aydınlatma, unreal engine 5.5 render
```

---

# Negatif Prompt

İstenmeyen özellikleri dışlamak için (Modern modellerde artık daha az ihtiyaç duyuluyor):

```
bulanık, düşük kalite, bozuk, eksik uzuvlar,
fazla parmaklar, filigran, grenli, çizgi film tarzı
```

**Etkisi:** Modelin olasılık uzayında bu alanlardan kaçınmasını sağlar.

---

# Model Parametreleri

| Parametre | Ne Yapar? | Değer Aralığı |
|-----------|-----------|---------------|
| **Guidance Scale (CFG)** | Prompt'a ne kadar sıkı bağlı kalacağı | 1-15 (önerilen: 3.5-7) |
| **Sampling Steps** | Gürültü temizleme kalitesi | 10-100 (önerilen: 28) |
| **Seed** | Üretimin "parmak izi" | 0-∞ |
| **Aspect Ratio** | Görüntü oranı | 1:1, 16:9, 9:16, 21:9 |

**Guidance Scale:**
- Düşük: Daha sanatsal ve özgür.
- Yüksek: Daha belirgin ama bazen yapay duran renkler.

---

# Çağdaş Üretken Modeller: Görüntü (2025-2026)

| Model | Geliştirici | Özellik |
|-------|-------------|---------|
| **GPT-5** | OpenAI | Multimodal (Metin, Görüntü, Ses, Video) |
| **Midjourney v7** | Midjourney | Dünyanın en iyi doku (texture) kalitesi |
| **Flux.1.1 Pro** | BFL | Açık kaynak kökenli en güçlü mimari |
| **Imagen 3** | Google | Tam fotorealizm ve Google Workspace entegrasyonu |
| **Firefly v4** | Adobe | Telif hakları garantili, tam ticari güven |

---

# Çağdaş Üretken Modeller: Metin (2025-2026)

| Model | Geliştirici | Özellik |
|-------|-------------|---------|
| **GPT-5.4** | OpenAI | Agentic AI (Kendi başına iş bitirme yeteneği) |
| **Claude 4.6 Opus** | Anthropic | İleri düzey akıl yürütme ve etik uyum |
| **Gemini 3.1 Ultra** | Google | 10M+ token video/doküman bağlamı |
| **Llama 4 2T** | Meta | Yerel kurulumda en yüksek performans |
| **DeepSeek-V4** | DeepSeek | En iyi fiyat/performans ve kodlama başarısı |

---

# Uygulama Alanları

- 🎨 **Reklamcılık** — Saniyeler içinde kampanya görselleri üretimi.
- 💻 **Yazılım Geliştirme** — Claude 4.6 ile uçtan uca uygulama kodlama.
- 💊 **Biyoteknoloji** — Yeni protein katlanmaları ve molekül keşfi.
- 🎬 **Eğlence** — Sora ve Veo 2 ile kişiye özel film sahneleri.
- 🏛️ **Eğitim** — Kişiselleştirilmiş, her öğrenciye özel öğretmen asistanları.

---

# Etik ve Telif Hakları

**Güncel Durum**
- **Eğitim Verisi:** Sanatçıların opt-out (veriden çıkma) hakları yasallaşıyor.
- **Deepfake:** C2PA protokolü ile görsellere "Yapay Zeka" damgası (Watermarking).
- **İş Gücü:** Tekrarlı işlerin otomasyonu ve yeni "AI Operatörlüğü" mesleği.

**Çözümler**
- **AB Yapay Zeka Yasası (AI Act):** Riskli modellerin denetlenmesi.
- **Sentetik Veri:** Modellerin artık kendi ürettikleri temiz verilerle eğitilmesi.

---