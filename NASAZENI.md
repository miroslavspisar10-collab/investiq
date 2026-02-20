# InvestIQ — Nasazení na Vercel (zdarma, ~5 minut)

## Co tato architektura dělá
- Frontend (index.html) volá `/api/claude` — tvůj vlastní server
- Server (`api/claude.js`) drží API klíč bezpečně jako environment variable
- Uživatelé nikdy neuvidí klíč, ani ve zdrojovém kódu

---

## Krok 1 — GitHub (2 minuty)

1. Jdi na **github.com** → přihlás se nebo vytvoř účet
2. Klikni **New repository** (zelené tlačítko)
3. Název: `investiq` → klikni **Create repository**
4. Na stránce repozitáře klikni **uploading an existing file**
5. Nahraj tyto soubory (zachovej strukturu složek):
   ```
   investiq/
   ├── api/
   │   └── claude.js
   ├── public/
   │   └── index.html
   ├── package.json
   └── vercel.json
   ```
6. Klikni **Commit changes**

---

## Krok 2 — Vercel (2 minuty)

1. Jdi na **vercel.com** → přihlás se přes GitHub
2. Klikni **Add New → Project**
3. Vyber svůj `investiq` repozitář → klikni **Import**
4. Vercel automaticky detekuje nastavení — klikni **Deploy**
5. Počkej ~30 sekund → dostaneš URL (např. `investiq-xyz.vercel.app`)

---

## Krok 3 — Přidat API klíč (1 minuta)

1. V Vercelu jdi do svého projektu → **Settings → Environment Variables**
2. Přidej:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-api03-...` (tvůj nový klíč z console.anthropic.com)
   - **Environment:** Production, Preview, Development (zaškrtni vše)
3. Klikni **Save**
4. Jdi do **Deployments** → klikni **Redeploy** (klíč se načte)

---

## Hotovo! ✅

Aplikace běží na `https://investiq-xyz.vercel.app`
- Všichni návštěvníci mají přístup k AI bez zadávání klíče
- Klíč je bezpečně skrytý na serveru
- Vercel free tier: 100GB bandwidth/měsíc, neomezené requesty

---

## Volitelné — vlastní doména

1. V Vercelu: **Settings → Domains → Add Domain**
2. Zadej svou doménu (např. `investiq.cz`)
3. Nastav DNS záznamy podle instrukcí Vercelu

---

## Monitoring nákladů Anthropic

Sleduj využití na **console.anthropic.com/usage**
Nastav spending limit: **Settings → Billing → Usage limits**
Doporučený limit pro začátek: $20/měsíc

---

## Struktura projektu

```
investiq/
├── api/
│   └── claude.js        ← Backend proxy (klíč zde bezpečný)
├── public/
│   └── index.html       ← Celá frontend aplikace
├── package.json         ← Node.js konfigurace
└── vercel.json          ← Vercel routing konfigurace
```
