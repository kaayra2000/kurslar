# Ders Branch’i README Kuralları

Bu belgenin tek amacı: **her bir ders branch’inde** yer alan `README.md` dosyasının **nasıl oluşturulacağını** standartlaştırmaktır.

## 1) Genel ilkeler

- `README.md` ders branch’inin **ana giriş sayfasıdır**: dersin bağlamını ve o branch’teki içerikleri hızlıca anlatır.
- Metin **kısa ve açık** olmalıdır; abartılı vaatlerden kaçınılır.
- Her ders için **tarih** ve **başlık** açıkça yazılır.
- Materyal varsa **doğrudan bağlantı** verilir (dosya yolu linki).

## 2) README zorunlu bölümleri

`README.md` aşağıdaki bölümleri içermelidir:

1. **Başlık (tek satır)**
   - Format: `Kurum / Program — Ders Adı` (gerekirse `— Dönem`)

2. **Kısa açıklama (1 paragraf)**
   - Bu branch’in ne içerdiğini anlatır.
   - Dersin düzeyi, dönem bilgisi ve kapsam bir-iki cümlede geçer.

3. **Bağlam / rol (opsiyonel ama önerilir)**
   - Sunum yapan/konuk olunan durumlar varsa kısa şekilde belirtilir.
   - Dersin yürütücüsü gibi bilgiler gerekiyorsa tek cümleyle eklenir.

4. **Ders listesi (zorunlu)**
   - Her ders için: tarih + ders adı + materyal bağlantıları + kısa içerik özeti.

## 3) Materyal bağlantıları (kural 1)

- Materyal varsa bağlantılar **her ders maddesinin altında** verilir.
- Bağlantı verilecek materyal türleri (varsa):
  - Sunum: `.pptx`, `.pdf`
  - Not defteri (demo): `.ipynb`
  - Ek dosyalar: veri, kod, okuma listesi, vb.
- Bağlantı yazımı:
  - Dosyalar repo içinde ise **göreli yol** kullanılır.
  - Örn: `Ders 1/sunum.pdf` veya `Ders 1/DDİ_Ders_1.ipynb`

## 4) Her ders açıklanacak (kural 2)

Her ders için en az şu bilgiler bulunmalıdır:

- **Ders X (Tarih) — Başlık**
- **Sunum:** (varsa) dosya link(leri)
- **Notebook (demo):** (varsa) dosya link(leri)
- **İçerik:** 1 satırda, noktalı virgül ile ana başlıklar
