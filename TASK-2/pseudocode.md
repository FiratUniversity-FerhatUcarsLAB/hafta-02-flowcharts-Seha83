BAŞLA

// --- 1. Kullanıcı Giriş Kontrolü ---
Ekrana "Kullanıcı adı giriniz:" yaz
kullanici_adi ← kullanıcıdan al
Ekrana "Şifre giriniz:" yaz
sifre ← kullanıcıdan al

EĞER (kullanici_adi == "admin" VE sifre == "1234") İSE
    Ekrana "Giriş başarılı!" yaz
    giriş_durumu ← true
DEĞİLSE
    Ekrana "Giriş başarısız. Tekrar deneyin." yaz
    giriş_durumu ← false
SON

EĞER (giriş_durumu == false) İSE
    PROGRAMI SONLANDIR
SON

// --- 2. Ürün Kategorileri Arasında Gezinme ---
kategori_listesi ← ["Elektronik", "Giyim", "Ev & Yaşam", "Kitaplar"]
sepet ← boş liste

TEKRAR
    Ekrana "Kategoriler:" ve kategori_listesi yaz
    Ekrana "Bir kategori seçin (çıkmak için 0 yazın):" yaz
    kategori_secimi ← kullanıcıdan al

    EĞER (kategori_secimi == 0) İSE
        ÇIK
    SON

    // Ürünleri listele
    ürün_listesi ← kategorideki ürünleri getir (örnek: ["Laptop", "Telefon", "Tablet"])
    Ekrana ürün_listesi yaz

    Ekrana "Bir ürün seçin (geri dönmek için 0 yazın):" yaz
    ürün_secimi ← kullanıcıdan al

    EĞER (ürün_secimi == 0) İSE
        DEVAM ET
    SON

    seçilen_ürün ← ürün_listesi[ürün_secimi]
    stok_miktarı ← seçilen_ürün.stok

    // --- 3. Stok Kontrolü ---
    EĞER (stok_miktarı > 0) İSE
        Ekrana "Sepete eklensin mi? (E/H)" yaz
        cevap ← kullanıcıdan al

        EĞER (cevap == "E") İSE
            sepet'e seçilen_ürün ekle
            stok_miktarı ← stok_miktarı - 1
            Ekrana "Ürün sepete eklendi." yaz
        SON
    DEĞİLSE
        Ekrana "Ürün stokta yok!" yaz
    SON

TEKRAR SONLANMA KOŞULU: kategori_secimi == 0

// --- 4. Sepeti Görüntüleme ve Düzenleme ---
TEKRAR
    Ekrana "Sepetinizdeki ürünler:" yaz
    sepeti listele (ürün_adi ve fiyat)
    toplam_tutar ← sepetteki ürünlerin fiyat toplamı

    Ekrana "Toplam: " + toplam_tutar yaz
    Ekrana "Sepetten ürün silmek ister misiniz? (E/H)" yaz
    cevap ← kullanıcıdan al

    EĞER (cevap == "E") İSE
        Ekrana "Silmek istediğiniz ürünün numarasını girin:" yaz
        ürün_no ← kullanıcıdan al
        seçilen_ürün ← sepet[ürün_no]
        sepet’ten seçilen_ürün çıkar
        Ekrana "Ürün silindi." yaz
    DEĞİLSE
        ÇIK
    SON
TEKRAR SONLANMA KOŞULU: cevap == "H"

// --- 5. İndirim Kodu Uygulama ---
Ekrana "İndirim kodunuz var mı? (E/H)" yaz
cevap ← kullanıcıdan al

indirim_tutari ← 0

EĞER (cevap == "E") İSE
    Ekrana "İndirim kodunu girin:" yaz
    kod ← kullanıcıdan al
    EĞER (kod == "INDIRIM10") İSE
        indirim_tutari ← toplam_tutar * 0.10
        Ekrana "10% indirim uygulandı." yaz
    DEĞİLSE
        Ekrana "Geçersiz kod." yaz
    SON
SON

// --- 6. Minimum 50 TL Kontrolü ---
ödenecek_tutar ← toplam_tutar - indirim_tutari

EĞER (ödenecek_tutar < 50) İSE
    Ekrana "Minimum alışveriş tutarı 50 TL olmalı!" yaz
    PROGRAMI SONLANDIR
SON

// --- 7. Kargo Ücreti Hesaplama ---
kargo_ucreti ← 0

EĞER (ödenecek_tutar >= 200) İSE
    kargo_ucreti ← 0
    Ekrana "200 TL üzeri kargo ücretsiz!" yaz
DEĞİLSE
    kargo_ucreti ← 30
    Ekrana "Kargo ücreti: 30 TL" yaz
SON

ödenecek_tutar ← ödenecek_tutar + kargo_ucreti

// --- 8. Ödeme Yöntemi Seçimi ---
Ekrana "Ödeme yöntemi seçin:"
Ekrana "1- Kredi Kartı"
Ekrana "2- Kapıda Ödeme"
ödeme_secimi ← kullanıcıdan al

EĞER (ödeme_secimi == 1) İSE
    Ekrana "Kredi kartı bilgilerini giriniz." yaz
    ödeme_yöntemi ← "Kredi Kartı"
DEĞİLSE EĞER (ödeme_secimi == 2) İSE
    ödeme_yöntemi ← "Kapıda Ödeme"
DEĞİLSE
    Ekrana "Geçersiz seçim!" yaz
    PROGRAMI SONLANDIR
SON

// --- 9. Sipariş Onayı ---
Ekrana "Sipariş Özeti:"
sepeti listele
Ekrana "Toplam: " + toplam_tutar
Ekrana "İndirim: " + indirim_tutari
Ekrana "Kargo: " + kargo_ucreti
Ekrana "Ödenecek Tutar: " + ödenecek_tutar
Ekrana "Ödeme Yöntemi: " + ödeme_yöntemi

Ekrana "Siparişi onaylıyor musunuz? (E/H)" yaz
cevap ← kullanıcıdan al

EĞER (cevap == "E") İSE
    Ekrana "Siparişiniz onaylandı! Teşekkür ederiz." yaz
DEĞİLSE
    Ekrana "Sipariş iptal edildi." yaz
SON

BİTİR
