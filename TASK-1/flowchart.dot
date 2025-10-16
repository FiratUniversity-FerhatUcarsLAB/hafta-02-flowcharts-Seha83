digraph ATM {
    rankdir=TB;
    node [fontname="Arial"];

    start [shape=oval, label="BAŞLA"];
    pin_input [shape=parallelogram, label="PIN'inizi giriniz"];
    increment [shape=box, label="hak = hak + 1"];
    check_pin [shape=diamond, label="girilenPIN = dogruPIN?"];
    correct_pin [shape=box, label="PIN doğru"];
    wrong_pin [shape=parallelogram, label="Hatalı PIN. Kalan hakkınız: MAX_HAK - hak"];
    check_max [shape=diamond, label="hak = MAX_HAK?"];
    block_card [shape=parallelogram, label="Kartınız bloke olmuştur"];
    stop [shape=oval, label="DUR"];
    withdraw_loop [shape=diamond, label="İşlem tekrarı (E/H)?"];
    amount_input [shape=parallelogram, label="Tutarı giriniz (20 TL katı olmalı)"];
    check_multiple [shape=diamond, label="tutar % 20 = 0?"];
    check_balance [shape=diamond, label="tutar > bakiye?"];
    check_limit [shape=diamond, label="gunlukCekilen + tutar > GUNLUK_LIMIT?"];
    withdraw [shape=box, label="bakiye = bakiye - tutar\ngunlukCekilen = gunlukCekilen + tutar"];
    output_withdraw [shape=parallelogram, label="Tutar çekildi. Kalan bakiye göster"];
    limit_exceed [shape=parallelogram, label="Günlük limit aşıldı!"];
    insufficient [shape=parallelogram, label="Yetersiz bakiye!"];
    invalid_amount [shape=parallelogram, label="Tutar 20 TL'nin katı olmalı!"];
    end [shape=oval, label="BİTİR"];
    goodbye [shape=parallelogram, label="İyi günler dileriz"];

    start -> pin_input -> increment -> check_pin;
    check_pin -> correct_pin [label="Evet"];
    check_pin -> check_max [label="Hayır"];
    check_max -> wrong_pin [label="Hayır"];
    wrong_pin -> pin_input;
    check_max -> block_card [label="Evet"];
    block_card -> stop;

    correct_pin -> amount_input;
    amount_input -> check_multiple;
    check_multiple -> invalid_amount [label="Hayır"];
    invalid_amount -> amount_input;
    check_multiple -> check_balance [label="Evet"];
    check_balance -> insufficient [label="Evet"];
    insufficient -> withdraw_loop;
    check_balance -> check_limit [label="Hayır"];
    check_limit -> limit_exceed [label="Evet"];
    limit_exceed -> withdraw_loop;
    check_limit -> withdraw [label="Hayır"];
    withdraw -> output_withdraw -> withdraw_loop;
    withdraw_loop -> amount_input [label="E"];
    withdraw_loop -> goodbye [label="H"];
    goodbye -> end;
}
