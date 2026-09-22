# Adımlar — 2D sahneden oyuna (21 Eylül 2026)

Her adım ayrı bir dosya olarak duruyor; 2D sahneden başlayıp Three.js oyununa varan on aşamanın kayıtları.

| # | Adım | Ne yapıldı, ne kullanıldı |
|---|---|---|
| 0 | 2D sahne (başlangıç) | Canvas, tek önden robot PNG'leri, yedek sprite'lar. "Çirkin ama çalışıyor." |
| 1 | Galeri: karakterler 8 yön | Higgsfield API: Qwen Image 3 Edit (4 açı, 0,075 USD/görsel), Seedance 2.5 i2v dönme videosu (5 sn 960×960, ~2,31 USD), ffmpeg 8 kare, rembg arka plan. Galeri kartlarında USD rozetleri. |
| 2 | Sahnede 8 yönlü robotlar | Aynı 2D sahne; robot yürürken hareket açısına göre kare seçiyor. |
| 3 | Ofis v1: içine girilebilir harita | Three.js r160, sahne yerleşimi birebir, binalar ve robotlar kart (billboard), WASD + serbest kamera. Canlı veri yok. |
| 4 | Ofis: canlı olaylar | Olay akışı bağlandı: takım koşarken robot istasyona yürür, üstünde iş balonu; 14 robot, 11 bina. |
| 5 | v2: 4 açılı binalar, orman, panel, sohbet | Binalara Qwen Edit ile 3 ek açı (0,90 USD), Qwen t2i orman propları (0,28 USD), dalgalı arazi, temas gölgeleri, sağ oyun paneli, yaklaşınca sohbet. Kamera hâlâ serbest. |
| 6 | Oyun kamerası, boyalı kartlar | Üçüncü şahıs kamera (A/D dön, kamera arkada), bina çarpışması, ölçek. Binalar hâlâ kart: kamera dönünce beraber dönüyorlar (sorun). |
| 7 | Taslak 3B: KayKit mesh'ler ("3D verilmeden önceki hal") | KayKit Medieval Hexagon Pack 1.0 (CC0, GitHub) glTF binalar + InstancedMesh orman, MeshToonMaterial + kenar çizgisi, kapı önü ışıkları. Boyalı tasarım kayboldu → sonraki adım. |
| 8 | Higgsfield 3D denemesi (kule) | Boyalı kulenin 4 açısından Meshy multi-image (30 kredi) ve tek görselden Tripo H3.1 (9 kredi). Yan yana karşılaştırma. |
| 9 | Kendi tasarımlarımız 3B, haritada | Meshy multi-image ile 4 bina (4'er açı) + tek görselden uzun çam, yapraklı ağaç, çalı; 219 kredi. Kuyu ve kayalar KayKit. Bacadan duman, titreşen ışık ve hale, Enter ile bina terminali (takımın olay geçmişi), yaklaşınca sohbet. |
| 10 | Masa, ajanın sorusu, zıplama (son hâl, 22 Eyl sabah) | Kuyu yerine boyalı çalışma masası (Qwen t2i 2k 0,075 USD → rembg → Meshy image-to-3D 30 kredi). Ajan sorusu: bekleyen bir soru varsa ajan oyuncuya yürür, panel açılır → cevap kuyruğa yazılır, koşu başlar. Space zıplama; menü perde + açılma animasyonu, ↑↓ kaydırma. |

Kütüphaneler ve lisanslar: [`KAYNAKLAR.md`](KAYNAKLAR.md). Maliyet defteri Selma'nın kendi altyapısında ayrıca tutulur (bu repoda değil).
