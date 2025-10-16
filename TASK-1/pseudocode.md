BAŞLA

KONST MAX_HAK = 3
KONST GUNLUK_LIMIT = 2000
hak ← 0
dogruPIN ← 1234
gunlukCekilen ← 0
bakiye ← 5000

DÖNGÜ sonsuz
    YAZ "PIN'inizi giriniz:"
    OKU girilenPIN
    hak ← hak + 1

    EĞER girilenPIN = dogruPIN İSE
        YAZ "PIN doğru."
        ÇIK DÖNGÜDEN
    DEĞİLSE
        YAZ "Hatalı PIN. Kalan hakkınız: ", MAX_HAK - hak
    EĞER hak = MAX_HAK İSE
        YAZ "Kartınız bloke olmuştur."
        DUR
    SON
SONDÖNGÜ

DÖNGÜ işlemTekrar = "E"
    YAZ "Çekmek istediğiniz tutarı giriniz (20 TL katı olmalı):"
    OKU tutar

    EĞER tutar MOD 20 ≠ 0 İSE
        YAZ "Tutar 20 TL’nin katı olmalıdır."
        DEVAM ET DÖNGÜYE
    SON

    EĞER tutar > bakiye İSE
        YAZ "Yetersiz bakiye!"
        DEVAM ET DÖNGÜYE
    SON

    EĞER gunlukCekilen + tutar > GUNLUK_LIMIT İSE
        YAZ "Günlük çekim limitini aşıyorsunuz!"
        DEVAM ET DÖNGÜYE
    SON

    bakiye ← bakiye - tutar
    gunlukCekilen ← gunlukCekilen + tutar
    YAZ tutar, " TL çekildi."
    YAZ "Kalan bakiye: ", bakiye

    YAZ "Başka işlem yapmak ister misiniz? (E/H)"
    OKU işlemTekrar
SONDÖNGÜ

YAZ "İyi günler dileriz."
DUR

BİTİR
