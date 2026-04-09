# Ses Dosyaları

Bu klasöre soru ve şık ses dosyalarını (.mp3) ekleyin.

---

## Temel soru yapısı (ses YOK)

Şu an questions.json dosyasındaki sorular böyle görünüyor:

```json
{
  "question": "Hecelerine doğru şekilde ayrılan sözcük hangisidir?",
  "options": ["Çiç-ek-çi", "Çör-ek", "Ça-dır"],
  "correct": 2
}
```

`audio` alanı yazılmamışsa ses butonu çıkmaz. Yazmak zorunda değilsiniz.

---

## Soruya ses eklemek

`audio` alanını sorunun içine ekleyin:

```json
{
  "question": "Hecelerine doğru şekilde ayrılan sözcük hangisidir?",
  "audio": "sounds/questions/q1.mp3",
  "options": ["Çiç-ek-çi", "Çör-ek", "Ça-dır"],
  "correct": 2
}
```

Soru metninin yanında 🔊 butonu çıkar, basınca ses çalar.

---

## Şıklara ses eklemek

Şıkları düz metin yerine obje olarak yazın ve `audio` ekleyin:

```json
{
  "question": "Hecelerine doğru şekilde ayrılan sözcük hangisidir?",
  "options": [
    { "text": "Çiç-ek-çi", "audio": "sounds/questions/q1_a1.mp3" },
    { "text": "Çör-ek",    "audio": "sounds/questions/q1_a2.mp3" },
    { "text": "Ça-dır",    "audio": "sounds/questions/q1_a3.mp3" }
  ],
  "correct": 2
}
```

Her şıkkın solunda küçük 🔊 butonu çıkar. Bazı şıklarda ses olup bazılarında olmayabilir, karıştırabilirsiniz.

---

## Konuşma balonlu soru (birden fazla ses parçası)

Soru birden fazla konuşma içeriyorsa `audio_parts` kullanın. Her parça için `label` (buton yazısı) ve isteğe bağlı `icon` (resim dosyası yolu) ekleyebilirsiniz:

```json
{
  "question": "...",
  "audio_parts": [
    { "audio": "sounds/questions/q5-qs1.mp3", "label": "Mehmet" },
    { "audio": "sounds/questions/q5-qs2.mp3", "label": "Selin" },
    { "audio": "sounds/questions/q5-qs3.mp3", "label": "Tarık" }
  ],
  "options": ["Mehmet", "Selin", "Tarık"],
  "correct": 1
}
```

`icon` alanıyla hoparlör ikonu yerine karakter resmi kullanabilirsiniz:

```json
{
  "audio_parts": [
    { "audio": "sounds/questions/q5-qs1.mp3", "label": "Mehmet", "icon": "Assets/icons/boy.png" },
    { "audio": "sounds/questions/q5-qs2.mp3", "label": "Selin",  "icon": "Assets/icons/girl.png" },
    { "audio": "sounds/questions/q5-qs3.mp3", "label": "Tarık"  }
  ]
}
```

- `icon` yazılmazsa veya `null` bırakılırsa 🔊 hoparlör ikonu çıkar
- `icon` bir resim dosyası yoluysa (PNG, SVG vb.) hoparlör yerine o resim gösterilir
- Resim dosyalarını `Assets/icons/` klasörüne koymanız önerilir

---

## Önerilen dosya isimlendirmesi

```
q1.mp3          → 1. sorunun sesi
q1_a1.mp3       → 1. sorunun 1. şıkkının sesi
q1_a2.mp3       → 1. sorunun 2. şıkkının sesi
q1_a3.mp3       → 1. sorunun 3. şıkkının sesi
q3_parca1.mp3   → 3. sorunun 1. konuşma balonunun sesi
q3_parca2.mp3   → 3. sorunun 2. konuşma balonunun sesi
```

---

## Önemli notlar

- Ses dosyası bu klasörde olmalı: `sounds/questions/`
- `audio` alanı hiç yazılmazsa veya `null` yazılırsa ses butonu çıkmaz
- Bir ses çalarken başka bir butona basılırsa önceki ses durur
- Cevap verilince veya süre dolunca ses otomatik durur
