# Yapay Zeka Kursları Projesi

## 🎯 Proje Tanımı

Bu proje, üniversite öğrencilerine yönelik **başlangıç seviyesi** yapay zeka eğitim materyallerini içermektedir. Katılımcıların önceden Python bilgisine sahip olması beklenmemektedir.

### Kapsanan Konular
1. **Bilgisayarlı Görü (Computer Vision)**
2. **Üretken Yapay Zeka (Generative AI)**

---

## 📁 Klasör Yapısı

```
kurslar/
├── .gitattributes
├── .gitignore
├── AGENT.md
├── README.md
├── pyproject.toml
│
├── bilgisayarla_goru/
│   ├── docs/
│   │   └── slaytlar/                # Ders slaytları (.pdf, .pptx)
│   ├── notebooks/
│   │   └── bilgisayarla_goru_ornek.ipynb   # Sunum sonrası gösterilecek örnek
│   ├── src/
│   │   ├── __init__.py
│   │   └── utils.py                 # Yardımcı fonksiyonlar
│   └── tests/
│       ├── __init__.py
│       └── test_utils.py
│
└── urekten_yapay_zeka/
    ├── docs/
    │   └── slaytlar/                # Ders slaytları (.pdf, .pptx)
    ├── notebooks/
    │   └── uretken_yapay_zeka_ornek.ipynb  # Sunum sonrası gösterilecek örnek
    ├── src/
    │   ├── __init__.py
    │   └── utils.py                 # Yardımcı fonksiyonlar
    └── tests/
        ├── __init__.py
        └── test_utils.py
```

---

## 🐍 Python Ortamı ve Bağımlılıklar

### Python Versiyonu
- **Minimum:** Python 3.12+

### Sanal Ortam Kurulumu

```bash
# Sanal ortam oluşturma
python -m venv venv

# Aktivasyon (Windows)
venv\Scripts\activate

# Aktivasyon (Linux/macOS)
source venv/bin/activate

# Bağımlılıkları yükleme
pip install -e ".[dev]"
```

### pyproject.toml Yapısı

```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "yapay-zeka-kurslari"
version = "1.0.0"
description = "Üniversite öğrencileri için yapay zeka eğitim materyalleri"
readme = "README.md"
requires-python = ">=3.12"
license = {text = "MIT"}
keywords = ["yapay zeka", "bilgisayarlı görü", "üretken yapay zeka", "eğitim"]

dependencies = [
    "numpy>=1.26.0",
    "matplotlib>=3.8.0",
    "opencv-python>=4.9.0",
    "mediapipe>=0.10.0",
    "torch>=2.2.0",
    "torchvision>=0.17.0",
    "diffusers>=0.27.0",
    "transformers>=4.38.0",
    "accelerate>=0.27.0",
    "Pillow>=10.2.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=8.0.0",
    "pytest-cov>=4.1.0",
    "black>=24.2.0",
    "pylint>=3.0.0",
    "mypy>=1.8.0",
]

[tool.setuptools.packages.find]
where = ["."]
include = ["bilgisayarla_goru*", "urekten_yapay_zeka*"]

[tool.black]
line-length = 88
target-version = ['py312']

[tool.pylint.main]
py-version = "3.12"

[tool.pylint.format]
max-line-length = 88

[tool.mypy]
python_version = "3.12"
disallow_untyped_defs = true
ignore_missing_imports = true

[tool.pytest.ini_options]
testpaths = [
    "bilgisayarla_goru/tests",
    "urekten_yapay_zeka/tests",
]
addopts = "-v --cov=bilgisayarla_goru/src --cov=urekten_yapay_zeka/src"
```

---

## 📝 Kod Standartları

| Kural | Değer |
|-------|-------|
| **Formatter** | Black |
| **Linter** | Pylint |
| **Type Hints** | ✅ Zorunlu |
| **Docstring Formatı** | NumPy Style |
| **Yorum Dili** | Türkçe |
| **Maksimum Satır Uzunluğu** | 88 karakter |

### Docstring Örneği (NumPy Style)

```python
def goruntu_yukle(dosya_yolu: str, gri_tonlama: bool = False) -> np.ndarray:
    """
    Belirtilen dosya yolundan görüntü yükler.

    Parameters
    ----------
    dosya_yolu : str
        Yüklenecek görüntünün dosya yolu.
    gri_tonlama : bool, optional
        True ise görüntü gri tonlamaya dönüştürülür.
        Varsayılan değer False.

    Returns
    -------
    np.ndarray
        Yüklenen görüntü dizisi.

    Raises
    ------
    FileNotFoundError
        Dosya bulunamazsa fırlatılır.
    """
    img = cv2.imread(dosya_yolu)
    
    if img is None:
        raise FileNotFoundError(f"Görüntü bulunamadı: {dosya_yolu}")
    
    if gri_tonlama:
        return cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    return cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

---

## 📚 Modül İçerikleri

### Modül 1: Bilgisayarlı Görü (2-3 Saat)

**Amaç:** Makinelerin görsel dünyayı nasıl "gördüğünü" ve yorumladığını anlamak.

#### Sunum İçeriği (docs/slaytlar/)
- Bilgisayarlı görüye giriş, tarihçe
- Görüntü işleme temelleri (filtreleme, kenar tespiti, renk uzayları)
- Özellik çıkarımı ve nesne tanıma
- Popüler mimariler (AlexNet, ResNet, YOLO, Mask R-CNN)
- Uygulama alanları (otonom araçlar, tıbbi görüntü, AR, kalite kontrol)

#### Notebook Örneği (notebooks/bilgisayarla_goru_ornek.ipynb)
**Seviye:** Giriş-Orta

**İçerik:**
- OpenCV ile temel görüntü işleme (yükleme, gösterme, renk dönüşümü)
- Basit filtre uygulama (blur, kenar tespiti)
- MediaPipe ile gerçek zamanlı yüz/el tespiti demosu

---

### Modül 2: Üretken Yapay Zeka (2-3 Saat)

**Amaç:** Üretken yapay zeka modellerinin çalışma prensiplerini ve uygulama alanlarını kavramak.

#### Sunum İçeriği (docs/slaytlar/)
- Üretken vs ayırt edici modeller
- Temel mimariler (GAN, VAE, Diffusion)
- Uygulama alanları (sanat, veri artırma, ilaç keşfi)

#### Notebook Örneği (notebooks/uretken_yapay_zeka_ornek.ipynb)
**Seviye:** Giriş-Orta

**İçerik:**
- Hazır bir Diffusion modeli ile metinden görüntü üretme
- Farklı prompt'lar ile denemeler
- Basit parametre değişikliklerinin etkisi

---

## 🧪 Test Standartları

```python
"""utils modülü için birim testleri."""

import numpy as np
import pytest

from bilgisayarla_goru.src.utils import goruntu_yukle


class TestGoruntuYukle:
    """goruntu_yukle fonksiyonu için test sınıfı."""

    def test_dosya_bulunamadi_hatasi(self) -> None:
        """Var olmayan dosya için hata fırlatıldığını doğrular."""
        with pytest.raises(FileNotFoundError):
            goruntu_yukle("var_olmayan_dosya.jpg")
```

### Test Komutları

```bash
# Tüm testleri çalıştır
pytest

# Coverage ile çalıştır
pytest --cov
```

---

## 🔧 Geliştirme Komutları

```bash
# Formatlama
black bilgisayarla_goru/ urekten_yapay_zeka/

# Lint kontrolü
pylint bilgisayarla_goru/src/ urekten_yapay_zeka/src/

# Type checking
mypy bilgisayarla_goru/src/ urekten_yapay_zeka/src/
```

---

## 📦 Veri Yönetimi

- ❌ Veri setleri repo'ya **dahil edilmez**
- ❌ Git LFS **kullanılmaz**
- ✅ Notebook içinde gerekli veriler harici linklerden indirilir veya runtime'da oluşturulur

---

## 📋 .gitignore

```gitignore
# Python
__pycache__/
*.py[cod]
venv/
.venv/

# IDE
.idea/
.vscode/

# Test
.pytest_cache/
.coverage
.mypy_cache/

# Veri
data/
*.csv
*.pkl
*.pt
*.pth

# OS
.DS_Store
Thumbs.db
```

---

## 👥 Hedef Kitle

| Özellik | Değer |
|---------|-------|
| **Seviye** | Başlangıç |
| **Kitle** | Üniversite öğrencileri |
| **Ön Koşul** | Python bilgisi gerekmez |
| **Ders Süresi** | Her modül 2-3 saat |
| **Format** | Sunum + Canlı notebook örneği |

---