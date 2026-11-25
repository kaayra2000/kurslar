# Derin Öğrenme ve Yapay Sinir Ağları
### Makineler Nasıl Öğrenir?

Muhammed Kayra Bulut — BT Yöneticisi, YTÜ Yıldız Teknopark — TeknoLab, 28 Kasım 2026 Cumartesi, 10.00

> Not: Ön bilgi gerekmez. Formüller yalnızca sezgiyi desteklemek için gösterilir; ezberlenmesi beklenmez.

---

# Bugün Ne Konuşacağız?

1. **Temeller:** yapay nöron, aktivasyon, katmanlar
2. **Bir ağ nasıl öğrenir?** Kayıp, gradyan inişi, geri yayılım
3. **Mimariler:** CNN, RNN, Transformer, büyük dil modelleri
4. **Uygulama ve başlangıç:** kod, canlı demo, yol haritası

---

# Derin Öğrenme, Makine Öğrenmesinin Bir Alt Dalıdır

- **Yapay zekâ:** insan zekâsı gerektiren işleri yapan sistemler
- **Makine öğrenmesi:** kuralları elle yazmak yerine veriden öğrenen yöntemler
- **Derin öğrenme:** çok katmanlı yapay sinir ağlarıyla öğrenme

| Klasik programlama | Makine öğrenmesi |
|---|---|
| Kural + veri → cevap | Veri + cevap → kural |

> Not: Spam filtresi örneği: kuralları tek tek yazmak yerine binlerce etiketli e-postadan kuralı modele buldururuz.

---

# Fikir 80 Yaşında, Patlama Son 15 Yılda

| Yıl | Olay |
|---|---|
| 1943 | McCulloch ve Pitts: ilk matematiksel nöron modeli |
| 1958 | Rosenblatt: Perceptron, öğrenebilen ilk nöron |
| 1969 | Minsky ve Papert: tek katman XOR'u çözemez → "yapay zekâ kışı" |
| 1986 | Rumelhart, Hinton, Williams: geri yayılım yaygınlaşır |
| 2012 | AlexNet: ImageNet yarışmasında derin öğrenme açık ara kazanır |
| 2017 | "Attention Is All You Need": Transformer mimarisi |
| 2022 | ChatGPT: büyük dil modelleri herkesin elinde |
| 2024 | Nobel Fizik: Hopfield ve Hinton; Nobel Kimya: AlphaFold (Hassabis, Jumper) ve Baker |

---

# Üç Şey Birleşti: Veri, Donanım, Algoritma

- **Veri:** internet ölçeğinde etiketli ve etiketsiz veri (ImageNet: 14 milyondan fazla görüntü)
- **Donanım:** GPU'lar binlerce çarpmayı aynı anda yapar
- **Algoritma:** ReLU, dropout, batch normalization, artık bağlantılar, Transformer

> Not: Derin öğrenmenin çekirdeği matris çarpımıdır. GPU, oyun grafiği için tasarlandı; aynı iş yapay sinir ağına da uyuyor.

---

# 01 · Temeller

---

# Yapay Nöron: Ağırlıklı Toplam ve Bir Karar

- Girdiler (x) ağırlıklarla (w) çarpılır ve toplanır, sonra sapma (b) eklenir
- Sonuç bir aktivasyon fonksiyonundan (f) geçer

```text
x1 ──w1──┐
x2 ──w2──┼──► Σ (w·x) + b ──► f ──► y
x3 ──w3──┘
```

**Formül:** y = f(w1·x1 + w2·x2 + w3·x3 + b)

> Not: Biyolojik nöron benzetmesi bir sezgidir. Yapay nöron beyni taklit etmez; yalnızca sayıları toplar ve eşikten geçirir.

---

# Örnek Nöron: "Konsere Gideyim mi?"

| Girdi | Değer (x) | Önem (w) | x · w |
|---|---|---|---|
| Hava güzel mi? | 1 | 0,6 | 0,6 |
| Arkadaşım geliyor mu? | 0 | 0,3 | 0,0 |
| Bilet ucuz mu? | 1 | 0,5 | 0,5 |
| Sapma (b) | | | −0,8 |
| **Toplam (z)** | | | **0,3** |

- z > 0 olduğu için karar: **Git**
- Öğrenme = bu ağırlıkları ve sapmayı veriden bulmak

---

# Aktivasyon Fonksiyonu Ağa Eğrilik Katar

| Fonksiyon | Formül | Nerede |
|---|---|---|
| Basamak | z > 0 ise 1, değilse 0 | İlk perceptron |
| Sigmoid | 1 / (1 + e^(−z)) | Olasılık çıktısı (0–1) |
| ReLU | max(0, z) | Gizli katmanların varsayılanı |

> Not: Aktivasyon olmasaydı katmanları üst üste koymak işe yaramazdı; doğrusal fonksiyonların bileşimi yine doğrusaldır.

---

# Tek Nöron XOR'u Çözemez

| x1 | x2 | XOR |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

- Tek nöron düzlemi **tek bir doğruyla** ikiye böler
- XOR'da 1'leri 0'lardan ayıran tek bir doğru yoktur
- 1969: bu gözlem yapay zekâ kışını başlatır
- **Çözüm:** nöronları katmanlar hâlinde birleştirmek

---

# Katmanlar: Girdi → Gizli → Çıktı

- **Girdi katmanı:** veriyi alır (piksel, kelime, sensör değeri)
- **Gizli katmanlar:** ara özellikleri öğrenir
- **Çıktı katmanı:** cevabı verir (sınıf olasılıkları, sayı)
- Her çizgi bir ağırlıktır: slayttaki örnek ağda 50, GPT-3'te 175 milyar ağırlık vardır

> Not: Bir gizli katmanlı ağ bile, yeterince nöronla, her sürekli fonksiyona istenen yakınlıkta yaklaşabilir (evrensel yaklaşım teoremi).

---

# "Derin" Kelimesi Katman Sayısından Gelir

- İlk katmanlar basit örüntüleri yakalar: kenar, köşe, renk
- Orta katmanlar bunları birleştirir: göz, tekerlek, harf
- Son katmanlar kavrama ulaşır: yüz, araba, kelime
- Özellikleri insan tasarlamaz; ağ veriden kendisi çıkarır

---

# 02 · Bir Ağ Nasıl Öğrenir?

---

# Öğrenme Dört Adımlı Bir Döngüdür

1. **İleri yayılım:** girdi ağdan geçer, tahmin üretilir
2. **Kayıp hesabı:** tahmin ile gerçek cevap karşılaştırılır
3. **Geri yayılım:** her ağırlığın hatadaki payı hesaplanır
4. **Güncelleme:** ağırlıklar hatayı azaltacak yöne küçük bir adım atar

Döngü binlerce, milyonlarca kez tekrarlanır.

---

# Kayıp Fonksiyonu Hatayı Tek Bir Sayıya Çevirir

- **Ortalama kare hata (MSE):** sayı tahmininde; L = (y − ŷ)² ortalaması
- **Çapraz entropi:** sınıflandırmada; doğru sınıfa verilen olasılık düştükçe kayıp hızla büyür
- Örnek: gerçek fiyat 100, tahmin 90 → kare hata 100

> Not: Öğrenmenin tek hedefi bu sayıyı küçültmektir. Ağ "doğruyu" bilmez; yalnızca kaybı azaltır.

---

# Gradyan İnişi: Sisli Dağda Aşağı İnmek

- Sisli bir dağdasınız, vadiyi göremiyorsunuz
- Ayağınızın altındaki eğime bakıp en dik iniş yönüne bir adım atarsınız
- **Güncelleme kuralı:** w ← w − η · ∂L/∂w
- **Öğrenme oranı (η)** adım boyudur

| Öğrenme oranı | Sonuç |
|---|---|
| Çok küçük | Çok yavaş öğrenir |
| Uygun | Vadiye ulaşır |
| Çok büyük | Vadiyi atlar, salınır ya da dağılır |

---

# Geri Yayılım Hatayı Sondan Başa Dağıtır

- Hata çıktıda ölçülür, katman katman geriye doğru taşınır
- Her ağırlığa "hatanın ne kadarı senden?" sorusu sorulur
- Matematiksel karşılığı **zincir kuralıdır:** ∂L/∂w = ∂L/∂ŷ · ∂ŷ/∂z · ∂z/∂w
- PyTorch ve TensorFlow bunu otomatik yapar (otomatik türev)

---

# Eğitimin Dili: Epoch, Batch, Veri Bölme

- **Batch:** ağırlıklar her seferde küçük bir örnek grubuyla güncellenir (ör. 32 örnek)
- **Epoch:** tüm veri setinin ağdan bir kez geçmesi
- **Eğitim / doğrulama / test:** öğren, ayarla, en sonda bir kez ölç (ör. %70 / %15 / %15)

> Not: Test verisi sınavdır. Sınav sorularıyla çalışılan model, gerçek hayatta kötü sonuç verir.

---

# Ezber Değil Genelleme: Aşırı Öğrenmeyi İzleyin

- Eğitim kaybı düşerken doğrulama kaybı yükselmeye başlarsa model **ezberliyordur**
- **Çareler:**
  - Daha fazla veri ya da veri artırma (döndürme, kırpma)
  - Dropout: eğitimde nöronları rastgele kapatmak
  - Erken durdurma: doğrulama kaybı kötüleşince durmak
  - Daha küçük model ya da düzenlileştirme

> Not: Grafik temsilîdir, kavramı göstermek içindir.

---

# 03 · Mimariler

---

# Her Veri Türüne Uygun Bir Mimari Var

| Mimari | Veri | Örnek |
|---|---|---|
| Çok katmanlı algılayıcı (MLP) | Tablo | Kredi riski |
| Evrişimli ağ (CNN) | Görüntü | Röntgen analizi |
| Yinelemeli ağ (RNN, LSTM) | Dizi | Eski çeviri ve konuşma sistemleri |
| Transformer | Metin, görüntü, ses | ChatGPT, Claude, Gemini |
| Difüzyon modeli | Görüntü üretimi | Stable Diffusion, Flux |

---

# CNN: Küçük Bir Filtre Görüntünün Üstünde Kayar

- 3×3'lük bir filtre görüntü üzerinde gezer, her konumda çarpım toplamı alır
- Aynı filtre her yerde kullanılır: kedinin yeri değişse de tanınır
- **Havuzlama (pooling):** haritayı küçültür, önemli bilgiyi korur
- Filtrelerin değerleri de veriden öğrenilir

```text
Kenar filtresi
-1  0  1
-2  0  2
-1  0  1
```

---

# Transformer: Her Kelime Diğerlerine Bakar

- RNN metni kelime kelime okur; uzun cümlede başı unutur
- **Dikkat (attention):** her kelime cümledeki tüm kelimelere bakar ve hangisinin önemli olduğunu tartar
- Tüm kelimeler paralel işlenir; GPU ile çok hızlı eğitilir

> Örnek: "Kedi süte uzandı çünkü **o** acıkmıştı." → "o" kelimesi en çok "kedi"ye dikkat eder.

---

# Dil Modelleri Bir Sonraki Kelimeyi Tahmin Eder

- Eğitim hedefi basit: metindeki bir sonraki token'ı tahmin et
- Örnek: "Bugün hava çok güzel, hadi ..." → dışarı %41, parka %27, yürüyüşe %18 (temsilî)
- Ölçek büyüdükçe yeni beceriler ortaya çıkar: özetleme, kod yazma, akıl yürütme
- Ardından insan geri bildirimiyle ince ayar yapılır (RLHF)
- Sınır: emin görünerek yanlış bilgi üretebilir (halüsinasyon)

> Not: Model her adımda bir kelime seçer, seçtiğini girdiye ekler ve yeniden tahmin eder.

---

# 04 · Uygulama ve Başlangıç

---

# Derin Öğrenme Hayatın Her Alanında

- **Sağlık:** röntgen ve MR'da hastalık tespiti
- **Bilim:** AlphaFold ile protein yapısı tahmini
- **Ulaşım:** otonom sürüşte nesne algılama
- **Dil:** çeviri, özetleme, sohbet asistanları
- **Ses:** konuşma tanıma, metinden sese
- **Üretim:** görüntü, müzik ve video üretimi

---

# 12 Satırda XOR'u Çözen Sinir Ağı (PyTorch)

```python
import torch
from torch import nn

model = nn.Sequential(
    nn.Linear(2, 8), nn.ReLU(),
    nn.Linear(8, 1), nn.Sigmoid(),
)
x = torch.tensor([[0., 0.], [0., 1.], [1., 0.], [1., 1.]])
y = torch.tensor([[0.], [1.], [1.], [0.]])
opt = torch.optim.Adam(model.parameters(), lr=0.05)
for _ in range(1000):
    loss = nn.functional.binary_cross_entropy(model(x), y)
    opt.zero_grad(); loss.backward(); opt.step()
```

> Not: XOR'u çözen ağ. `loss.backward()` geri yayılımı, `opt.step()` gradyan inişini yapar.

---

# Canlı Demo: Öğrenmeyi Gözünüzle Görün

- **TensorFlow Playground:** tarayıcıda ağ kur, katman ve nöron ekle, öğrenmeyi izle (playground.tensorflow.org)
- **Demo notebook** ([notebook/derin_ogrenme_ornek.ipynb](../notebook/derin_ogrenme_ornek.ipynb)): yalnızca NumPy ile sıfırdan sinir ağı; XOR ve el yazısı rakam tanıma, test doğruluğu yaklaşık %96
- İkisi de tarayıcıda ya da Google Colab'de ücretsiz çalışır; kurulum gerekmez

---

# Nereden Başlamalı? Beş Adımlık Yol Haritası

1. **Python:** temel sözdizimi, NumPy
2. **Matematik sezgisi:** vektör, matris, türev (3Blue1Brown videoları)
3. **Klasik makine öğrenmesi:** scikit-learn ile ilk modeller
4. **Derin öğrenme:** PyTorch, fast.ai, Dive into Deep Learning
5. **Proje:** Kaggle yarışmaları, kendi veri setinle küçük bir proje

---

# Sınırlar ve Sorumluluk

- **Veri yanlılığı:** veri neyi içeriyorsa model onu öğrenir, önyargı dâhil
- **Kara kutu:** kararın nedenini açıklamak zordur
- **Enerji ve maliyet:** büyük modellerin eğitimi çok elektrik tüketir
- **Halüsinasyon:** emin görünen yanlış cevaplar

**Sonuç:** Model öneri sunar; kararı ve sorumluluğu insan taşır.

---

# Teşekkürler

Sorular?

- Sunum ve kaynaklar: github.com/kaayra2000/kurslar
- GitHub: kaayra2000
- LinkedIn: Muhammed Kayra Bulut
