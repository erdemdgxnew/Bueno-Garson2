BUENO GARSON APK - ANDROID STUDIO GEREKMEDEN GITHUB ILE APK URETME

Hazir bilgiler:
- Site: https://buenofoca.com/
- Panel girisi: https://buenofoca.com/login.php
- Uygulama adi: Bueno Garson
- Android paket adi: com.bueno.garson
- Garson girisleri mevcut yoneticiler tablosundan calisir.

1) FIREBASE KURULUMU

1. Firebase Console'a girin.
2. Yeni proje olusturun. Ornek ad: Bueno Garson
3. Android uygulamasi ekleyin.
4. Paket adi olarak sunu yazin:
   com.bueno.garson
5. Uygulama adi:
   Bueno Garson
6. google-services.json dosyasini indirin.
7. Bu dosyayi Android projesinde app/google-services.json olarak yukleyin.

Sunucu icin ayrica:
1. Firebase Console > Project Settings > Service accounts.
2. Generate new private key deyin.
3. Inen dosyayi firebase-service-account.json olarak adlandirin.
4. cPanel'de public_html icine veya public_html'in bir ust klasorune koyun.

2) CPANEL'E YUKLENECEK PHP DOSYALARI

php_api klasorunun ICINDEKI dosyalari public_html icine yukleyin:

api_helpers.php
api_garson_login.php
api_fcm_token_kaydet.php
api_cagri_liste.php
api_cagri_kabul.php
api_firebase_test.php
firebase_gonder.php
firebase-service-account.json

Onemli: api_helpers.php, baglan.php dosyasini ayni klasorde arar. Bu yuzden dosyalari public_html icine, baglan.php ile ayni yere koymak en kolay yoldur.

3) INDEX.PHP ICINE BILDIRIM SATIRI EKLEME

Musteri masa cagirisini INSERT INTO cagrilar ile kaydettigin yerde, kayit basarili olduktan sonra sunu ekleyin:

require_once __DIR__ . '/firebase_gonder.php';
masaCagrisiFirebaseGonder($db, $gelenMasa);

Eger elinizde cagri id varsa daha iyi:

require_once __DIR__ . '/firebase_gonder.php';
masaCagrisiFirebaseGonder($db, $gelenMasa, $db->lastInsertId());

Buradaki $gelenMasa sizin index.php dosyanizdaki masa kodu degiskenidir. Onceki duzenlemede bu genellikle $gelenMasa olarak kullanilmisti.

4) GITHUB ILE APK URETME

1. GitHub'da yeni repository olusturun.
2. Bu paketin icindeki Android proje dosyalarini yukleyin.
3. Firebase'den indirdiginiz google-services.json dosyasini app/ klasorune koyun.
4. GitHub > Actions sekmesine girin.
5. Build Bueno Garson APK workflowunu calistirin.
6. Islem bitince Artifacts kismindan Bueno-Garson-debug-apk dosyasini indirin.
7. Icindeki app-debug.apk dosyasini garson telefonlarina kurun.

5) TELEFONDA ILK CALISTIRMA

1. APK'yi kurun.
2. Uygulamayi acin.
3. Paneldeki garson kullanici adi ve sifresiyle giris yapin.
4. Android bildirim iznini verin.
5. Bu giristen sonra uygulama FCM tokenini sunucuya kaydeder.
6. Masa cagirilinca APK bildirim alir, ozel alarm sesi ve titresim calisir.

6) NOTLAR

- Bu APK debug APK'dir. Kurulum icin telefonda bilinmeyen kaynaklara izin gerekebilir.
- Play Store'a koymak isterseniz release imzalama gerekir.
- Ekran kapaliyken web/PWA'dan daha kararli calisir, cunku Firebase Cloud Messaging kullanir.
- Android'in pil tasarrufu cok agresifse, garson telefonunda uygulama icin pil kisitlamasini kapatmak yine faydalidir.
