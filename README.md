# WM 2026 Dashboard V3

GitHub-Pages-fähige HTML-Version des WM-Dashboards mit:

- **Flaggen** für Teams
- **Auto-Refresh** im Browser
- **schönerem K.o.-Bracket** mit Verbindungslinien
- **Live-Daten-Versuch** über einen öffentlichen REST-Endpunkt
- **Snapshot-Fallback**, falls der Live-Feed nicht erreichbar ist
- eingebauter **Anleitung zum Anpassen von Teams und Spielen**

## Dateien

- `wm2026-dashboard-v3.html` – vollständiges Dashboard als eine einzige HTML-Datei
- `wm2026-snapshot-v3.json` – kleiner Snapshot-Hinweis / Fallback-Metadaten
- `README-wm2026-dashboard-v3.md` – diese Anleitung

## Deployment auf GitHub Pages

1. Lade `wm2026-dashboard-v3.html` herunter.
2. Benenne die Datei in **`index.html`** um.
3. Lege ein GitHub-Repository an oder verwende ein bestehendes.
4. Lade `index.html` in das Root-Verzeichnis hoch.
5. Optional kannst du `wm2026-snapshot-v3.json` ebenfalls mit hochladen.
6. Öffne in GitHub **Settings → Pages**.
7. Wähle bei **Build and deployment** die Branch `main` (oder `master`) und `/root`.
8. Speichern – danach ist das Dashboard über GitHub Pages erreichbar.

## Live-Daten-Modus

Die Datei versucht beim Laden diese öffentlichen Endpunkte abzurufen:

- `https://worldcup26.ir/get/games`
- `https://worldcup26.ir/get/groups`

Wenn der Feed nicht erreichbar ist oder CORS blockiert wird, läuft das Dashboard automatisch mit dem eingebetteten Snapshot weiter.

## Auto-Refresh

Im Dashboard kannst du direkt einstellen:

- Auto-Refresh **an/aus**
- Intervall **30 / 60 / 120 Sekunden**
- manuelles **„Jetzt aktualisieren“**

## Teams und Spiele anpassen

In V3 gibt es dafür **zwei Wege**:

### A) Direkt im Dashboard
Im Reiter **„Live & Anleitung“** ist eine aufklappbare Anleitung eingebaut.

### B) Direkt in der HTML-Datei
Suche in der Datei nach diesen Blöcken:

- `const TEAM_FLAGS = { ... }` → Flaggen anpassen
- `const RANKINGS = { ... }` → FIFA-Ranking / Teamstärke anpassen
- `const GROUPS = { ... }` → Gruppenzuordnung anpassen
- `SNAPSHOT.completedMatches` → gespielte Ergebnisse anpassen
- `SNAPSHOT.upcomingMatches` → kommende Spiele anpassen
- `SNAPSHOT.bracket` → K.o.-Bracket anpassen

## Hinweise

- Die Sieg-Wahrscheinlichkeiten sind **heuristisch** und kein Wettmodell.
- Für GitHub Pages ist **kein Build-Schritt** nötig.
- Alle Änderungen können in einem normalen Texteditor gemacht werden.

## Sinnvolle nächste Erweiterungen

- Team-Logos statt Emoji-Flaggen
- eigene Datenquelle / JSON-Datei im Repo
- GitHub Action zum periodischen Aktualisieren des Snapshots
- Detailansicht pro Team
