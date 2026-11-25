# TeknoLab (ÖNDER TeknoGenç) — Derin Öğrenme ve Yapay Sinir Ağları — 2026-2027 Güz

Bu branch, TeknoLab'da 28 Kasım 2026 Cumartesi günü saat 10.00'da yapılacak tek oturumluk dersin materyallerini içerir. Ders; yapay sinir ağlarının temellerini, bir ağın nasıl öğrendiğini ve derin öğrenme mimarilerini başlangıç düzeyinde ele alır. Ön bilgi gerektirmez. Önce sunum yapılır, ardından notebook ile canlı örnek gösterilir.

Dersi ben (Muhammed Kayra Bulut, YTÜ Yıldız Teknopark BT Yöneticisi) anlatıyorum. Sunum, YTÜ Yıldız Teknopark kurumsal kimliğine göre hazırlanmıştır.

- **Ders (28.11.2026)** — Derin Öğrenme ve Yapay Sinir Ağları: Makineler Nasıl Öğrenir?
	- Sunum: [sunum/sunum.pptx](sunum/sunum.pptx), [sunum/sunum.pdf](sunum/sunum.pdf)
	- Slayt akışı ve notlar: [sunum/slayt_basliklari.md](sunum/slayt_basliklari.md)
	- Notebook (demo): [notebook/derin_ogrenme_ornek.ipynb](notebook/derin_ogrenme_ornek.ipynb)
	- Kaynaklar ve araçlar: [sunum/kaynaklar.md](sunum/kaynaklar.md)
		- İçerik: yapay zekâ, makine öğrenmesi ve derin öğrenme ilişkisi; kısa tarihçe; yapay nöron ve aktivasyon fonksiyonları; XOR problemi ve katmanlar; kayıp fonksiyonu, gradyan inişi ve geri yayılım; epoch, batch ve veri bölme; aşırı öğrenme; CNN, RNN, Transformer ve büyük dil modelleri; uygulama alanları; PyTorch örneği; yol haritası; sınırlar ve sorumluluk

## Notebook'u çalıştırma

Notebook, sinir ağını hiçbir derin öğrenme kütüphanesi kullanmadan yalnızca NumPy ile sıfırdan yazar; grafikler için Matplotlib, el yazısı rakam veri seti için scikit-learn kullanır.

- **Google Colab:** Dosya → Not defteri yükle ile notebook'u açın; kütüphaneler hazır gelir.
- **Yerelde:**

```bash
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install numpy matplotlib scikit-learn jupyter
jupyter notebook notebook/derin_ogrenme_ornek.ipynb
```
