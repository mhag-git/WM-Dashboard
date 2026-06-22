# WM 2026 Dashboard (GitHub Pages)

Interaktives HTML-Dashboard für die **FIFA World Cup 2026™** mit:

- **Gruppenständen A–L**
- **aktuellen Ergebnissen & kommenden Anstoßzeiten**
- **lokalen Uhrzeiten im Browser**
- **modernem, minimalistischem UI**
- **Flaggen**
- **offiziellem K.o.-Bracket (Round of 32 bis Finale)**
- **heuristischen Sieg-/Titel-Wahrscheinlichkeiten** auf Basis von **FIFA-Ranking + Turnierform**
- **GitHub-Pages-fähig** (kein Build-Schritt nötig)

---

## Dateien

- `index.html` – komplette App in einer Datei
- `README.md` – diese Anleitung
- `wm_dashboard_2026_bundle.zip` – direkt hochladbares Bundle

---

## Schnellstart (GitHub Pages)

1. Neues GitHub-Repository anlegen, z. B. `wm-dashboard-2026`.
2. `index.html` und `README.md` ins Repo hochladen.
3. In GitHub zu **Settings → Pages** gehen.
4. Unter **Build and deployment** die Quelle **Deploy from a branch** wählen.
5. Branch `main` und Ordner `/ (root)` auswählen.
6. Speichern – GitHub veröffentlicht die Seite unter deiner Pages-URL.

> Kein Node, kein Build, kein Framework erforderlich.

---

## Datenquellen / Architektur

Die Seite versucht beim Laden zuerst **öffentliche JSON-Feeds** anzusprechen. Wenn das nicht klappt (z. B. CORS/Verfügbarkeit), fällt sie automatisch auf einen **eingebauten Snapshot** zurück.

### Primäre Live-/Public-Feeds im HTML

1. **GitHub Raw JSON (World Cup 2026 API Repo)**
   - `https://raw.githubusercontent.com/rezarahiminia/worldcup2026/main/football.matches.json`
   - `https://raw.githubusercontent.com/rezarahiminia/worldcup2026/main/football.matchtables.json`
   - `https://raw.githubusercontent.com/rezarahiminia/worldcup2026/main/football.teams.json`

2. **Public JSON Schedule / Static API**
   - `https://wheniskickoff.com/data/v1/matches.json`
   - `https://wheniskickoff.com/data/v1/groups.json`

### Eingebauter Fallback-Snapshot

Der Snapshot im HTML ist auf Basis öffentlich verfügbarer Turnierstände und Spielpläne vorbereitet und deckt die Gruppenphase sowie das offizielle K.o.-Gerüst ab.

---

## Transparenz zum Wahrscheinlichkeitsmodell

Die Anzeige **„Titelchancen / Sieg-Wahrscheinlichkeiten“** ist bewusst als **heuristische Orientierung** umgesetzt – nicht als Wettmodell.

Verwendete Signale:

- **FIFA-Ranking / FIFA-Punkte** (als Grundstärke)
- **Turnierform** aus bisheriger WM-Leistung
  - Punkte pro Spiel
  - Torverhältnis
  - erzielte / kassierte Tore
- **Fortschrittsbonus** für bereits sehr gut positionierte Teams

Kurzlogik:

- Aus Ranking + Form wird ein **Stärkewert** gebaut.
- Für direkte Matchups wird daraus via logistischer Funktion eine **Sieg-/Remis-Wahrscheinlichkeit** berechnet.
- Die **Titelchance** wird aus den relativen Team-Stärken normalisiert.

> Damit bleibt das Modell nachvollziehbar und robust, ohne versteckte Annahmen oder externe Keys.

---

## Design / Features

- Glas-/Dark-UI mit minimalistischem Layout
- Responsive Darstellung (Desktop / Laptop / Tablet / Smartphone)
- Filter für:
  - Gruppe / Phase
  - Status (Live / Beendet / Kommend)
  - Freitextsuche
- Bracket-Darstellung mit offiziellen Slots
- Browser-abhängige lokale Zeitformatierung (`Intl.DateTimeFormat`)
- Keine externen Build-Tools

---

## Bekannte Grenzen

1. **Echte Live-Daten in GitHub Pages hängen von der Erreichbarkeit der öffentlichen JSON-Feeds ab.**
   Deshalb gibt es den eingebauten Snapshot als Fallback.
2. **Drittplatz-Zuordnungen im K.o.-Baum** bleiben bis zur finalen Bestätigung zum Teil Platzhalter – das ist im Dashboard transparent markiert.
3. **Titelchancen sind heuristisch** und bewusst nicht als exakte Simulation der offiziellen FIFA-Annex-Kombinationen implementiert.

---

## Öffentliche Quellen, die für den Snapshot / die Struktur genutzt wurden

### Offizielle/nahezu offizielle Strukturquellen
- [FIFA – Match schedule, fixtures, results & stadiums](https://www.fifa.com/tournaments/mens/worldcup/canadamexicousa2026/articles/match-schedule-fixtures-results-teams-stadiums)
- [FIFA – Knockout stage match schedule bracket](https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026/articles/knockout-stage-match-schedule-bracket)
- [FIFA – Qualified and eliminated teams](https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026/articles/qualified-eliminated-teams)
- [FIFA Rankings overview](https://ipt.fifa.com/fifa-rankings)

### Öffentliche Ergänzungen für Stände / Rankings
- [NBC Sports – 2026 World Cup group stage table](https://www.nbcsports.com/soccer/news/2026-world-cup-group-stage-table-full-standings-for-all-12-groups)
- [ESPN – FIFA Men’s Top 50 World Rankings: June 2026](https://www.espn.com/soccer/story/_/id/46664763/fifa-mens-top-50-world-rankings)
- [When Is Kickoff – Public JSON API](https://wheniskickoff.com/data/)
- [GitHub – rezarahiminia/worldcup2026](https://github.com/rezarahiminia/worldcup2026)

---

## Anpassungen, die du leicht machen kannst

- Standard-Teams im Predictor ändern (`GER` / `ESP` im JS)
- Farben im `:root`-Block anpassen
- Logo / Titel / Firmenbranding ergänzen
- zusätzliche Tabs (z. B. Torschützen, Host Cities, TV-Infos)

---

## Tipp

Wenn du maximale Kontrolle willst, kannst du statt öffentlicher Feeds auch **eigene JSON-Dateien direkt ins Repo legen** und im `LIVE_ENDPOINTS`-Block auf relative Dateien umstellen – dann ist die Seite vollständig deterministisch.