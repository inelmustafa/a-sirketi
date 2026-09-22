# Kaynaklar — "Higgsfield API ile Ajan Oyunu" (21 Eylül 2026)

Videoda geçen, kaynakçaya girecek her şey. Rakamlar Selma'nın kendi maliyet defterinden.

## Higgsfield API ile üretilenler (console anahtarı, abonelik kredisi yok)

| Ne | Model / endpoint | Adet | USD |
|---|---|---|---|
| X İçerik 4 açı (ön, sol, arka, sağ) | `alibaba/qwen-image-3/edit` 2k | 7 (3'ü yeniden) | 0,525 |
| 5 karakter dönme videosu (8 yön sprite) | `bytedance/seedance-2.5/image-to-video` 5 sn 720p | 5 | 5 × 2,311 = 11,56 (formül, API fiyat dönmüyor) |
| 3 düz çizgi film ev (kullanılmadı) | `alibaba/qwen-image-3/text-to-image` 2k + seedance i2v | 3+3 | 7,16 |
| 4 sahne binasının 3 ek açısı | `alibaba/qwen-image-3/edit` 2k | 12 | 0,90 |
| Orman propları (3 ağaç, çalı, kaya, fener) + zemin dokusu | `alibaba/qwen-image-3/text-to-image` 1k | 7 | 0,28 |
| Çalışma masası (fener, defter, tüy kalem, tabure) — 22 Eyl sabah | `alibaba/qwen-image-3/text-to-image` 2k | 1 | 0,075 |

Toplam (22 Eyl sabah): **20,50 USD**, 39 istek (1 hata, ücretlendirilmedi), tek anahtar. Kling 2.5 Turbo Pro i2v karşılaştırma tahmini: 0,298 USD / 5 sn.

## Higgsfield 3D (abonelik kredisi, MCP üzerinden) — 21 Eyl gece denemesi

| Ne | Model | Kredi |
|---|---|---|
| Kule, 4 açıdan (deneme) | Meshy `multi_image_to_3d` (dokulu) | 30 |
| Kule, tek görsel (deneme, elendi: yan kulübe kayboldu, 41 MB) | Tripo H3.1 `tripo_h3_1_image_to_3d` | 9 |
| Bekçi kulesi, sinema, şirket kabini, 4'er açıdan | Meshy `multi_image_to_3d` (dokulu) | 3 × 30 = 90 |
| Uzun çam, yapraklı ağaç, çalı, tek görselden | Meshy `image_to_3d` (dokulu) | 3 × 30 = 90 |
| Çalışma masası, tek görselden (22 Eyl sabah; kuyunun yerine) | Meshy `image_to_3d` (dokulu) | 30 |

Toplam 249 kredi; bakiye 1087 → 838 (Plus). Meshy seçildi çünkü 4 açıyı girdi alıp yan kulübe, kapı ışığı gibi ayrıntıları koruyor.

## Açık kaynak paketler ve araçlar

| Kaynak | Lisans | Nerede kullandık |
|---|---|---|
| [KayKit Medieval Hexagon Pack 1.0](https://github.com/KayKit-Game-Assets/KayKit-Medieval-Hexagon-Pack-1.0) — Kay Lousberg | CC0 | Ofiste binalar (tower_A/B, tavern, market; well = masa taslağı) ve orman (tree_single_A/B, trees_A_small, trees_B_small, rock_single_A). |
| [Three.js r160](https://threejs.org) | MIT | ofis sahnesi, GLTFLoader, InstancedMesh, MeshToonMaterial |
| [rembg](https://github.com/danielgatis/rembg) (u2net) | MIT | sprite karelerinin ve propların arka plan temizliği |
| [FFmpeg 8.1](https://ffmpeg.org) | LGPL/GPL | dönme videosundan 8 kare kesimi |
| [pixel-agents](https://github.com/pixel-agents-hq/pixel-agents) | MIT | sahnedeki yedek pixel karakterler |
| Sahne binaları | fal nano-banana-pro + birefnet v2 | ofis sahnesinin kart sürümü |
| Robot çizimleri | fal nano-banana-pro (aynı üretim yöntemi) | 8 yön sprite'ların referansı |

## Kendi yazdıklarımız

- Oyun (üçüncü şahıs kamera, tank kontrol, canlı olay akışı, sohbet, sağ panel, orman, mesh binalar) — sürüm sürüm (v1 statik → v4 mesh binalarla) geliştirildi.
- Anlatım tahtası ve adım haritası — video çekimi için ekran görüntüleri alındı.
- Galeri sayfası (2D → 8 yön → 3D kartlar, USD rozetleri).
- Higgsfield API üretim scriptleri: fiyat tahmini → üretim → deftere kayıt hattını kullanan yardımcı script'ler (4 açı, dönme videosu, ev, bina açıları, orman üretimi).
- Video → 8 kare + arka plan temizleme script'i; galeriyi defterden dolduran script; başsız tarayıcı ile ekran görüntüsü alma script'i.
- Higgsfield API istemcisi (User-Agent, S3 upload başlıkları, token formülü, defter kilidi) — Selma'nın kendi altyapısında, bu repoda değil.
- 8 yönlü robot sahnesi ve sunucusu — Selma'nın kendi altyapısında, bu repoda değil.

## Araştırırken bulunan, henüz kullanılmayan (videoda "bakın, bunlar da var")

- [Kenney Fantasy Town Kit](https://kenney.nl/assets/fantasy-town-kit) — CC0, 160+ modüler parça (glTF).
- [Quaternius Medieval Village MegaKit](https://quaternius.com/packs/medievalvillagemegakit.html) — CC0, 300+ modüler parça; [poly.pizza](https://poly.pizza) üzerinden GLB.
- [KayKit Character Pack: Adventurers](https://github.com/KayKit-Game-Assets/KayKit-Character-Pack-Adventures-1.0) — rig'li, animasyonlu karakterler (bizim robotlar kart kaldı, karşılaştırma için).
- [KenneyNL/KayKit-Hexagons](https://github.com/KenneyNL/KayKit-Hexagons) — aynı paketle altıgen harita üretimi örneği.
