# WM 2026 Dashboard V4

GitHub-Pages-fähige HTML-Version des WM-Dashboards mit:

- **Multi-API-Fallback**
- **Health-Status** je Provider
- **Flaggen**, **Auto-Refresh** und **K.o.-Bracket**
- **Live-Overlay + Snapshot-Fallback**
- eingebauter **Anleitung zum Anpassen von Teams, Spielen und Providern**

## Dateien

- `wm2026-dashboard-v4.html` – vollständiges Dashboard als eine einzige HTML-Datei
- `README-wm2026-dashboard-v4.md` – diese Anleitung
- `wm2026-snapshot-v4.json` – Snapshot-Metadaten

## Deployment auf GitHub Pages

1. Lade `wm2026-dashboard-v4.html` herunter.
2. Benenne die Datei in **`index.html`** um.
3. Lade `index.html` in das Root-Verzeichnis deines GitHub-Repositories.
4. Optional kannst du `wm2026-snapshot-v4.json` zusätzlich ablegen.
5. Aktiviere in GitHub unter **Settings → Pages** das Hosting der Haupt-Branch.

## Multi-API-Fallback in V4

V4 versucht Daten in dieser Reihenfolge zu laden:

1. `worldcup26.ir` → vollständiger Spiel-Feed ohne Key
2. `KickoffAPI` → Live-Overlay über API-Key (`x-api-key`)
3. `WorldCupAPI` → Live-Overlay über Query-Parameter-Key
4. eingebetteter Snapshot

Wenn nur ein Overlay-Feed erfolgreich ist, wird dein Snapshot als Basis verwendet und mit Live-Scores ergänzt.

## Health-Status

Im Reiter **„Live & Health“** siehst du pro Provider:

- Status (`bereit`, `optional`, `fehler`, `idle`)
- letzte Latenz in ms
- letzten Prüfzeitpunkt
- verwendeten Endpoint

## API-Keys

API-Keys werden **nicht fest in die HTML-Datei geschrieben**. Stattdessen speichert V4 sie nur lokal im Browser via `localStorage`.

### Eingabefelder in V4

- **KickoffAPI Key**
- **WorldCupAPI Key**

## Teams, Spiele und Bracket anpassen

In der HTML-Datei kannst du folgende Blöcke bearbeiten:

- `TEAM_FLAGS` → Flaggen
- `RANKINGS` → Teamstärke / FIFA-Ranking
- `GROUPS` → Gruppenverteilung
- `SNAPSHOT.completedMatches` → Ergebnisse
- `SNAPSHOT.upcomingMatches` → kommende Spiele
- `SNAPSHOT.bracket` → K.o.-Baum
- `PROVIDERS` → Provider-Reihenfolge / Endpunkte

## Hinweise

- Die Sieg-Wahrscheinlichkeiten sind **heuristisch** und kein Wettmodell.
- Für GitHub Pages ist **kein Build-Prozess** nötig.
- Änderungen können in einem normalen Texteditor gemacht werden.
