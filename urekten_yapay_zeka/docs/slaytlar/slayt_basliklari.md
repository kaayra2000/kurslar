# Üretken Yapay Zeka
### Makineler Nasıl Yaratıcı Olur?

---

# Bugün Ne Öğreneceğiz?

- Üretken vs ayırt edici modeller
- Temel mimariler: GAN, VAE, Diffusion
- LLM ve LVM: Dil ve görüntü modelleri
- Metinden görüntü üretme
- Prompt mühendisliği
- Uygulama alanları

---

# Üretken vs Ayırt Edici Modeller

| Özellik | Ayırt Edici | Üretken |
|---------|-------------|---------|
| **Amaç** | Sınıflandırma, tahmin | Yeni veri üretme |
| **Öğrendiği** | P(y\|x) - Koşullu olasılık | P(x) veya P(x,y) - Birleşik olasılık |
| **Örnek** | CNN, SVM, Logistic Regression | GAN, VAE, Diffusion |
| **Çıktı** | Etiket, sınıf | Yeni görüntü, metin, ses |

---

# GAN: Generative Adversarial Networks

**Yapı:** Generator (Üretici) vs Discriminator (Ayırt Edici)

- İki ağın **rekabetçi eğitimi**
- Generator: sahte veri üretir
- Discriminator: gerçek/sahte ayırt eder
- Denge noktasında: ayırt edilemez kalitede üretim

**Avantajlar:** Keskin, gerçekçi görüntüler  
**Dezavantajlar:** Eğitim zorluğu, mode collapse

---

# VAE: Variational Autoencoders

**Yapı:** Encoder → Latent Space → Decoder

- **Olasılıksal latent uzay** öğrenimi
- Encoder: görüntüyü düşük boyutlu temsile sıkıştırır
- Decoder: latent koddan görüntü yeniden oluşturur
- Latent space'de gezinerek yeni varyasyonlar

**Avantajlar:** Kararlı eğitim, latent manipülasyonu  
**Dezavantajlar:** Bulanık çıktılar

---

# Diffusion Modelleri

**Yapı:** Forward (gürültü ekleme) → Reverse (gürültü çıkarma)

- Adım adım **gürültü temizleme** süreci
- Forward: görüntüye kademeli gürültü ekle
- Reverse: gürültüyü kademeli temizle
- Metin koşullandırması ile yönlendirme

**Avantajlar:** Yüksek kalite, çeşitlilik  
**Dezavantajlar:** Yavaş üretim (50-100 adım)

**Örnekler:** Stable Diffusion, DALL-E, Midjourney

---

# Diffusion Modelleri: Tarihçe

| Model | Yıl | Katkısı |
|-------|-----|---------|
| DDPM | 2020 | Diffusion temellerini attı |
| DALL-E | 2021 | Metinden görüntü, OpenAI |
| Stable Diffusion | 2022 | Açık kaynak, latent diffusion |
| Midjourney | 2022 | Sanatsal kalite odaklı |
| DALL-E 3 | 2023 | Gelişmiş prompt anlama |

---

# LLM: Large Language Models

**Büyük Dil Modelleri** — milyarlarca parametre ile metin anlama ve üretme

| Model | Geliştirici | Parametre | Özellik |
|-------|-------------|-----------|----------|
| GPT-4 | OpenAI | ~1.7T | En yetenekli, kapalı |
| Claude 3.5 Sonnet | Anthropic | ~200B | Uzun bağlam (200K token) |
| Gemini 1.5 Pro | Google | ~? | 1M token bağlam |
| Llama 3.1 | Meta | 405B | Açık kaynak SOTA |
| DeepSeek-V3 | DeepSeek | 671B | MoE, çok verimli |

**Çalışma Prensibi:** Transformer + autoregressive (kelime kelime tahmin)

---

# LVM: Large Vision Models

**Büyük Görüntü Modelleri** — görüntü anlama ve üretme

**Multimodal LVM'ler (Anlama + Üretim)**

| Model | Geliştirici | Yetenek |
|-------|-------------|----------|
| GPT-4o | OpenAI | Metin + görüntü + ses anlama/üretim |
| Claude 3.5 Sonnet | Anthropic | Görüntü analizi, kod üretimi |
| Gemini 1.5 Pro | Google | Video anlama, uzun bağlam |
| Qwen2-VL | Alibaba | Açık kaynak multimodal |

**Sadece Görüntü Üretimi**
- DALL-E 3, Midjourney, Stable Diffusion (sonraki slaytlarda)

---

# Transformer Tabanlı Üretken Modeller

**GPT Ailesi (Metin)**
- GPT-3, GPT-4: metin üretimi
- Autoregressive: kelime kelime üretim
- ChatGPT: konuşma arayüzü

**Claude Ailesi (Anthropic)**
- Claude 4.6 Opus, Sonnet, Haiku
- Güvenlik ve etik odaklı
- Constitutional AI ile eğitildi

**Vision Transformer Üretken Modelleri**
- **DALL-E 2/3**: CLIP + Diffusion
- **Imagen**: Google, metin-görüntü
- **Parti**: Google, photorealistic

---

# CLIP: Görüntü-Metin Köprüsü

- OpenAI tarafından geliştirildi (2021)
- 400 milyon görüntü-metin çiftiyle eğitildi
- Görüntü ve metni **aynı embedding uzayına** taşır
- Diffusion modellerinin "yönlendirme" katmanı

**Kullanım Alanları**
- Zero-shot sınıflandırma
- Metinden görüntü arama
- Stable Diffusion'da prompt anlama

---

# Stable Diffusion Mimarisi

**3 Ana Bileşen**

1. **Text Encoder (CLIP)** — prompt'u anlar
2. **U-Net** — latent space'de gürültü temizler
3. **VAE Decoder** — latent'i görüntüye dönüştürür

**Latent Diffusion Avantajı**
- Piksel yerine **sıkıştırılmış latent** üzerinde çalışır
- 8x daha hızlı, 8x daha az bellek

---

# Prompt Mühendisliği

**Temel Prompt**
```
a cat sitting on a chair
```

**Detaylı Prompt**
```
a fluffy orange cat sitting on a vintage wooden chair,
soft natural lighting, cozy living room background
```

**Stil Belirtilmiş**
```
a cat sitting on a chair, oil painting style,
impressionist, vibrant colors, artistic
```

**Fotografik**
```
a cat sitting on a chair, professional photography,
DSLR, shallow depth of field, 8k, highly detailed
```

---

# Negatif Prompt

İstenmeyen özellikleri belirtir:

```
blurry, low quality, distorted, ugly, bad anatomy,
cartoon, illustration, watermark
```

**Etkisi:** Modelin bu özellikleri üretmesini engeller

---

# Model Parametreleri

| Parametre | Ne Yapar? | Değer Aralığı |
|-----------|-----------|---------------|
| **Guidance Scale** | Prompt'a bağlılık | 1-20 (önerilen: 7-10) |
| **Steps** | Gürültü temizleme adımı | 20-150 (önerilen: 50) |
| **Seed** | Tekrarlanabilirlik | 0-∞ |
| **Resolution** | Çıktı boyutu | 512×512, 768×768, 1024×1024 |

**Guidance Scale:**
- Düşük (3-5): yaratıcı, çeşitli ama prompt'tan sapabilir
- Yüksek (15-20): prompt'a sadık ama tekdüze

---

# Çağdaş Üretken Modeller: Görüntü (2023-2025)

| Model | Geliştirici | Özellik |
|-------|-------------|---------|
| DALL-E 3 | OpenAI | Gelişmiş prompt anlama |
| Midjourney v6 | Midjourney | Sanatsal kalite |
| Stable Diffusion XL | Stability AI | Yüksek çözünürlük |
| Imagen 2 | Google | Photorealistic |
| Firefly | Adobe | Ticari kullanım güvenli |
| Flux | Black Forest Labs | Açık kaynak, SOTA |

---

# Çağdaş Üretken Modeller: Metin (2023-2025)

| Model | Geliştirici | Özellik |
|-------|-------------|---------|
| GPT-4 Turbo/o | OpenAI | Multimodal, function calling |
| Claude 3.5 Sonnet | Anthropic | 200K bağlam, kod üretimi |
| Gemini 1.5 Pro | Google | 1M token, video anlama |
| Llama 3.1 405B | Meta | Açık kaynak, en büyük |
| DeepSeek-V3 | DeepSeek | MoE, maliyet-verimli |
| Qwen2.5 | Alibaba | Çok dilli, açık kaynak |

---

# Flux: Yeni Nesil Diffusion

- Black Forest Labs (Stable Diffusion ekibi) tarafından geliştirildi (2024)
- **Rectified Flow** mimarisi (diffusion'dan daha hızlı)
- 12 milyar parametre
- Metin rendering'de çok başarılı
- Açık kaynak versiyonları mevcut

**Varyantlar:**
- Flux.1 Pro — en kaliteli, kapalı
- Flux.1 Dev — açık, ticari olmayan
- Flux.1 Schnell — hızlı, 4 adım

---

# Uygulama Alanları

- 🎨 **Sanat ve Tasarım** — Midjourney, DALL-E ile görsel içerik
- 📊 **Veri Artırma** — eğitim verisi çoğaltma
- 💊 **İlaç Keşfi** — molekül yapısı, protein tasarımı
- 🎮 **Oyun/Film** — texture, karakter, asset üretimi
- 👤 **Kişiselleştirilmiş İçerik** — avatar, özel tasarım
- 📝 **Belge Üretimi** — sentetik form, fatura

---

# Etik ve Telif Hakları

**Sorunlar**
- Eğitim verisi telif hakkı ihlali mi?
- Deepfake ve dezenformasyon riski
- Sanatçıların işlerinin kopyalanması

**Çözümler**
- Adobe Firefly: lisanslı veri ile eğitildi
- Watermarking: üretilen içeriği işaretle
- Yasal düzenlemeler (AB AI Act)

---