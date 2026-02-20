# 🔧 Oprava PWA pro GitHub Pages - Evidence-prace-v2

## ✅ Co jsem opravil

### 1. **Cesty v HTML souborech**
- Manifest: `/Evidence-prace-v2/manifest_arnost.json`
- Service Worker: `/Evidence-prace-v2/service-worker.js`
- Ikony: `/Evidence-prace-v2/icon-192-arnost.png`

### 2. **Cesty v manifest.json**
- `start_url`: `/Evidence-prace-v2/arnost_pwa.html`
- `icons.src`: `/Evidence-prace-v2/icon-192-arnost.png`

### 3. **Cesty v service-worker.js**
- Všechny cached soubory mají prefix `/Evidence-prace-v2/`

## 📋 Co musíte udělat

### KROK 1: Nahrajte opravené soubory na GitHub

Nahraďte tyto soubory novými verzemi:

**Pro Arnošta:**
- ✅ `arnost_pwa.html` (opravený)
- ✅ `manifest_arnost.json` (opravený)

**Pro Ivana:**
- ✅ `ivan_pwa.html` (opravený)
- ✅ `manifest_ivan.json` (opravený)

**Pro Víťu:**
- ✅ `vita_pwa.html` (opravený)
- ✅ `manifest_vita.json` (opravený)

**Společné:**
- ✅ `service-worker.js` (opravený)

### KROK 2: Vyčistěte cache

Po nahrání nových souborů:

1. Otevřete aplikaci v Chrome na mobilu
2. Menu (⋮) → **Nastavení**
3. **Soukromí a zabezpečení** → **Vymazat data prohlížení**
4. Zaškrtněte:
   - ✅ Soubory cookie a data webu
   - ✅ Obrázky a soubory uložené v mezipaměti
5. Klikněte **Vymazat data**
6. **Zavřete a znovu otevřete Chrome**

### KROK 3: Znovu navštivte aplikaci

1. Otevřete: `https://ldurcak-lang.github.io/Evidence-prace-v2/arnost_pwa.html`
2. **Mělo by se objevit zelené tlačítko "Instalovat"** 📲
3. Klikněte a nainstalujte!

## 🔍 Jak ověřit, že to funguje

### Chrome DevTools kontrola:

1. Otevřete stránku v Chrome (desktop nebo mobil)
2. Stiskněte **F12** (nebo dlouhý stisk → Zkontrolovat)
3. Záložka **Application**

#### Kontrola 1: Service Worker
- **Application → Service Workers**
- ✅ Měli byste vidět: `service-worker.js` - **Activated and running**

#### Kontrola 2: Manifest
- **Application → Manifest**
- ✅ Měli byste vidět:
  - Name: "Evidence práce - Arnošt"
  - Start URL: `/Evidence-prace-v2/arnost_pwa.html`
  - Icons: 2 ikony (192x192, 512x512)
  - ✅ **Žádné chyby!**

#### Kontrola 3: Install Prompt
- V horní části stránky by se mělo zobrazit:
  - 📲 **Zelený banner "Nainstalovat aplikaci"**
  - Nebo ikona instalace v address baru ⊕

## ⚠️ Pokud stále nefunguje

### Problém 1: "Service Worker se neregistruje"

**Řešení:**
```javascript
// Otevřete Console v DevTools a spusťte:
navigator.serviceWorker.getRegistrations().then(registrations => {
  registrations.forEach(reg => reg.unregister());
  console.log('All service workers unregistered');
});
// Pak obnovte stránku (F5)
```

### Problém 2: "Manifest se nenačítá"

**Zkontrolujte:**
- Otevřete: `https://ldurcak-lang.github.io/Evidence-prace-v2/manifest_arnost.json`
- Měli byste vidět JSON (ne 404 chybu)
- Zkontrolujte, že všechny cesty začínají `/Evidence-prace-v2/`

### Problém 3: "Ikony se nenačítají"

**Zkontrolujte:**
- `https://ldurcak-lang.github.io/Evidence-prace-v2/icon-192-arnost.png` ✅
- `https://ldurcak-lang.github.io/Evidence-prace-v2/icon-512-arnost.png` ✅
- Měly by se zobrazit obrázky (ne 404)

### Problém 4: "Stále žádné tlačítko Install"

**GitHub Pages cache:**
- GitHub Pages může cachovat soubory až 10 minut
- Počkejte 10 minut po nahrání
- Nebo přidejte `?v=2` na konec URL:
  - `arnost_pwa.html?v=2`

## 📱 Test na mobilu

### Android Chrome:

1. Otevřete URL na mobilu
2. **Mělo by se stát jedno z:**
   - ✅ Zelený banner "Instalovat aplikaci" se zobrazí
   - ✅ V menu (⋮) je možnost "Instalovat aplikaci"
   - ✅ V address baru je ikona ⊕

### Pokud nic z toho:

**Hard refresh:**
1. Chrome menu → Nastavení
2. Soukromí → Vymazat data
3. Zavřít Chrome úplně (recent apps → swipe)
4. Znovu otevřít a navštívit URL

## 🎯 Checklist před distribucí

Než pošlete odkazy pracovníkům:

- [ ] Service Worker je "Activated and running"
- [ ] Manifest se načítá bez chyb
- [ ] Ikony se načítají (192x192 a 512x512)
- [ ] Install banner/tlačítko se zobrazuje
- [ ] Instalace funguje (zkuste nainstalovat)
- [ ] Aplikace se otevírá na celou obrazovku
- [ ] Data se ukládají do Google Sheets
- [ ] Offline režim funguje (vypněte internet, otevřete app)

## 💡 Tipy

### Pro rychlejší vývoj:

**Disable cache v Chrome:**
1. DevTools (F12)
2. Network tab
3. ✅ Zaškrtněte "Disable cache"
4. Nechte DevTools otevřené

### Pro testování instalace:

**Reset PWA instalace:**
1. Chrome → Settings → Apps
2. Najděte "Evidence - Arnošt"
3. Uninstall
4. Zkuste znovu nainstalovat

### Pro debugging:

**Console log v Service Worker:**
```javascript
// V service-worker.js přidejte:
console.log('SW: Installing...');
console.log('SW: Caching files:', urlsToCache);
```

## 📞 Support

Pokud máte problémy:

1. **Kontrola 1:** DevTools → Application → zkontrolujte Service Worker a Manifest
2. **Kontrola 2:** Vyčistěte cache a zkuste znovu
3. **Kontrola 3:** Počkejte 10 minut (GitHub Pages cache)
4. **Kontrola 4:** Zkuste jiný prohlížeč (Chrome Canary, Edge)

## ✅ Potvrzení funkčnosti

Po nahrání opravených souborů byste měli vidět:

```
✅ https://ldurcak-lang.github.io/Evidence-prace-v2/arnost_pwa.html
   → Zelený banner "Instalovat aplikaci" 📲
   → Nebo ikona ⊕ v address baru
   
✅ Chrome DevTools → Application → Manifest
   → Name: Evidence práce - Arnošt
   → Start URL: /Evidence-prace-v2/arnost_pwa.html ✓
   → Icons: 2 ✓
   
✅ Chrome DevTools → Application → Service Workers
   → service-worker.js - Activated and running ✓
```

---

**Po nahrání těchto opravených souborů by instalace měla fungovat! 🎉**
