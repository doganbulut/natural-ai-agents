# Yapay Zeka Ajanı Tasarım Prensipleri

> Üretim düzeyindeki yapay zeka sistem istemlerinin analizinden türetilmiş, doğal, zeki ve güvenilir hissettiren ajanlar oluşturmak için prensipler.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Agent Skill](https://img.shields.io/badge/Agent-Skill-blue.svg)](https://agentskills.io)

🇬🇧 **[Click here for English documentation](README.md)**

## İçindekiler
- [Bu nedir?](#bu-nedir)
- [Kimin içindir?](#kimin-içindir)
- [Temel Prensipler](#temel-prensipler)
- [Hızlı Başlangıç](#hızlı-başlangıç)
- [Depo Yapısı](#depo-yapısı)
- [Bir Bakışta Prensipler](#bir-bakışta-prensipler)
- [Katkıda Bulunma](#katkıda-bulunma)
- [Metodoloji](#metodoloji)
- [Etik & Beyan](#etik--beyan)
- [Lisans](#lisans)

## Bu nedir?

Yapay zeka ajanlarının iletişimi, bağlam yönetimi ve kullanıcı etkileşimi tasarımı için **üretim analizinden türetilmiş prensipleri** yakalayan kapsamlı, açık kaynaklı bir yetenek (tekrar kullanılabilir ajan talimat seti). Üretim düzeyindeki yapay zeka sistem istemlerinin (system prompts) derinlemesine analizinden elde edilmiştir.

**Temel içgörü:** Sıradan bir yapay zeka ajanı ile harika bir ajan arasındaki fark yetenek değil, *ölçülülüktür* (restraint). Ne zaman formatlamayacağını, ne zaman kişiselleştirmeyeceğini, ne zaman aşırı açıklama yapmayacağını bilmek etkileşimlerin insani hissettirmesini sağlar.

## Kimin içindir?

- Diyalogsal ajanlar, kod asistanları veya sohbet botları geliştiren **Yapay Zeka/Makine Öğrenimi Mühendisleri**
- Yapay zeka ajanı davranış spesifikasyonlarını tanımlayan **Ürün Yöneticileri**
- Sistem istemleri (system prompts) yazan veya iyileştiren **İstem Mühendisleri (Prompt Engineers)**
- Yapay zeka etkileşim kalıplarını inceleyen **Araştırmacılar**
- İnsanlarla etkileşime giren yapay zeka ürünleri geliştiren herkes

## Temel Prensipler

### 1. 🗣️ Doğal İletişim
Aşırı formatlamayın. Madde işaretleri yerine düz yazı (düzyazı) kullanın. Kullanıcının enerjisine uyum sağlayın. Genellikle birkaç cümle yeterlidir.

### 2. 🧠 Seçici Bağlam Uygulaması
Kullanıcı verilerinin her bir parçası her yanıtta görünmemelidir. Bağlamı yalnızca yanıtı önemli ölçüde iyileştirdiğinde uygulayın.

### 3. 🔇 Sıfır Meta-Yorum (Meta-Commentary)
Veri getirme sürecinizi asla açığa vurmayın. "Hafızama göre..." yasaktır. Gerçekleri doğal bir şekilde ifade edin.

### 4. 🛡️ Hassas İçerik Koruması
Keder, sağlık sorunları veya kişisel krizleri asla proaktif olarak gündeme getirmeyin. Sadece kullanıcı konuyu açtığında dahil olun.

### 5. 🎯 Şarap Uzmanı (Sommelier) Testi
Kullanıcı bir şarap uzmanıysa ve Python hakkında bir soru soruyorsa, şarap metaforları kullanmayın. Tercihleri yalnızca alakalı olduklarında uygulayın.

### 6. 🔧 Doğal Araç Önerileri
Araçları bir satış temsilcisi gibi değil, yardımsever bir iş arkadaşı gibi önerin. Her zaman isteğe bağlı bırakın (opt-in), asla zorlamayın.

## Hızlı Başlangıç

### Ajan Yeteneği (Skill) Olarak (Önerilen)

`skills/ai-agent-design-principles/translations/tr/` dizinini ajanınızın yetenek (skill) dizinine kopyalayın:

```bash
# Gemini CLI için
cp -r skills/ai-agent-design-principles/translations/tr ~/.gemini/config/skills/ai-agent-design-principles-tr

# Claude Code için
cp -r skills/ai-agent-design-principles/translations/tr ~/.claude/skills/ai-agent-design-principles-tr

# Çapraz çalışma zamanı (Cross-runtime) için
cp -r skills/ai-agent-design-principles/translations/tr ~/.agents/skills/ai-agent-design-principles-tr
```

### Referans Kılavuzu Olarak

Ana belgeyi doğrudan okuyun:

```bash
cat skills/ai-agent-design-principles/translations/tr/SKILL.md
```

### Sistem İstemi (System Prompt) Materyali Olarak

Sistem isteminiz için belirli bölümleri ayıklayın:

```python
# Örnek: Aşırı formatlamayı önleme kurallarını ayıklayın
with open("skills/ai-agent-design-principles/translations/tr/SKILL.md") as f:
    content = f.read()
    # Ajanınızla ilgili bölümleri kullanın
```

## Depo Yapısı

```
.
├── README.md                          # İngilizce README
├── README.tr.md                       # Bu dosya
├── LICENSE                            # MIT Lisansı
├── CONTRIBUTING.md                    # Katkıda bulunma kuralları
├── CHANGELOG.md                       # Sürüm geçmişi
│
├── skills/
│   └── ai-agent-design-principles/
│       ├── SKILL.md                   # İngilizce ana yetenek belgesi
│       ├── translations/
│       │   └── tr/
│       │       └── SKILL.md           # Türkçe ana yetenek belgesi
│       └── references/
│           ├── fable5-prompt-analysis.md         
│           ├── preference-application-examples.md 
│           └── memory-system-patterns.md          
│
└── docs/
    ├── METHODOLOGY.md                 # Prensiplerin nasıl türetildiği
    ├── PRINCIPLES.md                  # Örnekler ve kültürel notlarla birlikte tam prensipler
    └── EXAMPLES.md                    # Gerçek dünya uygulama örnekleri
```

## Bir Bakışta Prensipler

| Prensip | Tek Cümlelik Özet |
|-----------|-----------|
| **Formatlama** | Açıklık için gereken asgari miktar. Düz yazı > maddeler. |
| **Ton** | Sıcak, dürüst, profesyonel. Dalkavukluk yapmayın. |
| **Meta-yorum** | Veri alımını asla ifşa etmeyin. Gerçekleri doğal bir şekilde belirtin. |
| **Hassas içerik** | Davetsiz olarak asla yüzeye çıkarmayın. Önce kullanıcı tetiklemelidir. |
| **Tercihler** | Sadece maddi olarak alakalı olduğunda uygulayın. Sommelier testi. |
| **Araç önerileri** | Doğal, isteğe bağlı, kullanıcı için asla siz seçmeyin. |
| **Arama** | Güncel olaylar için otomatik arama yapın. İçerik anahtar kelimelerini kullanın. |
| **Sınırlar** | Tespiti mekaniğini değil, prensibi açıklayın. |
| **Bağımlılık** | Aşırı bağımlılığı teşvik etmeyin. Ne zaman yönlendireceğinizi bilin. |
| **Hafıza** | Aşırı indekslemeyin. Çalışma zamanı araması ≠ insan bağı. |

## Katkıda Bulunma

Yönergeler için [CONTRIBUTING.md](CONTRIBUTING.md) dosyasına bakın. Şunları memnuniyetle karşılıyoruz:

- Kanıtlarla veya üretim deneyimiyle desteklenen yeni prensipler
- Ek örnekler (iyi/kötü yanıt çiftleri)
- Çeviriler
- Gerçek yapay zeka ajanı dağıtımlarından vaka çalışmaları
- Belirli çerçeveler için entegrasyon kılavuzları

## Metodoloji

Bu prensipler, üretim düzeyindeki yapay zeka sistem istemlerinin sistematik analizi yoluyla türetilmiştir. Metodoloji şunları içerir:

1. **Kaynak Analizi** — Gönderilen sistem istemlerinin mimarisini incelemek
2. **Kalıp Çıkarma** — Tekrarlayan tasarım kalıplarını ve anti-kalıpları (anti-patterns) belirlemek
3. **Genelleştirme** — Platforma özgü kuralları evrensel prensiplere dönüştürmek
4. **Doğrulama** — Farklı yapay zeka ajanı bağlamlarında prensipleri test etmek

Tam metodoloji için [docs/METHODOLOGY.md](docs/METHODOLOGY.md) dosyasına bakın.

## Etik & Beyan

Bu projenin prensipleri halka açık yapay zeka sistem istemlerinin analizinden türetilmiştir. Hiçbir istem metni aynen kopyalanmamıştır (verbatim). Tam etik beyan, adil kullanım pozisyonu ve sorumlu kullanım yönergeleri için [ETHICS.md](ETHICS.md) dosyasına bakın.

## Lisans

MIT Lisansı — Ayrıntılar için [LICENSE](LICENSE) dosyasına bakın.

## Teşekkürler

- Halka açık yapay zeka sistem istemlerinin analizinden türetilmiştir (bkz. [ETHICS.md](ETHICS.md))
- Yapay zeka ajanı topluluğu düşünülerek oluşturulmuştur
- [Agent Skills Specification](https://agentskills.io/specification) standardını takip eder

Bunu yararlı bulduysanız, lütfen depoyu ⭐ (yıldızlayın)!

---

*"En iyi yapay zeka ajanları görünmezdir. Gösteriş yapmadan yardım ederler, duyurmadan hatırlarlar ve ne zaman geri çekileceklerini bilirler."*
