# Yapay Zekâ ile Kariyer
### CV Hazırlama, Yönetme ve İlan Bulma

Muhammed Kayra Bulut — BT Yöneticisi, YTÜ Yıldız Teknopark — Ekim 2026

> Not: Bu sunumdaki CV sistemi kendi iş arama sürecimde kullandığım gerçek bir depodur.

---

# Bugün Ne Konuşacağız?

1. CV'nin temelleri ve ATS
2. CV'yi kod gibi yönetmek (kendi sistemim)
3. İlan bulma ve akıllı başvuru
4. Araç haritası: ücretsiz, ücretli, açık kaynak

---

# 2026'da İşe Alım: İki Tarafta da Yapay Zekâ

| İşveren tarafı | Aday tarafı |
|---|---|
| ATS CV'yi ayrıştırır ve sıralar | LLM ile ilan analizi |
| YZ destekli aday arama (LinkedIn Recruiter) | CV uyarlama, ön yazı |
| Otomatik eleme soruları | Açık kaynak iş arama ajanları |

**Sonuç:** Fark yaratan şey araç değil; doğru, ölçülebilir ve ilana uygun içerik.

---

# ATS CV'nizi Nasıl Okur?

1. **Ayrıştırma:** PDF metne çevrilir, alanlara bölünür (iletişim, deneyim, eğitim, beceri)
2. **Eşleştirme:** İlandaki anahtar kelime, beceri ve unvanlar aranır
3. **Sıralama:** Aday puanlanır, eleme soruları uygulanır

> Not: Son kararı insan verir. ATS'nin görevi önce okumak, sonra öne çıkarmaktır.

---

# ATS Uyumlu CV: Yap ve Yapma

| Yap | Yapma |
|---|---|
| Tek sütun, standart başlıklar | Medeni durum, din gibi kişisel bilgi |
| Metni seçilebilen PDF | "CV" veya "Özgeçmiş" başlığı |
| İlandaki terimleri birebir kullan | Açıklanmamış kısaltma |
| Ters kronolojik sıra | Aynı bilginin tekrarı |
| | Gerçek olmayan bilgi |

> Not: "Yapma" listesi kendi CV depomdaki RULES.md dosyasından alındı.

---

# İyi Bir Madde Nasıl Yazılır?

**Aktif fiil + ne yaptın + nasıl (teknoloji) + ölçülebilir sonuç**

- Zayıf: "Backend geliştirmelerinde görev aldım."
- Güçlü: "Java 21 ve virtual thread'lerle REST servisini yeniden tasarladım; p95 gecikmeyi %40 düşürdüm."

> Not: Bu örnek kurgusaldır, formülü göstermek içindir.

---

# Aynı Deneyim, Farklı Vurgu

- **Genel CV:** "C++ uygulamalarında güvenli veri kalıcılığı için Wt::Dbo ORM kütüphanesini ve veri serileştirme amacıyla Protobuf araçlarını entegre ettim."
- **Java CV:** "PostgreSQL üzerinde Wt::Dbo ORM kütüphanesi, ilişkisel veri modelleme ve Protobuf veri serileştirme entegrasyonu ile nesne yönelimli veri kalıcılık katmanı tasarladım. Temel tasarım kalıplarını uyguladım."

> Not: Yalan yok, vurgu var. Hedef alanla ilişkili kavram (ORM, veri modelleme, OOP) maddenin başına alınır.

---

# LLM ile Madde İyileştirme

```text
Aşağıdaki ilan metnini ve CV maddemi karşılaştır.
1) İlanda geçen ama CV'mde olmayan kavramları listele.
2) Maddeyi "aktif fiil + iş + sonuç" biçiminde yeniden yaz.
3) CV'mde olmayan hiçbir deneyim, sayı veya teknoloji ekleme.
   Emin değilsen bana soru sor.
```

---

# CV'yi Kod Gibi Yönetmek: Problem

- Tek CV her ilana uymaz
- 4 alan (Java, LLM, ML, MLOps) × 2 dil + 64 ilan paketi = onlarca dosya
- Hangi sürüm güncel? Yeni proje hangi CV'lere girdi? TR ve EN tutarlı mı?

**Çözüm:** Yazılım mühendisliği prensipleri: tek doğruluk kaynağı, derleme, sürüm kontrolü, otomasyon.

---

# Mimari: Tek Kaynaktan Onlarca CV

```text
info/*.yml  ──►  genel_cvler/ (java, llm, machine_learning, mlops)
   │                   │
   └──────────────►  ilana_ozel_cvler/<sirket_pozisyon>/
                         │
                 LaTeX + build.sh (Docker pdflatex)
                         │
                  ATS uyumlu TR/EN PDF  ── Git ile sürümlenir
```

- 71 proje kaydı, 4 alan CV'si, 64 ilan paketi (17'sinde ilana özel CV)
- 76 commit (Mart–Eylül 2026)

---

# Tek Doğruluk Kaynağı: info/projects.yml

```yaml
- id: agentic-dynamic-memory-router
  name:
    en: Agentic Dynamic Memory Router
    tr: Ajan Dinamik Bellek Yönlendiricisi
  category: llm_ai
  tags: [python, ai-agents, context-window]
  dates: Jul 2026 -- Aug 2026
  github_url: https://github.com/kaayra2000/agentic_dynamic_memory_router
  featured: true
```

- İki dil tek kayıtta
- Tarih aralığı reponun ilk ve son commit'inden hesaplanır
- Etiketler alan CV'si eşlemesinde kullanılır

---

# Ajan Kuralları Dosyada Yaşar (AGENTS.md / RULES.md)

- Her değişiklik TR ve EN CV'ye eşzamanlı yansır
- Sıfır halüsinasyon: gerçek olmayan bilgi yazılmaz, ilan canlı doğrulanır
- Onaysız ekleme veya silme yok: "şu anki veri" ile "gerçek veri" karşılaştırılır
- Snapshot koruması: başvurulan paket geriye dönük değişmez
- Kalite kapısı: Overfull \hbox yok, her sayfa görsel kontrol, ATS metin çıkarımı

> Not: AGENTS.md dosyasını Claude Code, Codex ve Gemini gibi farklı ajanlar okur.

---

# İş Akışları: Tek Cümleyle Tetiklenir

- **hesapları senkronize et:** `fetch_latest_data.py` GitHub, Hugging Face, Medium, ORCID ve LinkedIn verisini çeker; ajan kıyaslar; madde madde onay
- **cvleri senkronize et:** `info/*.yml` ile kök ve alan CV'leri karşılaştırılır; ilgisiz alana dokunulmaz
- **ilan eşleştir:** ilan metni → en uygun CV ya da yeni paket
- **iş araştırması yap ve cv üret:** LinkedIn öncelikli tarama → filtre → paket
- **eski ilanları temizle:** `clean_old_jobs.py --dry-run` → tablo → onay → silme

---

# Bir İlan Paketinin Anatomisi

```text
ilana_ozel_cvler/anzera_ai_engineer/
├── IS_ILANI.md       # ilanın tam ham metni ve bağlantısı (özet yok)
└── ILAN_NOTLARI.md   # eşleşme analizi ve tek öncelikli CV
```

- Karar: `genel_cvler/llm` yeterli, yeni .tex ve .pdf üretilmedi
- Uygun CV yoksa veya eskiyse: `info/` verisinden ilana özel TR/EN .tex ve .pdf üretilir

---

# İlan Nerede?

- **LinkedIn:** iş uyarıları, YZ destekli iş arama
- **Kurumsal kariyer portalları:** en güncel ve doğrudan kaynak
- **Kariyer.net, Techcareer.net, Youthall:** yerel platformlar
- **YTÜ Yıldız Teknopark Firmalarımız sayfası:** 750+ firma; ilan açılmadan önce firmayı tanıyın

---

# Akıllı Filtre

1. **Aktif mi?** "Başvuru kabul etmiyor" uyarısı varsa veya Başvur butonu yoksa ele
2. **Daha önce başvurdum mu?** Depodaki ilan bağlantıları ve LinkedIn "Applied" etiketi
3. **Ham metni çek:** LinkedIn guest endpoint + `curl` → `IS_ILANI.md`
4. **Eşleştir:** CV seç veya üret; son kontrol insanda

> Not: Kişisel kullanım, düşük hacim. Platform kullanım koşullarına uyun.

---

# Gizli Pazar: Doğrudan İletişim

- Hedef şirket listesi → işe alım uzmanı veya teknik yönetici
- Kısa ve kişisel mesaj; toplu, kopyala-yapıştır mesaj yok
- Kendi sistemimde: şirket başına tek dosya, mesaj taslağı ilanın hemen altında

```text
Merhaba [Ad], [Şirket]'in [ekip/ürün] çalışmalarını takip ediyorum.
[İlgili tek somut deneyim]. [Rol] pozisyonları için CV'mi
paylaşabilir miyim?
```

---

# Açık Kaynak Araçlar

| Araç | Tür | Ne yapar | Lisans |
|---|---|---|---|
| Reactive Resume | CV | Tarayıcıda CV editörü; self-host, JSON, YZ desteği | MIT |
| RenderCV | CV | YAML'dan PDF; CV'yi kod gibi yönet | MIT |
| JSON Resume | CV | Standart CV şeması ve CLI | MIT |
| OpenResume | CV | CV oluşturucu ve ATS ayrıştırıcı | AGPL-3.0 |
| Resume Matcher | CV | Yerel LLM ile ilan–CV uyumu | Apache-2.0 |
| career-ops | Ajan | CLI ajanı: ilan tarar, 1-5 puanlar, CV uyarlar, takip eder | MIT |
| ai-job-search | Ajan | Claude Code ile ilan değerlendirme, CV, ön yazı, mülakat | MIT |
| ApplyPilot | Ajan | Otomatik başvuru; platform koşullarını kontrol edin | AGPL-3.0 |

---

# Ücretli ve Freemium Servisler

| Servis | Ücretsiz | Ücretli |
|---|---|---|
| Teal | Sınırsız CV, iş takibi | Teal+ 29 $/ay |
| Jobscan | Kayıtta 5 tarama | 49,95 $/ay |
| Rezi | 1 CV, 3 PDF | 29 $/ay veya 149 $ ömür boyu |
| Kickresume | Temel şablonlar | 8 $/ay (yıllık) |
| Huntr | İş takibi | 40 $/ay |

Genel LLM'ler (ChatGPT, Claude, Gemini): ücretsiz katman mevcut.

---

# Hangi Araç Kime?

- **Yeni başlıyorum:** ücretsiz LLM + Reactive Resume
- **ATS'ye takılıyor muyum?** OpenResume ayrıştırıcı, Jobscan ücretsiz taramaları
- **Çok başvuru, takip zor:** Huntr veya Teal ücretsiz katmanı
- **Geliştiriciyim, kontrol bende olsun:** RenderCV veya LaTeX + Git + ajan (career-ops, ai-job-search ya da kendi AGENTS.md dosyan)

---

# Riskler ve Etik

- **Halüsinasyon:** LLM olmayan deneyim veya sayı ekleyebilir; her maddeyi doğrula
- **Kişisel veri (KVKK):** telefon, adres, kimlik bilgisini bulut LLM'e yükleme; maskele veya yerel model kullan
- **Otomatik toplu başvuru:** platform koşullarını ihlal edebilir, hesap kısıtlanabilir
- **"YZ kokan" metin:** kalıp ifadeler, abartılı sıfatlar; kendi sesini koru
- **Son karar insanda**

---

# Bugün Başlayın

1. Tüm deneyim ve projeleri tek kaynak dosyada topla (YAML veya JSON)
2. ATS uyumlu tek sütun şablon seç (LaTeX, RenderCV, Reactive Resume)
3. Hedef rollerine göre 2-4 alan CV'si çıkar
4. Her ilan için: LLM ile boşluk analizi → uyarlama → insan kontrolü
5. Başvuru takibi ve haftalık rutin: ilan uyarıları, eski ilan temizliği

**İlk adım en önemlisi:** tek kaynak olmadan her uyarlama yeni bir kopya demektir.

---

# Teşekkürler — Sorular?

- Sunum ve kaynaklar: github.com/kaayra2000/kurslar
- Araç listesi: `sunum/kaynaklar.md`
- LinkedIn: Muhammed Kayra Bulut · GitHub: kaayra2000
