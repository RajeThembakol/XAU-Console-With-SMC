# XAU Console – Android APK

Proyek ini membungkus `www/index.html` (kode Anda) menjadi aplikasi Android memakai Capacitor.

## Cara 1 – Tanpa install apa pun (GitHub Actions, paling mudah)
1. Buat akun di github.com → **New repository** (boleh private).
2. Upload **semua isi folder ini** (termasuk folder `.github`) ke repository tersebut.
3. Buka tab **Actions** → workflow **Build APK** → tunggu ±5–8 menit sampai hijau.
   (Kalau tidak jalan otomatis: klik **Run workflow**.)
4. Klik run yang selesai → bagian **Artifacts** → unduh **XAU-Console-debug-apk**.
5. Ekstrak zip-nya → `app-debug.apk` → kirim ke HP → install
   (izinkan "Install dari sumber tidak dikenal").

## Cara 2 – Di komputer sendiri
Syarat: Node.js 20+, JDK 17, Android Studio (Android SDK terpasang).
```bash
npm install
npx cap add android
npx --yes @capacitor/assets generate --android --iconBackgroundColor '#0b0e14'
npx cap sync android
cd android && ./gradlew assembleDebug      # Windows: gradlew.bat assembleDebug
```
APK ada di `android/app/build/outputs/apk/debug/app-debug.apk`.
Atau `npx cap open android` lalu Build → Build APK(s) di Android Studio.

## Memperbarui isi aplikasi
Edit `www/index.html`, lalu build ulang (push ke GitHub / `npx cap sync android` + gradle).

## Untuk Google Play
APK debug hanya untuk dipasang langsung. Untuk Play Store buat keystore lalu
build **release** (`./gradlew bundleRelease`) dan tanda-tangani AAB.

## Catatan
- Aplikasi butuh internet (data harga Binance, widget TradingView, Tailwind CDN).
- Ganti `appId`/`appName` di `capacitor.config.json` bila perlu.
