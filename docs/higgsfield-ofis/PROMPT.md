# "Bu hataları yapmayın" promptu — ajan ofisini oyuna çevirmek

Videoda "sizin de aynı hatalara düşmemeniz için şöyle bir prompt hazırladım" diyeceğin metin. Her madde bugün gerçekten yaşanmış bir hatadan çıktı; altında neden öyle yazıldığı var.

## Prompt (Claude Code'a yapıştır)

```
Elimde 2D bir ajan sahnesi var (canvas, her ajan tek önden PNG, binalar boyalı PNG). Bunu
Three.js ile içinde yürünebilen bir 3B oyuna çevir. Kurallar:

1. Karakterler kart (billboard) kalsın ama 8 yönlü olsun: her karakterin dönme videosundan
   8 kare kes, arka planı temizle, hareket açısına göre kareyi seç. Kare→yön eşlemesini
   tahmin etme; kontakt şeridini çıkar, hangi karenin sola/sağa baktığını GÖREREK yaz.
2. Binaları ve ağaçları billboard YAPMA. Kart bina kamera dönünce beraber döner, yassı görünür.
   Bina ve ağaç gerçek mesh olacak: önce CC0 bir pakete (KayKit / Kenney) yerleştir, sonra
   kendi boyalı tasarımlarımı image-to-3D ile modele çevir. Boyalı tasarımın 4 açısı (ön, sol,
   arka, sağ) varsa çok-görünüm modelini kullan; tek görselden üreten daha ucuz ama ayrıntı kaybediyor.
3. Kamera üçüncü şahıs olsun: fare kamera yönünü çevirir, karakter gittiği yöne döner (yana basınca yan kare görünsün); kamera karakterden hızlı dönsün ki dönüş görülsün. Tek tuşla omuz / tepeden / gözünden kamera.
   Fare/Q/E ile geçici bakınma, yürüyünce kamera arkaya döner. Serbest orbit kamera oyun hissi vermiyor.
4. Zemine oturma: her nesnenin altına temas gölgesi, binaları 10-15 cm zemine göm, diplerine çalı/kaya.
   Gölgesiz kart havada duruyor gibi görünür.
5. Ölçek: karakter 1 birimse bina 2,5-3 birim. Kamera alçak ve yakın (2,5 birim geri, 1,5 yukarı).
6. Canlı veri: ajanların hook olay akışını (/api/olaylar) oku; PreToolUse'ta ajan istasyona
   yürüsün, üstünde iş balonu, Stop'ta evine dönsün. Sağda oyun paneli: kim çalışıyor, hangi araç,
   ne taşıyor. Yaklaşınca ajan durumunu KENDİ verisinden söylesin, uydurma cümle yok.
7. Küçük canlılık: bacadan duman, titreşen fener ışığı, ateş böcekleri, yıldız. Ucuz ama oyun yapıyor.
8. Bina kapısında Enter: o takımın terminali (olay geçmişi) açılsın.
   E tuşu şirket menüsü: takım başına "iş ver" kutusu (gerçek kuyruğa yazar ve koşuyu başlatır), bekleyen
   kuyruk, son rapor. Sadece izlemek yetmez; iş vermeden oyun değil, ekran koruyucu olur. Görev alan ajan
   önce oyuncuya yürüsün, koşu bitince rapor için yanına gelsin. Ajan kendi binasında çalışıyorsa hiç
   yürümez; iş istasyonunu ortadaki masaya taşı ki hareket görünsün.
9. Her API üretiminden önce fiyat tahmini al ve deftere yaz; deneme turlarında API çağırma,
   sadece kod. Kullandığın her paketi, modeli ve maliyeti tek bir KAYNAKLAR.md'ye yaz.
10. Her ara sürümü ayrı dosya olarak sakla (v1, v2, …) ve linklerini listele; adım adım anlatılacak.
```

## Neden böyle

| Madde | Yaşanan hata |
|---|---|
| 1 | Kare→yön tablosunu varsayımla yazdım; sağa basınca karakter sola döndü. Kontakt şeridine bakınca 2 numaralı karenin sola baktığı görüldü. |
| 2 | İlk ofis tamamen billboard'du; "binalar benimle dönüyor, yassı" şikâyeti geldi. 4 açılı kart bile çözmedi; mesh gerekti. Tripo tek görselden yan kulübeyi kaybetti, Meshy 4 açıyla korudu. |
| 3 | Serbest orbit kamera "oyun gibi değil" dedirtti; tank kontrol + arkadan takip kamerası hissi verdi. |
| 4 | Gölgesiz kartlar "havada duruyor" göründü. Gömme + gölge + dip bitkileri çözdü. |
| 5 | İlk mesh turunda pazar binası karakterden 6 kat büyük çıktı; bounding box'a göre ölçek + hedef yükseklik tablosu. |
| 6 | Statik sahne sıkıcı; asıl ilgi ajanların iş başında görünmesi. Uydurma diyalog istenmedi, olay verisinden cümle kuruldu. |
| 7 | Selma'nın isteği: "bacadan duman, ışıklara ışıltı". Birkaç sprite ile büyük fark. |
| 8 | "Binaya girince terminal açılsın" fikri; şimdilik olay geçmişi, sonra gerçek konuşma. |
| 8b | İlk canlı izlemede ajanlar "hiç yürümedi": okudukları dosyalar kendi binalarına eşleniyordu, ev = istasyon. Selma: "ekranda hiçbir şey yapamıyoruz, iş vermeliyiz, ajanlar bize gelmeli" → E menüsü + gerçek kuyruk + GorevVerildi olayı. |
| 9 | Seedance fiyatı API'den dönmüyor, formül 720×720 varsayımıyla 1,30 çıktı, gerçek 960×960 → 2,31 USD. Üç düz çizgi film ev boşa gitti (7,16 USD): sahnedeki gerçek evler neydi diye önce bakılmalıydı. |
| 10 | Video adım adım anlatılacak; sürümler kaybolursa "nereden nereye" gösterilemez. |
