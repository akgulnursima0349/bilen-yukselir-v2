# questions.json — Soru Ekleme Kılavuzu

Bu dosya oyundaki tüm soruları içerir. Her soru için metin zorunludur; ses, görsel ve ikon alanları tamamen **isteğe bağlıdır**.

---

## İçindekiler

1. [Temel yapı](#1-temel-yapı)
2. [Soruya ses ekleme](#2-soruya-ses-ekleme)
3. [Soruya görsel ekleme](#3-soruya-görsel-ekleme)
4. [Diyalog sorusu — birden fazla ses parçası](#4-diyalog-sorusu--birden-fazla-ses-parçası)
5. [Ses butonuna karakter ikonu ekleme](#5-ses-butonuna-karakter-ikonu-ekleme)
6. [Şıklara ses ekleme](#6-şıklara-ses-ekleme)
7. [Şıklara görsel ekleme](#7-şıklara-görsel-ekleme)
8. [Her şeyi birlikte kullanma](#8-her-şeyi-birlikte-kullanma)
9. [Dosya isimlendirme önerileri](#9-dosya-isimlendirme-önerileri)
10. [Hızlı başvuru tablosu](#10-hızlı-başvuru-tablosu)

---

## 1. Temel yapı

En sade haliyle bir soru şöyle yazılır:

```json
{
  "question": "Hangi besin grubu en fazla enerji verir?",
  "options": ["Şeker ve tatlılar", "Sağlıklı sebze ve meyveler", "Paketlenmiş abur cuburlar"],
  "correct": 0
}
```

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `question` | ✅ | Soru metni |
| `options` | ✅ | 3 şıktan oluşan dizi |
| `correct` | ✅ | Doğru şıkkın sırası (0 = birinci, 1 = ikinci, 2 = üçüncü) |

---

## 2. Soruya ses ekleme

Soru metninin yanında 🔊 butonu çıkar, basınca ses çalar.

```json
{
  "question": "Hangi besin grubu en fazla enerji verir?",
  "audio": "sounds/questions/q1.mp3",
  "options": ["Şeker ve tatlılar", "Sağlıklı sebze ve meyveler", "Paketlenmiş abur cuburlar"],
  "correct": 0
}
```

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `audio` | ❌ | Soru sesi için MP3 dosyası yolu. Yazılmazsa buton çıkmaz. |

---

## 3. Soruya görsel ekleme

Soru metninin üstünde bir resim gösterilir.

```json
{
  "question": "Resimdeki hayvan hangisidir?",
  "questionImage": "Assets/questions/aslan.png",
  "options": ["Kaplan", "Aslan", "Leopar"],
  "correct": 1
}
```

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `questionImage` | ❌ | Görselin dosya yolu (PNG, JPG, SVG). Yazılmazsa görsel çıkmaz. |

> Görsel dosyalarını `Assets/questions/` klasörüne koymanız önerilir.

---

## 4. Diyalog sorusu — birden fazla ses parçası

Soruda birden fazla kişi konuşuyorsa `audio_parts` kullanılır. Her parça için ayrı bir buton çıkar.

```json
{
  "question": "Mehmet: \"Emniyet kemeri bizi korur.\" Selin: \"Çocukların takmasına gerek yok.\" Tarık: \"Araçta yerimizden kalkmamalıyız.\" Yanlış bilgi veren kimdir?",
  "audio_parts": [
    { "audio": "sounds/questions/q5-qs1.mp3", "label": "Mehmet" },
    { "audio": "sounds/questions/q5-qs2.mp3", "label": "Selin" },
    { "audio": "sounds/questions/q5-qs3.mp3", "label": "Tarık" }
  ],
  "options": ["Mehmet", "Selin", "Tarık"],
  "correct": 1
}
```

Her parça için şu alanlar kullanılabilir:

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `audio` | ✅ | Bu parçanın ses dosyası yolu |
| `label` | ❌ | Buton üzerinde görünecek isim/yazı. Yazılmazsa sıra numarası (1, 2, 3) çıkar. |
| `icon` | ❌ | Hoparlör ikonu yerine gösterilecek resim dosyası yolu. Bir sonraki bölüme bakın. |

---

## 5. Ses butonuna karakter ikonu ekleme

`audio_parts` içindeki her parçaya `icon` eklenirse 🔊 hoparlör yerine o resim gösterilir.

```json
"audio_parts": [
  { "audio": "sounds/questions/q5-qs1.mp3", "label": "Mehmet", "icon": "Assets/icons/erkek_cocuk.png" },
  { "audio": "sounds/questions/q5-qs2.mp3", "label": "Selin",  "icon": "Assets/icons/kiz_cocuk.png" },
  { "audio": "sounds/questions/q5-qs3.mp3", "label": "Tarık"  }
]
```

- `icon` **yazılmazsa** veya `null` bırakılırsa 🔊 hoparlör çıkar — karıştırabilirsiniz.
- `icon` için önerilen klasör: `Assets/icons/`
- PNG, JPG, SVG formatları desteklenir.

---

## 6. Şıklara ses ekleme

Şıklar düz metin yerine obje olarak yazılırsa her birine ses butonu eklenebilir.

```json
{
  "question": "Doğru sözcüğü seçin.",
  "options": [
    { "text": "Çiçekçi",  "audio": "sounds/questions/q1-s1.mp3" },
    { "text": "Çörек",    "audio": "sounds/questions/q1-s2.mp3" },
    { "text": "Çadır",    "audio": null }
  ],
  "correct": 0
}
```

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `text` | ✅ | Şık metni |
| `audio` | ❌ | Şık ses dosyası. `null` yazılırsa veya hiç yazılmazsa bu şıkta ses butonu çıkmaz. |

> `audio` olan şıklarda 🔊 butonu şık metninin solunda görünür.

---

## 7. Şıklara görsel ekleme

Şıklar metin yerine veya metinle birlikte görsel içerebilir.

```json
{
  "question": "Hangisi meyve?",
  "options": [
    { "text": "Elma",  "image": "Assets/questions/elma.png" },
    { "text": "Havuç", "image": "Assets/questions/havuc.png" },
    { "text": "Ekmek", "image": "Assets/questions/ekmek.png" }
  ],
  "correct": 0
}
```

| Alan | Zorunlu | Açıklama |
|------|---------|----------|
| `text` | ✅ | Şık metni (görsel altında gösterilir) |
| `image` | ❌ | Şık görseli. Yazılmazsa yalnızca metin çıkar. |

---

## 8. Her şeyi birlikte kullanma

Tüm alanlar aynı anda kullanılabilir:

```json
{
  "question": "Diyaloğu dinleyip doğru cevabı işaretleyin.",
  "questionImage": "Assets/questions/okul_sahnesi.png",
  "audio_parts": [
    { "audio": "sounds/questions/q6-qs1.mp3", "label": "Ali",    "icon": "Assets/icons/erkek_cocuk.png" },
    { "audio": "sounds/questions/q6-qs2.mp3", "label": "Zeynep", "icon": "Assets/icons/kiz_cocuk.png"  },
    { "audio": "sounds/questions/q6-qs3.mp3", "label": "Kerem",  "icon": "Assets/icons/erkek_cocuk.png" }
  ],
  "options": [
    { "text": "Ali",    "image": "Assets/icons/erkek_cocuk.png" },
    { "text": "Zeynep", "image": "Assets/icons/kiz_cocuk.png"  },
    { "text": "Kerem",  "image": "Assets/icons/erkek_cocuk.png" }
  ],
  "correct": 1
}
```

---

## 9. Dosya isimlendirme önerileri

```
sounds/questions/q1.mp3         → 1. sorunun sesi
sounds/questions/q1-s1.mp3      → 1. sorunun 1. şıkkının sesi
sounds/questions/q5-qs1.mp3     → 5. sorunun 1. diyalog parçasının sesi

Assets/questions/soru1.png      → Soru görseli
Assets/questions/sik1.png       → Şık görseli
Assets/icons/erkek_cocuk.png    → Ses butonu için erkek çocuk ikonu
Assets/icons/kiz_cocuk.png      → Ses butonu için kız çocuk ikonu
```

---

## 10. Hızlı başvuru tablosu

| Alan | Nerede | Zorunlu | Ne yapar |
|------|--------|---------|----------|
| `question` | Soru | ✅ | Soru metni |
| `correct` | Soru | ✅ | Doğru şıkkın indeksi (0/1/2) |
| `options` | Soru | ✅ | Şık listesi |
| `audio` | Soru | ❌ | Soru ses butonu (🔊) |
| `questionImage` | Soru | ❌ | Soru görseli |
| `audio_parts` | Soru | ❌ | Diyalog ses butonları dizisi |
| `audio_parts[].audio` | Diyalog parçası | ✅* | Parçanın ses dosyası |
| `audio_parts[].label` | Diyalog parçası | ❌ | Buton yazısı (yoksa numara) |
| `audio_parts[].icon` | Diyalog parçası | ❌ | Hoparlör yerine karakter resmi |
| `options[].text` | Şık (obje) | ✅* | Şık metni |
| `options[].audio` | Şık (obje) | ❌ | Şık ses butonu |
| `options[].image` | Şık (obje) | ❌ | Şık görseli |

> \* `audio_parts` veya obje şık kullanılıyorsa zorunludur.
