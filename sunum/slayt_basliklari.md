# Yapay Zekâ ile Kariyer
### CV Hazırlama, Yönetme ve İlan Bulma

Muhammed Kayra Bulut — BT Yöneticisi, YTÜ Yıldız Teknopark — Ekim 2026

> Not: Bu sunumdaki CV sistemi kendi iş arama sürecimde kullandığım gerçek bir depodur.

---

# Bugün Ne Konuşacağız?

1. CV'nin temelleri ve ATS
2. CV'yi kod gibi yönetmek (genel çerçeve, örnek: kendi sistemim)
3. İlan bulma ve akıllı başvuru
4. Araç haritası: ücretsiz, ücretli, açık kaynak

---

# 2026'da İşe Alım: İki Tarafta da Yapay Zekâ

| İşveren tarafı | Aday tarafı |
|---|---|
| ATS CV'yi ayrıştırır ve sıralar | LLM ile ilan analizi |
| YZ destekli aday arama (LinkedIn Recruiter) | CV uyarlama, ön yazı |
| Otomatik eleme soruları | Açık kaynak iş arama eylemcileri |

**Sonuç:** Farkı oluşturan şey araç değil; doğru, ölçülebilir ve ilana uygun içerik.

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

# Sorun: Tek CV Her İlana Uymaz

- Tek CV her ilana uymaz
- Birden çok alan × iki dil + ilana özel sürümler = onlarca dosya
- Hangi sürüm güncel? Yeni proje hangi CV'lere girdi? TR ve EN tutarlı mı?

> Örnek (kendi CV depom): 4 alan (Java, LLM, ML, MLOps) × 2 dil + 64 ilan paketi

**Çözüm:** Yazılım mühendisliği prensipleri: tek doğruluk kaynağı, derleme, sürüm kontrolü, eylemci otomasyonu.

---

# Mimari: Tek Kaynaktan Onlarca CV

Genel akış (altta kendi depomdaki karşılığı):

```text
Tek kaynak  ──►  Alan CV'leri  ──►  İlana özel CV'ler  ──►  Derleme  ──►  ATS uyumlu PDF
(YAML/JSON)      (hedef role göre)  (gerektiğinde)         (LaTeX, RenderCV)  (TR ve EN)
info/*.yml       genel_cvler/       ilana_ozel_cvler/      build.sh           TR / EN PDF
```

- Git ile sürümlenir; kurallar eylemcilere dosyada verilir
- Örnek uygulama (kendi CV depom): 71 proje kaydı, 4 alan CV'si, 64 ilan paketi, 76 commit

---

# Tek Doğruluk Kaynağı Olmalı

- **Her bilgi tek yerde:** CV'ler kopyalanmaz, kaynaktan türetilir
- **İki dil tek kayıtta:** TR ve EN birbirinden kopmaz
- **Etiketler eşler:** kaydın hangi CV'ye gireceğini belirler
- **Tarih kanıttan gelir:** örneğin reponun ilk ve son commit'i

Örnek: `info/projects.yml`

```yaml
- id: agentic-dynamic-memory-router
  name:
    en: Agentic Dynamic Memory Router
    tr: Eylemci Dinamik Bellek Yönlendiricisi
  category: llm_ai
  tags: [python, ai-agents, context-window]
  dates: Jul 2026 -- Aug 2026
  featured: true
  cv_section: featured_llm
```

---

# Eylemcilere Kurallar Verilmeli

- **Diller eşzamanlı:** her değişiklik tüm dillere anlamca eşit yansır
- **Sıfır uydurma:** gerçek olmayan bilgi yazılmaz, ilan canlı doğrulanır
- **Onaysız değişiklik yok:** eylemci farkı gösterir, insan onaylar
- **Başvuru anı korunur:** gönderilen CV sonradan değiştirilmez
- **Kalite kapısı:** taşma kontrolü, sayfa sayfa görsel kontrol, ATS metin çıkarımı
- **Kurallar dosyada:** düz metin; hangi eylemci olursa olsun aynı dosyayı okur

> Örnek uygulama: AGENTS.md ve RULES.md dosyaları; Claude Code, Codex ve Gemini aynı dosyayı okur.

---

# İş Akışları: Tek Cümleyle Tetiklenir

| İş akışı | Ne yapar | Örnek komut (kendi depom) |
|---|---|---|
| Hesap verisini güncelle | Profil verisi çekilir, kaynakla kıyaslanır; her fark tek tek onaylanır | `hesapları senkronize et` |
| CV'leri kaynakla eşitle | Kaynak dosya CV'lerle karşılaştırılır; yalnızca ilgili CV değişir | `cvleri senkronize et` |
| İlanı eşleştir | İlan metni analiz edilir; en uygun CV seçilir ya da yeni CV önerilir | `ilan eşleştir` |
| İlan ara, CV hazırla | İlanlar taranır; kapalı ve başvurulmuş olanlar elenir, paket hazırlanır | `iş araştırması yap ve cv üret` |
| Eski ilanları temizle | Silinecekler önce listelenir; açık onaydan sonra silinir | `eski ilanları temizle` |

---

# Her Başvurunun Kaydı Tutulmalı

- **İlan metni saklanır:** ilan yayından kalksa da neye başvurulduğu bilinir
- **Eşleşme notu tutulur:** hangi CV seçildi ve neden seçildi
- **Önce mevcut CV denenir:** uygun ve güncel CV varsa yenisi oluşturulmaz
- **Gerekirse ilana özel CV:** kaynaktan türetilir; elle kopyalanmaz

Örnek uygulama (ilan paketi):

```text
ilana_ozel_cvler/anzera_ai_engineer/
├── IS_ILANI.md       # ilanın tam ham metni ve bağlantısı (özet yok)
└── ILAN_NOTLARI.md   # eşleşme analizi ve tek öncelikli CV
```

- 64 ilan paketi, 17'sinde ilana özel CV

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
| career-ops | Eylemci | CLI eylemcisi: ilan tarar, 1-5 puanlar, CV uyarlar, takip eder | MIT |
| ai-job-search | Eylemci | Claude Code ile ilan değerlendirme, CV, ön yazı, mülakat | MIT |
| ApplyPilot | Eylemci | Otomatik başvuru; platform koşullarını kontrol edin | AGPL-3.0 |

---

# Ücretli ve Freemium Servisler

| Servis | Ücretsiz | Ücretli |
|---|---|---|
| Teal | Sınırsız CV, iş takibi | Teal+ 29 $/30 gün |
| Jobscan | Ayda 5 tarama | 49,95 $/ay |
| Rezi | 1 CV, 3 PDF | 29 $/ay veya 149 $ ömür boyu |
| Kickresume | 4 temel CV şablonu | 19 $/ay veya yıllık 54 $ |
| Huntr | 100 ilana kadar takip | 40 $/ay |

Genel LLM'ler (ChatGPT, Claude, Gemini): ücretsiz katman mevcut.

---

# Hangi Araç Kime?

- **Yeni başlıyorum:** ücretsiz LLM + Reactive Resume
- **ATS'ye takılıyor muyum?** OpenResume ayrıştırıcı, Jobscan ücretsiz taramaları
- **Çok başvuru, takip zor:** Huntr veya Teal ücretsiz katmanı
- **Geliştiriciyim, kontrol bende olsun:** RenderCV veya LaTeX + Git + eylemci (career-ops, ai-job-search ya da kendi AGENTS.md dosyan)

---

# Riskler ve Etik

- **Uydurma:** LLM olmayan deneyim veya sayı ekleyebilir; her maddeyi doğrula
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
- LinkedIn: Muhammed Kayra Bulut · GitHub: kaayra2000
