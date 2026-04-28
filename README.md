# WooDr — Statická webstránka

Stolárska webstránka vyrobená v čistom HTML + CSS + Vanilla JS. Žiadne frameworky, žiadne build tools okrem jednoduchého bash skriptu na generovanie zoznamu obrázkov.

---

## Štruktúra projektu

```
/
├── index.html              — Celá stránka (CSS + JS inline)
├── build.sh                — Skript na regeneráciu gallery-data.js
├── netlify.toml            — Konfigurácia Netlify deployu
├── images/
│   ├── hero/               → Fotky pre hero sekciu (rotujú náhodne)
│   ├── galeria/            → Galéria hotových prác (hlavná sekcia)
│   ├── showcase/           → Ďalšie ukážky prác (aj tie sa zobrazia v galérii)
│   ├── o-mne/              → Fotky pre sekciu "O mne" (použije sa náhodná)
│   ├── proces/             → Fotky pre sekciu "Proces" (max 3)
│   └── sluzby/             → Fotky pre sekciu "Služby" (fáza 2)
├── generated/
│   └── gallery-data.js     → AUTO-GENERATED — neupravovať ručne!
└── README.md
```

---

## Správa fotografií

### Pridanie fotiek

1. Skopíruj obrázky do správneho podpriečinka v `images/`
2. Spusti build skript:
   ```bash
   bash build.sh
   ```
3. Hotovo — `generated/gallery-data.js` sa automaticky aktualizuje.

### Odporúčané formáty a rozmery

| Priečinok   | Odporúčaný rozmer | Formát       |
|-------------|-------------------|--------------|
| `hero/`     | 1920 × 1080 px    | JPG / WebP   |
| `galeria/`  | 1200 × 900 px     | JPG / WebP   |
| `showcase/` | 1200 × 900 px     | JPG / WebP   |
| `o-mne/`    | 800 × 1100 px     | JPG / WebP   |
| `proces/`   | 1200 × 800 px     | JPG / WebP   |

**Tip:** Pre rýchlejšie načítanie používaj WebP formát a komprimuj fotky na max 300–500 KB.

### Placeholder systém

Kým nie sú nahrané skutočné fotky, každé miesto kde chýba obrázok zobrazí:
- Tmavohnedý obdĺžnik s jemným wood-grain vzorom
- Text "WooDr" v strede
- **Žiadne škaredé "broken image" ikony**

---

## Lokálny vývoj

```bash
# 1. Generuj gallery-data.js
bash build.sh

# 2. Spusti lokálny server (Python 3)
python3 -m http.server 3000

# alebo (Node.js)
npx serve .
```

Otvor `http://localhost:3000` v prehliadači.

> **Dôležité:** Stránka musí bežať cez HTTP server, nie cez `file://` — kvôli načítaniu `generated/gallery-data.js`.

---

## Deployment na Netlify

1. Pushni repo na GitHub
2. Prepoj repo s Netlify
3. Netlify automaticky spustí `bash build.sh` pred každým deployom
4. Publish directory: `.` (koreň projektu)

Konfigurácia je v `netlify.toml` — **nič netreba meniť**.

### Aktualizácia fotiek na produkcii

1. Pridaj/zmeň fotky v `images/`
2. Commitni a pushni
3. Netlify automaticky rebuilduje a deployuje

---

## Fázy vývoja

- [x] **Fáza 1** — Štruktúra, dizajn systém, build skript, placeholder systém
- [ ] **Fáza 2** — Obsah sekcií (texty, ikony, kontaktné údaje)
- [ ] **Fáza 3** — SEO, meta tagy, Open Graph, kontaktný formulár

---

## Technické detaily

- **Farby:** Len 4 farby + odtiene (`--cream`, `--warm`, `--accent`, `--dark`)
- **Písmo:** DM Serif Display (nadpisy) + DM Sans (body text) — Google Fonts
- **Breakpointy:** Mobile-first, hlavný breakpoint na `960px`
- **Animácie:** CSS transitions + IntersectionObserver reveal (žiadne knižnice)
- **Galéria:** CSS Grid s nepravidelným masonry vzorcom, lightbox v čistom JS
