# Üretken Yapay Zeka Modülü

## 🎯 Modül Tanımı

**Amaç:** Üretken yapay zeka modellerinin çalışma prensiplerini, temel mimarileri (GAN, VAE, Diffusion) ve metinden görüntü üretme, sentetik veri oluşturma gibi popüler uygulama alanlarını kavramak.

**Süre:** 2-3 Saat  
**Seviye:** Başlangıç (Giriş-Orta seviye örnek)  
**Hedef Kitle:** Üniversite öğrencileri

---

## 📁 Klasör Yapısı

```
urekten_yapay_zeka/
├── AGENT.md
├── docs/
│   └── slaytlar/                           # Sunum dosyaları (.pdf, .pptx)
├── notebooks/
│   └── uretken_yapay_zeka_ornek.ipynb      # Canlı demo notebook
├── src/
│   ├── __init__.py
│   └── utils.py                            # Yardımcı fonksiyonlar
└── tests/
    ├── __init__.py
    └── test_utils.py
```

---

## 📚 Sunum İçeriği (docs/slaytlar/)

### 1. Üretken ve Ayırt Edici Modeller

| Özellik | Ayırt Edici (Discriminative) | Üretken (Generative) |
|---------|------------------------------|----------------------|
| **Amaç** | Sınıflandırma, tahmin | Yeni veri üretme |
| **Öğrendiği** | P(y\|x) - Koşullu olasılık | P(x) veya P(x,y) - Birleşik olasılık |
| **Örnek** | CNN, SVM, Logistic Regression | GAN, VAE, Diffusion |
| **Çıktı** | Etiket, sınıf | Yeni görüntü, metin, ses |

### 2. Temel Mimariler

#### 2.1 Generative Adversarial Networks (GANs)
- **Yapı:** Generator (Üretici) vs Discriminator (Ayırt Edici)
- **Çalışma Prensibi:** İki ağın rekabetçi eğitimi
- **Avantajlar:** Keskin, gerçekçi görüntüler
- **Dezavantajlar:** Eğitim zorluğu, mode collapse

#### 2.2 Variational Autoencoders (VAEs)
- **Yapı:** Encoder → Latent Space → Decoder
- **Çalışma Prensibi:** Olasılıksal latent uzay öğrenimi
- **Avantajlar:** Kararlı eğitim, latent space manipülasyonu
- **Dezavantajlar:** Bulanık çıktılar

#### 2.3 Diffusion Modelleri
- **Yapı:** Forward (gürültü ekleme) → Reverse (gürültü çıkarma)
- **Çalışma Prensibi:** Adım adım gürültü temizleme
- **Avantajlar:** Yüksek kalite, çeşitlilik
- **Dezavantajlar:** Yavaş üretim süreci
- **Örnekler:** Stable Diffusion, DALL-E, Midjourney

### 3. Uygulama Alanları

| Alan | Kullanım | Örnek |
|------|----------|-------|
| **Sanat ve Tasarım** | Görsel içerik üretimi | Midjourney, DALL-E |
| **Veri Artırma** | Eğitim verisi çoğaltma | Sentetik görüntüler |
| **İlaç Keşfi** | Molekül yapısı üretimi | Protein tasarımı |
| **Kişiselleştirilmiş İçerik** | Özelleştirilmiş medya | Avatar oluşturma |
| **Oyun/Film** | Asset üretimi | Texture, karakter |

---

## 💻 Notebook İçeriği (notebooks/uretken_yapay_zeka_ornek.ipynb)

### Örnek Seviyesi: Giriş-Orta

### Bölüm 1: Ortam Hazırlığı

```python
"""Gerekli kütüphanelerin import edilmesi."""

import torch
from diffusers import StableDiffusionPipeline
from PIL import Image
import matplotlib.pyplot as plt


def gpu_kontrol() -> str:
    """
    Kullanılabilir cihazı kontrol eder.

    Returns
    -------
    str
        Kullanılacak cihaz ('cuda' veya 'cpu').
    """
    if torch.cuda.is_available():
        print(f"GPU bulundu: {torch.cuda.get_device_name(0)}")
        return "cuda"
    else:
        print("GPU bulunamadı, CPU kullanılacak.")
        return "cpu"
```

### Bölüm 2: Stable Diffusion ile Görüntü Üretme

```python
"""Stable Diffusion ile metinden görüntü üretme."""

from typing import Optional

import torch
from diffusers import StableDiffusionPipeline
from PIL import Image


def model_yukle(
    model_id: str = "runwayml/stable-diffusion-v1-5",
    cihaz: str = "cuda"
) -> StableDiffusionPipeline:
    """
    Stable Diffusion modelini yükler.

    Parameters
    ----------
    model_id : str, optional
        Hugging Face model ID'si.
        Varsayılan "runwayml/stable-diffusion-v1-5".
    cihaz : str, optional
        Kullanılacak cihaz ('cuda' veya 'cpu').
        Varsayılan "cuda".

    Returns
    -------
    StableDiffusionPipeline
        Yüklenmiş model pipeline'ı.
    """
    pipe = StableDiffusionPipeline.from_pretrained(
        model_id,
        torch_dtype=torch.float16 if cihaz == "cuda" else torch.float32
    )
    pipe = pipe.to(cihaz)

    return pipe


def goruntu_uret(
    pipe: StableDiffusionPipeline,
    prompt: str,
    negatif_prompt: Optional[str] = None,
    adim_sayisi: int = 50,
    rehberlik_olcegi: float = 7.5,
    seed: Optional[int] = None
) -> Image.Image:
    """
    Verilen prompt'a göre görüntü üretir.

    Parameters
    ----------
    pipe : StableDiffusionPipeline
        Yüklenmiş model pipeline'ı.
    prompt : str
        Üretilecek görüntüyü tanımlayan metin.
    negatif_prompt : str, optional
        Görüntüde olmaması istenen özellikler.
    adim_sayisi : int, optional
        Diffusion adım sayısı. Varsayılan 50.
    rehberlik_olcegi : float, optional
        Prompt'a bağlılık derecesi. Varsayılan 7.5.
    seed : int, optional
        Tekrarlanabilirlik için rastgele tohum.

    Returns
    -------
    Image.Image
        Üretilen görüntü.
    """
    generator = None
    if seed is not None:
        generator = torch.Generator(device=pipe.device).manual_seed(seed)

    sonuc = pipe(
        prompt=prompt,
        negative_prompt=negatif_prompt,
        num_inference_steps=adim_sayisi,
        guidance_scale=rehberlik_olcegi,
        generator=generator
    )

    return sonuc.images[0]
```

### Bölüm 3: Prompt Mühendisliği Örnekleri

```python
"""Farklı prompt teknikleri ve sonuçları."""

# Temel prompt örnekleri
PROMPT_ORNEKLERI: dict[str, str] = {
    "basit": "a cat sitting on a chair",

    "detayli": "a fluffy orange cat sitting on a vintage wooden chair, "
               "soft natural lighting, cozy living room background",

    "stil_belirtilmis": "a cat sitting on a chair, "
                        "oil painting style, impressionist, "
                        "vibrant colors, artistic",

    "fotografik": "a cat sitting on a chair, "
                  "professional photography, DSLR, "
                  "shallow depth of field, 8k, highly detailed",
}

# Negatif prompt örnekleri
NEGATIF_PROMPT_ORNEKLERI: dict[str, str] = {
    "genel": "blurry, low quality, distorted, ugly, bad anatomy",

    "fotografik": "cartoon, illustration, painting, drawing, "
                  "low resolution, watermark",
}


def prompt_karsilastirma_goster(
    pipe: StableDiffusionPipeline,
    promptlar: dict[str, str],
    seed: int = 42
) -> dict[str, Image.Image]:
    """
    Farklı promptların sonuçlarını karşılaştırır.

    Parameters
    ----------
    pipe : StableDiffusionPipeline
        Yüklenmiş model pipeline'ı.
    promptlar : dict[str, str]
        Prompt adı ve içeriği çiftleri.
    seed : int, optional
        Karşılaştırma için sabit seed. Varsayılan 42.

    Returns
    -------
    dict[str, Image.Image]
        Prompt adı ve üretilen görüntü çiftleri.
    """
    sonuclar = {}

    for ad, prompt in promptlar.items():
        print(f"Üretiliyor: {ad}")
        sonuclar[ad] = goruntu_uret(pipe, prompt, seed=seed)

    return sonuclar
```

### Bölüm 4: Parametre Etkilerini Keşfetme

```python
"""Model parametrelerinin çıktı üzerindeki etkisi."""

def parametre_etkisi_goster(
    pipe: StableDiffusionPipeline,
    prompt: str,
    seed: int = 42
) -> dict[str, list[Image.Image]]:
    """
    Farklı parametre değerlerinin etkisini gösterir.

    Parameters
    ----------
    pipe : StableDiffusionPipeline
        Yüklenmiş model pipeline'ı.
    prompt : str
        Test için kullanılacak prompt.
    seed : int, optional
        Karşılaştırma için sabit seed. Varsayılan 42.

    Returns
    -------
    dict[str, list[Image.Image]]
        Parametre adı ve farklı değerlerle üretilen görüntüler.
    """
    sonuclar = {}

    # Guidance scale etkisi
    print("Guidance scale testi...")
    sonuclar["guidance_scale"] = []
    for scale in [3.0, 7.5, 15.0]:
        img = goruntu_uret(pipe, prompt, rehberlik_olcegi=scale, seed=seed)
        sonuclar["guidance_scale"].append(img)

    # Adım sayısı etkisi
    print("Adım sayısı testi...")
    sonuclar["adim_sayisi"] = []
    for adim in [20, 50, 100]:
        img = goruntu_uret(pipe, prompt, adim_sayisi=adim, seed=seed)
        sonuclar["adim_sayisi"].append(img)

    return sonuclar
```

---

## 🛠️ src/utils.py İçeriği

```python
"""Üretken yapay zeka yardımcı fonksiyonları."""

from pathlib import Path
from typing import Optional

import torch
from PIL import Image


def cihaz_sec() -> torch.device:
    """
    En uygun hesaplama cihazını seçer.

    Returns
    -------
    torch.device
        Kullanılacak cihaz (CUDA, MPS veya CPU).
    """
    if torch.cuda.is_available():
        return torch.device("cuda")
    elif torch.backends.mps.is_available():
        return torch.device("mps")
    else:
        return torch.device("cpu")


def goruntu_kaydet(
    goruntu: Image.Image,
    dosya_yolu: str | Path,
    kalite: int = 95
) -> Path:
    """
    Görüntüyü belirtilen yola kaydeder.

    Parameters
    ----------
    goruntu : Image.Image
        Kaydedilecek görüntü.
    dosya_yolu : str | Path
        Hedef dosya yolu.
    kalite : int, optional
        JPEG kalitesi (1-100). Varsayılan 95.

    Returns
    -------
    Path
        Kaydedilen dosyanın yolu.
    """
    dosya_yolu = Path(dosya_yolu)
    dosya_yolu.parent.mkdir(parents=True, exist_ok=True)

    goruntu.save(dosya_yolu, quality=kalite)

    return dosya_yolu


def goruntu_grid_olustur(
    goruntuler: list[Image.Image],
    sutun_sayisi: int = 3,
    bosluk: int = 10
) -> Image.Image:
    """
    Birden fazla görüntüyü grid formatında birleştirir.

    Parameters
    ----------
    goruntuler : list[Image.Image]
        Birleştirilecek görüntüler.
    sutun_sayisi : int, optional
        Grid sütun sayısı. Varsayılan 3.
    bosluk : int, optional
        Görüntüler arası boşluk (piksel). Varsayılan 10.

    Returns
    -------
    Image.Image
        Birleştirilmiş grid görüntüsü.
    """
    if not goruntuler:
        raise ValueError("Görüntü listesi boş olamaz.")

    # Görüntü boyutlarını al
    img_genislik, img_yukseklik = goruntuler[0].size

    # Grid boyutlarını hesapla
    satir_sayisi = (len(goruntuler) + sutun_sayisi - 1) // sutun_sayisi

    grid_genislik = sutun_sayisi * img_genislik + (sutun_sayisi - 1) * bosluk
    grid_yukseklik = satir_sayisi * img_yukseklik + (satir_sayisi - 1) * bosluk

    # Boş grid oluştur
    grid = Image.new("RGB", (grid_genislik, grid_yukseklik), color=(255, 255, 255))

    # Görüntüleri yerleştir
    for idx, img in enumerate(goruntuler):
        satir = idx // sutun_sayisi
        sutun = idx % sutun_sayisi

        x = sutun * (img_genislik + bosluk)
        y = satir * (img_yukseklik + bosluk)

        grid.paste(img, (x, y))

    return grid


def seed_ayarla(seed: int) -> torch.Generator:
    """
    Tekrarlanabilirlik için rastgele tohum ayarlar.

    Parameters
    ----------
    seed : int
        Rastgele tohum değeri.

    Returns
    -------
    torch.Generator
        Ayarlanmış generator nesnesi.
    """
    torch.manual_seed(seed)

    if torch.cuda.is_available():
        torch.cuda.manual_seed_all(seed)

    generator = torch.Generator(device=cihaz_sec()).manual_seed(seed)

    return generator
```

---

## 🧪 tests/test_utils.py İçeriği

```python
"""utils modülü için birim testleri."""

from pathlib import Path

import pytest
import torch
from PIL import Image

from urekten_yapay_zeka.src.utils import (
    cihaz_sec,
    goruntu_kaydet,
    goruntu_grid_olustur,
    seed_ayarla,
)


class TestCihazSec:
    """cihaz_sec fonksiyonu için test sınıfı."""

    def test_gecerli_cihaz_doner(self) -> None:
        """Geçerli bir torch.device döndüğünü doğrular."""
        cihaz = cihaz_sec()

        assert isinstance(cihaz, torch.device)
        assert cihaz.type in ["cuda", "mps", "cpu"]


class TestGoruntuKaydet:
    """goruntu_kaydet fonksiyonu için test sınıfı."""

    def test_goruntu_basariyla_kaydedilir(self, tmp_path: Path) -> None:
        """Görüntünün başarıyla kaydedildiğini doğrular."""
        # Arrange
        img = Image.new("RGB", (100, 100), color="red")
        dosya_yolu = tmp_path / "test_goruntu.png"

        # Act
        sonuc = goruntu_kaydet(img, dosya_yolu)

        # Assert
        assert sonuc.exists()
        assert sonuc == dosya_yolu

    def test_klasor_otomatik_olusturulur(self, tmp_path: Path) -> None:
        """Alt klasörlerin otomatik oluşturulduğunu doğrular."""
        # Arrange
        img = Image.new("RGB", (100, 100), color="blue")
        dosya_yolu = tmp_path / "alt_klasor" / "test.png"

        # Act
        sonuc = goruntu_kaydet(img, dosya_yolu)

        # Assert
        assert sonuc.exists()
        assert sonuc.parent.exists()


class TestGoruntuGridOlustur:
    """goruntu_grid_olustur fonksiyonu için test sınıfı."""

    def test_bos_liste_hatasi(self) -> None:
        """Boş liste için ValueError fırlatıldığını doğrular."""
        with pytest.raises(ValueError, match="boş olamaz"):
            goruntu_grid_olustur([])

    def test_tek_goruntu_grid(self) -> None:
        """Tek görüntü ile grid oluşturulduğunu doğrular."""
        # Arrange
        img = Image.new("RGB", (100, 100), color="green")

        # Act
        grid = goruntu_grid_olustur([img], sutun_sayisi=1)

        # Assert
        assert grid.size == (100, 100)

    def test_coklu_goruntu_grid(self) -> None:
        """Birden fazla görüntü ile grid oluşturulduğunu doğrular."""
        # Arrange
        goruntuler = [Image.new("RGB", (100, 100), color="red") for _ in range(4)]

        # Act
        grid = goruntu_grid_olustur(goruntuler, sutun_sayisi=2, bosluk=10)

        # Assert
        beklenen_genislik = 2 * 100 + 1 * 10  # 2 sütun + 1 boşluk
        beklenen_yukseklik = 2 * 100 + 1 * 10  # 2 satır + 1 boşluk
        assert grid.size == (beklenen_genislik, beklenen_yukseklik)


class TestSeedAyarla:
    """seed_ayarla fonksiyonu için test sınıfı."""

    def test_generator_doner(self) -> None:
        """torch.Generator döndüğünü doğrular."""
        generator = seed_ayarla(42)

        assert isinstance(generator, torch.Generator)

    def test_ayni_seed_ayni_sonuc(self) -> None:
        """Aynı seed ile aynı rastgele sayıların üretildiğini doğrular."""
        # Arrange & Act
        seed_ayarla(42)
        tensor1 = torch.rand(5)

        seed_ayarla(42)
        tensor2 = torch.rand(5)

        # Assert
        assert torch.equal(tensor1, tensor2)
```

---

## 📦 Kullanılan Kütüphaneler

| Kütüphane | Kullanım Amacı |
|-----------|----------------|
| `torch` | Derin öğrenme framework'ü |
| `diffusers` | Stable Diffusion ve diğer diffusion modelleri |
| `transformers` | Model tokenizer ve konfigürasyonları |
| `accelerate` | GPU optimizasyonu |
| `Pillow` | Görüntü işleme |
| `matplotlib` | Görselleştirme |

---

## ⚠️ Donanım Gereksinimleri

| Bileşen | Minimum | Önerilen |
|---------|---------|----------|
| **RAM** | 8 GB | 16 GB |
| **GPU VRAM** | 4 GB | 8+ GB |
| **Disk** | 10 GB | 20 GB |

> **Not:** GPU olmadan da çalıştırılabilir ancak görüntü üretimi çok yavaş olacaktır (CPU'da ~5-10 dakika/görüntü).

---

## 🎓 Öğrenme Çıktıları

Bu modülü tamamlayan katılımcılar:

1. ✅ Üretken ve ayırt edici modeller arasındaki farkı anlayacak
2. ✅ GAN, VAE ve Diffusion modellerinin temel çalışma prensiplerini kavrayacak
3. ✅ Stable Diffusion ile metinden görüntü üretebilecek
4. ✅ Prompt mühendisliği tekniklerini uygulayabilecek
5. ✅ Model parametrelerinin çıktı üzerindeki etkisini anlayacak
6. ✅ Kendi projelerinde sentetik veri üretimini planlayabilecek

---

## 💡 Vaka Çalışması: Sentetik Veri Üretimi

### Senaryo
Bir görüntü sınıflandırma projesi için yeterli eğitim verisi yok. Stable Diffusion kullanarak sentetik veri üretelim.

### Adımlar

```python
"""Sentetik veri üretimi örneği."""

SINIFLAR: list[str] = ["kedi", "köpek", "kuş"]

PROMPT_SABLONU: str = (
    "a {sinif} in a natural environment, "
    "realistic photography, high quality, detailed"
)


def sentetik_veri_uret(
    pipe: StableDiffusionPipeline,
    siniflar: list[str],
    goruntu_sayisi: int = 10
) -> dict[str, list[Image.Image]]:
    """
    Her sınıf için sentetik görüntüler üretir.

    Parameters
    ----------
    pipe : StableDiffusionPipeline
        Yüklenmiş model pipeline'ı.
    siniflar : list[str]
        Üretilecek sınıf isimleri.
    goruntu_sayisi : int, optional
        Her sınıf için üretilecek görüntü sayısı.
        Varsayılan 10.

    Returns
    -------
    dict[str, list[Image.Image]]
        Sınıf adı ve üretilen görüntüler.
    """
    veri_seti: dict[str, list[Image.Image]] = {}

    for sinif in siniflar:
        print(f"'{sinif}' sınıfı için görüntüler üretiliyor...")
        veri_seti[sinif] = []

        for i in range(goruntu_sayisi):
            prompt = PROMPT_SABLONU.format(sinif=sinif)
            img = goruntu_uret(pipe, prompt, seed=i)
            veri_seti[sinif].append(img)

    return veri_seti
```