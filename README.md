# WM 2026 Dashboard V2

GitHub-Pages-fähige HTML-Version des WM-Dashboards mit:

- visuellem **K.o.-Bracket**
- **Live-Daten-Versuch** über einen öffentlichen REST-Endpunkt
- **Snapshot-Fallback**, falls der Live-Feed nicht erreichbar ist
- Gruppenständen, Drittplatzierten-Ranking und Heuristik für Sieg-Wahrscheinlichkeiten

## Dateien

- `wm2026-dashboard-v2.html` – vollständiges Dashboard als eine einzige HTML-Datei
- `wm2026-snapshot-v2.json` – Snapshot-Datenstand, aus denen die HTML-Datei ebenfalls gespeist werden kann
- `README-wm2026-dashboard-v2.md` – diese Anleitung

## GitHub Pages Deployment

1. Neues Repository auf GitHub anlegen
2. `wm2026-dashboard-v2.html` nach `index.html` umbenennen
3. `index.html` in das Root-Verzeichnis des Repos hochladen
4. Optional zusätzlich `wm2026-snapshot-v2.json` mit hochladen
5. In GitHub: **Settings → Pages** öffnen
6. Bei **Build and deployment** die Branch `main` (oder `master`) und `/root` auswählen
7. Speichern – danach ist die Seite unter der GitHub-Pages-URL erreichbar

## Datenmodus

Das Dashboard nutzt zwei Ebenen:

### 1) Live-Daten
Die HTML-Datei versucht beim Laden diese öffentlichen Endpunkte zu lesen:

- `https://worldcup26.ir/get/games`
- `https://worldcup26.ir/get/groups`

### 2) Fallback-Snapshot
Wenn der Feed nicht erreichbar ist oder ein Browser/CORS-Problem auftritt, schaltet das Dashboard automatisch auf den eingebetteten Snapshot zurück.

## K.o.-Bracket

Der Turnierbaum ist von der **Runde der letzten 32** bis zum **Finale** vorstrukturiert.
Bekannte Paarungen bzw. feststehende Startplätze (z. B. sichere Gruppensieger) werden im Bracket angezeigt.

## Hinweise

- Die Sieg-Wahrscheinlichkeiten sind **heuristisch** und kein Wettmodell.
- Für GitHub Pages ist **kein Build-Schritt** nötig.
- Wenn du ein komplett persistentes Setup willst, kannst du zusätzlich einen eigenen JSON-Feed oder einen GitHub Action Job ergänzen.

## Sinnvolle Erweiterungen

- echtes Team-Logo/Flaggen-Rendering
- Auto-Polling alle 30–60 Sekunden
- Farbliche Kennzeichnung für Live-Spiele
- getrennte Ansicht für mobile Geräte
- eigenes JSON-Caching im Repo via GitHub Actions
