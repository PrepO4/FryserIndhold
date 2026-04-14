# FryserApp — Projektnotater

## Formål
Ny app bygget med samme teknologistak som Preplager-appen (`C:\Users\Lone\kode\Preplager\index.html`).
Indhold og nye features aftales ved næste session.

---

## Reference-app: Preplager
Kildekode: `C:\Users\Lone\kode\Preplager\index.html`
GitHub: https://github.com/PrepO4/FryserIndhold.git

Preplager er en lagerstyring for tørre fødevarer med udløbsdato-tracking.

---

## Teknologistak (genbrug fra Preplager)

### Arkitektur
- **Én enkelt HTML-fil** — ingen build-tools, ingen frameworks
- Kører direkte i browseren og som PWA på iPhone
- Data i skyen via JSONBin.io REST API
- AI-billedanalyse via Cloudflare Worker → Claude AI

### Data-lag: JSONBin.io
- REST API til at gemme JSON-arrays i skyen
- API-nøgle i `BIN_KEY` konstant øverst i scriptet
- To bins pr. app: én til data, én til katalog/produktliste
- `binGet(id)` — henter data
- `binCreate(data, name)` — opretter ny bin (første gang)
- `binUpdate(id, data)` — gemmer opdateret data

### AI-integration: Cloudflare Worker
- Worker-URL: `https://preplager-ai.lone-988.workers.dev`
- Modtager base64-kodet billede, returnerer JSON med produktinfo
- Bruges til kamerafunktion + automatisk udfyldning af formular
- Til ny app: overvej om kamera/AI er relevant, eller om en ny Worker skal laves

### PWA (virker som app på iPhone)
Disse meta-tags i `<head>` giver iPhone-app-oplevelse:
```html
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="AppNavn">
<meta name="theme-color" content="#1a1917">
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icon.svg">
```
Kræver en `manifest.json` og et ikon ved siden af HTML-filen.

### Styling
- CSS custom properties (`--bg`, `--surface`, `--text`, osv.) for let tema-skift
- Automatisk dark mode via `@media (prefers-color-scheme: dark)`
- Font: DM Sans fra Google Fonts
- Max-bredde 480px, centreret — designet til mobil

### UI-mønstre at genbruge
| Mønster | Beskrivelse |
|---|---|
| `.stat`-grid | 3 kolonner med tal-oversigt øverst |
| `.filter-row` | Vandret scrollbar med filtreringsknapper |
| `.sort-row` | Sorteringsknapper |
| `.search-row` | Søgefelt med clear-knap |
| `.item` + `.item-group` | Listeelement med gruppering |
| `.pill` | Statusmærkat (ok/snart/udløbet) |
| `.modal-overlay` | Bottom-sheet modal til redigering |
| `.toast` | Kort besked-notifikation nederst |
| `.dot.spin` | Sync-indikator (grøn/gul/rød) |

---

## GitHub Pages opsætning
Repository: https://github.com/PrepO4/FryserIndhold.git
- Push `index.html` (og `manifest.json`) til `main`-branch
- Aktiver GitHub Pages under Settings → Pages → Source: main / root
- App tilgængelig på: `https://prepo4.github.io/FryserIndhold/`

---

## Hvad appen skal være
**Fryser-lagerstyring** — tracker indholdet i fryseren med udløbsdatoer.

### Kategorier (fryser-relevante)
Forslag baseret på typisk fryserforbrug — tilpasses ved næste session:
- 🥩 Kød
- 🐟 Fisk/skaldyr
- 🥛 Mejeri
- 🥦 Grøntsager
- 🍞 Brød/Bagværk
- 🍲 Færdigretter/Rester
- 🍦 Is/Dessert
- 📦 Andet

---

## Ønskede features (ny i forhold til Preplager)

### Flyt produkt til anden kategori
- I redigerings-modalen skal der være mulighed for at ændre kategori
- Bruges når man har tastet forkert, f.eks. lagt noget under Kød der rettelig hører til Mejeri
- Teknisk: i `saveEditItem()` opdateres `item.cat` og gemmes til JSONBin

*(Flere features aftales ved næste session)*

---

## Næste skridt
- [x] Beslut hvad den nye app skal tracke → **fryserindhold**
- [ ] Bekræft kategoriliste og tilføj/fjern kategorier
- [ ] Beslut om kamera/AI skal med
- [ ] Beslut hvilke yderligere nye features der ønskes
- [ ] Opret JSONBin bins til ny app
- [ ] Byg `index.html` med tilpasset indhold
- [ ] Opret `manifest.json` og ikon
- [ ] Push til GitHub og aktiver Pages
