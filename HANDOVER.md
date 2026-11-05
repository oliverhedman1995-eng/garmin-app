# HANDOVER: garmin-app (frontend för Olivers Garmin-dashboard)

Senast uppdaterad 2026-11-06.

## Vad det är
Det här repot är **bara den publicerade frontenden**: en statisk sida som GitHub Pages serverar på
**https://oliverhedman1995-eng.github.io/garmin-app/**. All källkod, backend och dokumentation finns i det privata repot
**oliverhedman1995-eng/garmin-dash** (se dess `HANDOVER.md`). Ändra aldrig här direkt; ändra i `garmin-dash/web/` och kopiera hit.

| Fil | Vad |
|---|---|
| `index.html` | Hela appen (HTML, CSS, JS). Chart.js och supabase-js från CDN. |
| `manifest.json`, `icon.png` | Hemskärmsikon och PWA-manifest. |

## Köra lokalt
```bash
python3 -m http.server 8790   # öppna http://localhost:8790 och logga in
```

## Tjänster och inloggning
- **Supabase** `https://eiixsjcqcmgcullkjjhp.supabase.co`: läser/skriver tabeller med supabase-js. URL och *publishable* key står i `index.html` med avsikt; åtkomsten styrs av RLS (`is_oliver()` släpper bara Olivers e-post).
- Inloggning: Supabase Auth med e-post + lösenord. Sidan har även en "Skapa konto"-knapp, se säkerhetsnotis i garmin-dash.
- **Edge functions** som anropas: `food-analyze` (matfoto), `pantry-coach` (kylskåpscoach).
- Garmin och Strava nås aldrig från sidan; knappar lägger rader i `garmin_commands` som GitHub Actions i garmin-dash kör.

## Miljövariabler
Inga. Sidan är statisk.

## Hosting och telefonappen
GitHub Pages (branch `main`, rot). Deploy = pusha. I iPhone: Safari → Dela → Lägg till på hemskärmen. Öppnas medvetet i Safari (inte fristående PWA) eftersom standalone-läget på iOS bröt inloggning och fält.

## Status
- Fungerar: dashboard, matlogg, kylskåpscoach, påminnelser.
- 2026-11-06: datan uppdateras inte just nu, eftersom Actions-jobbet `garmin-sync` i garmin-dash är avstängt (Oliver pausade alla utskick).
- Nästa steg: se garmin-dash `HANDOVER.md`.
