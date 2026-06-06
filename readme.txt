EfeKitap — Site Hakkında Samimi Açıklama
==========================================
Yazan: Özkan Efe Işık

Bu siteyi nasıl yaptım?
--------------------------
EfeKitap'ı sıfırdan, tek bir HTML dosyası olarak tasarladım. Yani ayrı CSS dosyası, ayrı JS dosyası yok — her şey tek çatı altında. Bunun nedeni basit: taşıması, düzenlemesi ve paylaşması çok kolay olsun istedim. Dosyayı çift tıklayıp tarayıcıda açabilirsin.

Temel Yapı
-----------
Site üç ana parçadan oluşuyor:

1. HTML (iskelet)
   Sayfanın görünür her şeyi HTML etiketleriyle yazılmış.
   Menüden kitap kartlarına, modallardan footer'a kadar her şey <div>, <span>, <button> gibi etiketler.

2. CSS (görünüm)
   <style> bloğunda yaklaşık 700+ satır CSS var.
   CSS değişkenleri (--primary, --bg, --text gibi) ile tema sistemi kurdum.
   Dark, Light, Blue ve Classic olmak üzere 4 tema var — sadece data-theme özelliğini değiştirerek geçiş yapıyor.

3. JavaScript (davranış)
   <script> bloğunda tüm site mantığı var.
   Kitap verileri (BOOKS dizisi), yazar verileri (AUTHORS), kategori verileri (CATEGORIES) burada tanımlı.
   Sepet, favoriler, kullanıcı bilgileri localStorage'da saklanıyor — böylece sayfa yenilenince kaybolmuyor.

Önemli Kod Parçaları
---------------------

CAT_FOLDERS
  Kitap kategorisini klasör adına dönüştüren sözlük.
  Örn: 'Roman' → 'roman', 'Bilim Kurgu' → 'bilimkurgu'
  Bu sayede coverUrl() fonksiyonu otomatik olarak doğru resim yolunu üretiyor.

titleSlug(t)
  Kitap adını dosya adına çeviriyor.
  Örn: "İnce Memed" → "ince-memed"
  Türkçe harfleri (ğ→g, ü→u, ş→s, ı→i, ö→o, ç→c) ASCII'ye çeviriyor.

coverUrl(id)
  Kitap ID'sini alıp resim yolunu döndürüyor.
  Örn: id=1 → "kitaplar/roman/ince-memed.jpg"
  Resim bulunamazsa tarayıcı zaten boş gösterir — hata vermez.

openModal(id) / closeModal(id)
  Modal pencerelerini açıp kapıyor.
  Modal overlay'e "open" class'ı ekleyip kaldırıyor.
  Fullscreen modallar için "fullscreen" class'ı da var.

showPage(page)
  Sayfa geçişlerini yönetiyor.
  Tüm .page-view elemanlarından "active" class'ını kaldırıp
  sadece hedef sayfaya ekliyor.

bookCard(b)
  Bir kitap verisini alıp HTML kart kodu üretiyor.
  Kapak resmi, başlık, yazar, yıldız puanı, fiyat içeriyor.

Klasör Yapısı
--------------
kitaplar/
  roman/          → Roman kategorisi kapak resimleri
  bilim/          → Bilim kitapları
  bilimkurgu/     → Bilim kurgu
  biyografi/      → Biyografi
  çocuk/          → Çocuk kitapları
  dergiler/       → Dergi kapakları
  felsefe/        → Felsefe
  kırkambar/      → Kırk ambar ürün görselleri
  kırtasiye/      → Kırtasiye ürün görselleri
  kişiselgelişim/ → Kişisel gelişim kitapları
  oyunhobi/       → Oyun ve hobi ürünleri
  psikoloji/      → Psikoloji kitapları
  sanat/          → Sanat kitapları
  tarih/          → Tarih kitapları
  yazarlar/       → Yazar fotoğrafları (küçük, daire)
  yazarlar-gorseli/ → Yazar fotoğrafları (büyük, profil)
  sozleri-yazan-yazarlarin-gorseli/ → Sözler diyarı yazar görselleri
  hero/           → Ana slider arka plan görselleri (hero1.jpg … hero5.jpg)
  siir/           → Şiir kitapları
  egitim/         → Eğitim kitapları

Resim Ekleme Kuralı
--------------------
Her kitabın resmi şu formatta olmalı:
  kitaplar/[kategori-klasörü]/[kitap-adı-slug].jpg

Kitap adı slug kuralı:
  - Küçük harf
  - Türkçe harfler ASCII'ye çevrilir (ğ→g, ü→u, ş→s, ı→i, ö→o, ç→c)
  - Boşluklar ve özel karakterler tire (-) olur
  - Örnek: "İnce Memed" → "ince-memed.jpg"
  - Örnek: "Kürk Mantolu Madonna" → "kurk-mantolu-madonna.jpg"
  - Örnek: "Şeker Portakalı" → "seker-portakali.jpg"

Tam dosya yolu örneği:
  kitaplar/roman/ince-memed.jpg
  kitaplar/tarih/sapiens.jpg
  kitaplar/bilimkurgu/dune.jpg

Fullscreen Modallar
--------------------
Dergiler, Kırtasiye, Kırk Ambar, Oyun & Hobi ve Yayıncılar bölümlerinde
"Tümüne Bak" düğmesine basıldığında açılan pencere tam ekranı kaplar.
Bu CSS ile sağlandı:
  .modal-overlay.fullscreen { padding:0; align-items:stretch }
  .modal-overlay.fullscreen .modal { border-radius:0; max-width:100%; height:100vh }

EfeAI (Yapay Zeka Asistan)
----------------------------
Sol altta yeşil WhatsApp tarzı buton ile açılıyor.
Groq API (llama-3.3-70b-versatile modeli) kullanıyor.
İnternet bağlantısı yoksa veya API yanıt vermezse yerel cevap sistemi devreye giriyor.

Temalar
--------
4 tema var: Dark (varsayılan), Light, Blue, Classic.
Navbar'daki boya paleti ikonuna tıklayarak değiştirilir.
Seçilen tema localStorage'a kaydedilir, sayfa yenilenince hatırlanır.

Kullanıcı Sistemi
------------------
Gerçek bir veritabanı yok — tüm veriler localStorage'da.
Kayıt ol, giriş yap, sepet, favoriler, okuma geçmişi hepsi tarayıcıda saklanır.
QR kod girişi henüz aktif değil, yakında gelecek.

Son Not
--------
Bu siteyi sevgiyle yaptım. Her satırını kendim yazdım, her detayı düşündüm.
Umarım seni ve ziyaretçilerini mutlu eder.

                                        — Özkan Efe Işık
