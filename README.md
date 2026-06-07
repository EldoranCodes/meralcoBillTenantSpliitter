# Meralco Bill Splitter

Split a main meter bill across 4 tenants with nested submeter hierarchy.

## Meter Structure

```
Main Meter
├── Submeter 1: Cel        (direct reading)
└── Submeter 2: Vic        (includes subtenants)
    ├── Sub: Zyville       (nested under Vic)
    └── Sub: Freda         (nested under Vic)
```

## How It Works

```
rate = mainBill / mainKwh

cel     = cel_new - cel_old
zyville = zyville_new - zyville_old
freda   = freda_new - freda_old
vic     = (vic_new - vic_old) - zyville - freda

diff  = mainKwh - (cel + zyville + freda + vic)
adjust = diff / 4   (equally distributed)

bill = (consumption + adjust) × rate
```

## File Structure

```
├── index.html            App (open in any browser)
├── src/input.css         Tailwind source
├── styles/output.css     Built CSS (generated)
├── www/                  Web copy for APK (generated)
├── android/              Android project (generated)
├── capacitor.config.json Capacitor config
├── tailwind.config.js    Tailwind config
├── package.json          Scripts + dependencies
└── MeralcoBillSplitter.apk  Built APK (generated)
```

## Run as Web

Open `index.html` directly in a browser — no server needed.

Or serve locally:
```bash
npx serve .
# or
python3 -m http.server 8080
```

## Requirements to Build APK

- **Node.js** v18+ — [nodejs.org](https://nodejs.org)
- **JDK** 17+ — `sudo apt install openjdk-17-jdk`
- **Android SDK** — command-line tools + platform 35 + build-tools 35.0.0

## Build APK

```bash
# 1. Install dependencies
npm install

# 2. Build Tailwind CSS
npm run build:css

# 3. Copy web files to www/
npm run build:www

# 4. Sync Capacitor
npx cap sync

# 5. Build APK
cd android && ./gradlew assembleDebug
```

APK output: `android/app/build/outputs/apk/debug/app-debug.apk`

### Quick build (all steps)
```bash
npm run build:apk
```

## After Making Changes

1. Edit `index.html`
2. Rebuild: `npm run build:css && npm run build:www && npx cap sync`
3. Open in Android Studio: `npx cap open android`
4. Or build from CLI: `cd android && ./gradlew assembleDebug`

## Install on Phone

1. Copy `MeralcoBillSplitter.apk` to the phone
2. Enable **Install from unknown sources** in Settings → Security
3. Open the APK file and tap Install
4. No internet connection needed — the app works fully offline
