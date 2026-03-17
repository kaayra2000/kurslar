# Bilgisayarlı Görü Modülü

## 🎯 Modül Tanımı

**Amaç:** Makinelerin görsel dünyayı nasıl "gördüğünü" ve yorumladığını anlamak, bilgisayarlı görü alanındaki temel uygulamaları ve bu alandaki proje potansiyellerini öğrenmek.

**Süre:** 2-3 Saat  
**Seviye:** Başlangıç (Giriş-Orta seviye örnek)  
**Hedef Kitle:** Üniversite öğrencileri

---

## 📁 Klasör Yapısı

```
bilgisayarla_goru/
├── AGENT.md
├── docs/
│   └── slaytlar/                          # Sunum dosyaları (.pdf, .pptx)
├── notebooks/
│   └── bilgisayarla_goru_ornek.ipynb      # Canlı demo notebook
├── src/
│   ├── __init__.py
│   └── utils.py                           # Yardımcı fonksiyonlar
└── tests/
    ├── __init__.py
    └── test_utils.py
```

---

## 📚 Sunum İçeriği (docs/slaytlar/)

### 1. Bilgisayarlı Görüye Giriş
- Alanın tanımı ve tarihçesi
- Makinelerin pikselleri nasıl anlamsal bilgiye dönüştürdüğü
- Bilgisayarlı görme ile görüntü işleme arasındaki fark
- Yapay zeka ve makine öğrenimi ile ilişkisi

### 2. Görüntü İşlemenin Temelleri
- **Filtreleme:** Görüntü yumuşatma, keskinleştirme
- **Kenar Tespiti:** Sobel, Canny algoritmaları
- **Renk Uzayları:** RGB, HSV, Grayscale dönüşümleri
- **Yeniden Boyutlandırma:** Enterpolasyon yöntemleri

### 3. Özellik Çıkarımı ve Nesne Tanıma
- **Geleneksel Yöntemler:** SIFT, SURF, HOG
- **Derin Öğrenme ile Özellik Çıkarımı:** CNN tabanlı yaklaşımlar
- **Temel Görevler:**
  - Görüntü sınıflandırma (Image Classification)
  - Nesne tespiti (Object Detection)
  - Görüntü segmentasyonu (Image Segmentation)

### 4. Popüler Mimariler ve Modeller

| Model | Yıl | Özellik |
|-------|-----|---------|
| **AlexNet** | 2012 | CNN devriminin başlangıcı |
| **VGGNet** | 2014 | Derin ve basit mimari |
| **ResNet** | 2015 | Skip connection ile derin ağlar |
| **YOLO** | 2016 | Gerçek zamanlı nesne tespiti |
| **Mask R-CNN** | 2017 | Instance segmentation |

### 5. Uygulama Alanları
- **Otonom Araçlar:** Şerit takibi, nesne algılama
- **Tıbbi Görüntü Analizi:** X-ray, MRI, CT tarama analizi
- **Artırılmış Gerçeklik (AR):** Yüz filtreleri, sanal objeler
- **Kalite Kontrol:** Üretim hattında hata tespiti
- **Güvenlik Sistemleri:** Yüz tanıma, hareket algılama

---

## 💻 Notebook İçeriği (notebooks/bilgisayarla_goru_ornek.ipynb)

### Örnek Seviyesi: Giriş-Orta

### Bölüm 1: Temel Görüntü İşleme (OpenCV)

```python
"""Temel görüntü işleme örneği."""

import cv2
import numpy as np
import matplotlib.pyplot as plt


def goruntu_yukle_ve_goster(dosya_yolu: str) -> np.ndarray:
    """
    Görüntüyü yükler ve RGB formatına dönüştürür.

    Parameters
    ----------
    dosya_yolu : str
        Görüntü dosyasının yolu.

    Returns
    -------
    np.ndarray
        RGB formatında görüntü dizisi.
    """
    img = cv2.imread(dosya_yolu)
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    return img_rgb


def kenar_tespit_et(goruntu: np.ndarray, esik1: int = 100, esik2: int = 200) -> np.ndarray:
    """
    Canny algoritması ile kenar tespiti yapar.

    Parameters
    ----------
    goruntu : np.ndarray
        Giriş görüntüsü.
    esik1 : int, optional
        Alt eşik değeri. Varsayılan 100.
    esik2 : int, optional
        Üst eşik değeri. Varsayılan 200.

    Returns
    -------
    np.ndarray
        Kenar haritası.
    """
    gri = cv2.cvtColor(goruntu, cv2.COLOR_RGB2GRAY)
    kenarlar = cv2.Canny(gri, esik1, esik2)
    return kenarlar
```

### Bölüm 2: Gerçek Zamanlı Yüz Tespiti (MediaPipe)

```python
"""MediaPipe ile yüz tespiti örneği."""

import cv2
import mediapipe as mp


def yuz_tespiti_baslat() -> None:
    """
    Webcam üzerinden gerçek zamanlı yüz tespiti yapar.

    MediaPipe Face Detection modülünü kullanarak
    kameradan alınan görüntüde yüzleri tespit eder
    ve işaretler.
    """
    mp_face_detection = mp.solutions.face_detection
    mp_drawing = mp.solutions.drawing_utils

    cap = cv2.VideoCapture(0)

    with mp_face_detection.FaceDetection(
        model_selection=0,
        min_detection_confidence=0.5
    ) as face_detection:

        while cap.isOpened():
            success, frame = cap.read()
            if not success:
                continue

            # BGR -> RGB dönüşümü
            frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
            results = face_detection.process(frame_rgb)

            # Yüzleri çiz
            if results.detections:
                for detection in results.detections:
                    mp_drawing.draw_detection(frame, detection)

            cv2.imshow('Yuz Tespiti', frame)

            if cv2.waitKey(5) & 0xFF == ord('q'):
                break

    cap.release()
    cv2.destroyAllWindows()
```

### Bölüm 3: Basit Filtre Galerisi

```python
"""Farklı filtrelerin görüntü üzerindeki etkisi."""

def filtre_galerisi_olustur(goruntu: np.ndarray) -> dict[str, np.ndarray]:
    """
    Görüntüye çeşitli filtreler uygular.

    Parameters
    ----------
    goruntu : np.ndarray
        Giriş görüntüsü (RGB).

    Returns
    -------
    dict[str, np.ndarray]
        Filtre adı ve sonuç görüntüsü çiftleri.
    """
    gri = cv2.cvtColor(goruntu, cv2.COLOR_RGB2GRAY)

    filtreler = {
        "Orijinal": goruntu,
        "Gri Tonlama": gri,
        "Gaussian Blur": cv2.GaussianBlur(goruntu, (15, 15), 0),
        "Canny Kenar": cv2.Canny(gri, 100, 200),
        "Sobel X": cv2.Sobel(gri, cv2.CV_64F, 1, 0, ksize=3),
        "Sobel Y": cv2.Sobel(gri, cv2.CV_64F, 0, 1, ksize=3),
    }

    return filtreler
```

---

## 🛠️ src/utils.py İçeriği

```python
"""Bilgisayarlı görü yardımcı fonksiyonları."""

from pathlib import Path
from typing import Optional

import cv2
import numpy as np
import numpy.typing as npt


def goruntu_yukle(
    dosya_yolu: str | Path,
    gri_tonlama: bool = False
) -> npt.NDArray[np.uint8]:
    """
    Belirtilen dosya yolundan görüntü yükler.

    Parameters
    ----------
    dosya_yolu : str | Path
        Yüklenecek görüntünün dosya yolu.
    gri_tonlama : bool, optional
        True ise görüntü gri tonlamaya dönüştürülür.
        Varsayılan değer False.

    Returns
    -------
    npt.NDArray[np.uint8]
        Yüklenen görüntü dizisi.

    Raises
    ------
    FileNotFoundError
        Dosya bulunamazsa fırlatılır.
    """
    dosya_yolu = Path(dosya_yolu)

    if not dosya_yolu.exists():
        raise FileNotFoundError(f"Görüntü bulunamadı: {dosya_yolu}")

    img = cv2.imread(str(dosya_yolu))

    if img is None:
        raise ValueError(f"Geçersiz görüntü dosyası: {dosya_yolu}")

    if gri_tonlama:
        return cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    return cv2.cvtColor(img, cv2.COLOR_BGR2RGB)


def goruntu_boyutlandir(
    goruntu: npt.NDArray[np.uint8],
    genislik: Optional[int] = None,
    yukseklik: Optional[int] = None
) -> npt.NDArray[np.uint8]:
    """
    Görüntüyü belirtilen boyutlara yeniden boyutlandırır.

    Parameters
    ----------
    goruntu : npt.NDArray[np.uint8]
        Giriş görüntüsü.
    genislik : int, optional
        Hedef genişlik. None ise orana göre hesaplanır.
    yukseklik : int, optional
        Hedef yükseklik. None ise orana göre hesaplanır.

    Returns
    -------
    npt.NDArray[np.uint8]
        Yeniden boyutlandırılmış görüntü.

    Raises
    ------
    ValueError
        Her iki boyut da None ise fırlatılır.
    """
    if genislik is None and yukseklik is None:
        raise ValueError("En az bir boyut belirtilmelidir.")

    h, w = goruntu.shape[:2]

    if genislik is None:
        oran = yukseklik / h
        yeni_boyut = (int(w * oran), yukseklik)
    elif yukseklik is None:
        oran = genislik / w
        yeni_boyut = (genislik, int(h * oran))
    else:
        yeni_boyut = (genislik, yukseklik)

    return cv2.resize(goruntu, yeni_boyut, interpolation=cv2.INTER_LINEAR)
```

---

## 🧪 tests/test_utils.py İçeriği

```python
"""utils modülü için birim testleri."""

from pathlib import Path

import cv2
import numpy as np
import pytest

from bilgisayarla_goru.src.utils import goruntu_yukle, goruntu_boyutlandir


class TestGoruntuYukle:
    """goruntu_yukle fonksiyonu için test sınıfı."""

    def test_dosya_bulunamadi_hatasi(self) -> None:
        """Var olmayan dosya için FileNotFoundError fırlatıldığını doğrular."""
        with pytest.raises(FileNotFoundError):
            goruntu_yukle("var_olmayan_dosya.jpg")

    def test_gecerli_goruntu_yukleme(self, tmp_path: Path) -> None:
        """Geçerli görüntünün başarıyla yüklendiğini doğrular."""
        # Arrange
        test_img = np.random.randint(0, 255, (100, 100, 3), dtype=np.uint8)
        dosya = tmp_path / "test.png"
        cv2.imwrite(str(dosya), test_img)

        # Act
        sonuc = goruntu_yukle(dosya)

        # Assert
        assert sonuc.shape == (100, 100, 3)

    def test_gri_tonlama(self, tmp_path: Path) -> None:
        """Gri tonlama dönüşümünün çalıştığını doğrular."""
        # Arrange
        test_img = np.random.randint(0, 255, (100, 100, 3), dtype=np.uint8)
        dosya = tmp_path / "test.png"
        cv2.imwrite(str(dosya), test_img)

        # Act
        sonuc = goruntu_yukle(dosya, gri_tonlama=True)

        # Assert
        assert len(sonuc.shape) == 2


class TestGoruntuBoyutlandir:
    """goruntu_boyutlandir fonksiyonu için test sınıfı."""

    def test_boyut_belirtilmedi_hatasi(self) -> None:
        """Boyut belirtilmediğinde ValueError fırlatıldığını doğrular."""
        img = np.zeros((100, 100, 3), dtype=np.uint8)

        with pytest.raises(ValueError):
            goruntu_boyutlandir(img)

    def test_genislik_ile_boyutlandirma(self) -> None:
        """Sadece genişlik ile boyutlandırmayı doğrular."""
        img = np.zeros((100, 200, 3), dtype=np.uint8)

        sonuc = goruntu_boyutlandir(img, genislik=100)

        assert sonuc.shape == 100
        assert sonuc.shape[0] == 50  # Oran korunmalı
```

---

## 📦 Kullanılan Kütüphaneler

| Kütüphane | Kullanım Amacı |
|-----------|----------------|
| `opencv-python` | Görüntü işleme, filtreleme, kenar tespiti |
| `mediapipe` | Gerçek zamanlı yüz/el/poz tespiti |
| `numpy` | Dizi işlemleri |
| `matplotlib` | Görselleştirme |

---

## 🎓 Öğrenme Çıktıları

Bu modülü tamamlayan katılımcılar:

1. ✅ Bilgisayarlı görünün temel kavramlarını anlayacak
2. ✅ OpenCV ile temel görüntü işleme yapabilecek
3. ✅ Kenar tespiti ve filtreleme tekniklerini uygulayabilecek
4. ✅ MediaPipe ile gerçek zamanlı yüz tespiti yapabilecek
5. ✅ Popüler CNN mimarilerini tanıyacak
6. ✅ Kendi projelerinde bilgisayarlı görüyü nasıl kullanacaklarını bilecek