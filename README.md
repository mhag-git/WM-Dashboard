# WM 2026 Dashboard – README

Diese README beschreibt die HTML-Datei **`wm2026-dashboard-v5-timestamps-flags.html`**.

## Inhalt
- Interaktives Dashboard zur WM 2026
- Live-Fetch für Spiele und Gruppen
- Snapshot-Fallback bei nicht erreichbaren Live-Daten
- Automatische Gruppentabellen
- Drittplatzierten-Ranking
- K.o.-Bracket
- Prognose-Modul
- Last-Updated-Timestamps je Datenquelle
- Sichtbare Kennzeichnung veralteter Snapshot-Daten
- Nationenflaggen bei Team-/Länderbezeichnungen

---

## Dateien
- **`wm2026-dashboard-v5-timestamps-flags.html`** → aktuelle Dashboard-Version
- **`wm2026-dashboard-v4-fixed.html`** → vorherige Fix-Version
- **`wm2026-dashboard-v3.html`** → ursprüngliche Ausgangsdatei

---

## Funktionsumfang

### 1. Live-Daten + Snapshot-Fallback
Das Dashboard versucht beim Start, Daten aus folgenden Quellen zu laden:
- `https://worldcup26.ir/get/games`
- `https://worldcup26.ir/get/groups`

Wenn der Live-Abruf fehlschlägt oder die Antwort nicht nutzbar ist, wird automatisch der in der HTML-Datei eingebettete **Snapshot** verwendet.

### 2. Zeitstempel je Datenquelle
Im Bereich **„Live-Daten & Quellen“** werden pro Quelle angezeigt:
- **Last Updated**
- **Alter**
- **Status**

Quellen:
- Snapshot
- Live-Games API
- Live-Gruppen API

### 3. Stale-Daten-Erkennung
Veraltete Daten werden farblich hervorgehoben.

Aktuelle Schwellenwerte in der Datei:
- **Snapshot veraltet ab 6 Stunden**
- **Live-Quelle veraltet ab 20 Minuten**

### 4. Gruppenlogik
Die Gruppentabellen werden wie folgt erzeugt:
1. Wenn aus `/get/groups` ein verwertbarer Gruppenstand gelesen werden kann, wird dieser bevorzugt verwendet.
2. Falls nicht, werden die Tabellen lokal aus den bekannten Resultaten berechnet.

### 5. Namensnormalisierung
Damit API-Bezeichnungen konsistent zu Rankings, Gruppen und Flaggen passen, werden einige Namen automatisch gemappt.

Beispiele:
- `Turkey` → `Türkiye`
- `Bosnia-Herzegovina` → `Bosnia and Herzegovina`
- `Curacao` → `Curaçao`
- `DR Congo` → `Congo DR`
- `Cape Verde` → `Cabo Verde`
- `United States` → `USA`

### 6. Flaggenanzeige
Flaggen werden an vielen Stellen automatisch eingeblendet, u. a. in:
- Teamlisten
- Gruppentabellen
- Matchlisten
- Prognose-Modul
- Übersichtskacheln
- Bracket-Darstellung

---

## Verwendung

### Lokal öffnen
Die HTML-Datei kann direkt im Browser geöffnet werden:
1. Datei herunterladen
2. Doppelklick auf `wm2026-dashboard-v5-timestamps-flags.html`
3. Dashboard im Browser nutzen

### Auf GitHub Pages / SharePoint / Webserver bereitstellen
Da es sich um eine Einzeldatei handelt, kann sie direkt hochgeladen und bereitgestellt werden.

Hinweis:
Wenn ein Browser oder Host den externen API-Zugriff blockiert (z. B. durch CORS), funktioniert das Dashboard weiterhin mit dem eingebetteten Snapshot.

---

## Bedienung

### Tabs
- **Überblick**
- **Gruppen**
- **Spiele**
- **K.o.-Bracket**
- **Live & Anleitung**

### Filter
- Gruppenfilter
- Teamsuche
- Phasenfilter für Spiele

### Refresh
- Auto-Refresh ein/aus
- Intervall wählbar
- Manueller Button **„Jetzt aktualisieren“**

---

## Anpassungen in der HTML-Datei
Die Datei kann direkt mit einem Texteditor bearbeitet werden.

### 1. Rankings ändern
Suche nach:
```js
const RANKINGS = { ... }
```

### 2. Gruppen ändern
Suche nach:
```js
const GROUPS = { ... }
```

### 3. Teamflaggen ergänzen
Suche nach:
```js
const TEAM_FLAGS = { ... }
```

### 4. Snapshot-Spiele ändern
Suche nach:
```js
SNAPSHOT.completedMatches
SNAPSHOT.upcomingMatches
```

### 5. Bracket ändern
Suche nach:
```js
SNAPSHOT.bracket
```

### 6. Alias-Mapping ändern
Suche nach:
```js
const TEAM_ALIASES = { ... }
```

### 7. Veraltet-Schwellen ändern
Suche nach der Funktion:
```js
function isSourceStale(source)
```

Dort können die Grenzwerte angepasst werden.

---

## Wichtige technische Hinweise

### Snapshot-Zeit
Die Datei verwendet eine dynamische aktuelle Uhrzeit im Browser, damit Spiele nicht mit einem veralteten festen Zeitpunkt bewertet werden.

### Live-Games vs. Live-Gruppen
- **Games API** liefert Spiele / Resultate
- **Groups API** liefert – sofern verfügbar – direkt nutzbare Gruppenstände

### Fallback-Verhalten
Wenn Live-Gruppen nicht nutzbar sind, bleibt das Dashboard stabil und berechnet die Tabelle lokal aus den Spielresultaten.

---

## Bekannte Grenzen
- Das Dashboard ist auf die Verfügbarkeit und Struktur der externen API angewiesen.
- Änderungen an Feldnamen im API-Payload können eine Anpassung des Parsers erforderlich machen.
- Die Wahrscheinlichkeiten im Prognose-Modul sind **heuristisch** und keine offiziellen Quoten.
- Nicht jedes Team-Label im Bracket ist zwingend bereits ein final bekannter Landesname; Platzhalter wie `A1`, `B2`, `W73` usw. bleiben bewusst erhalten.

---

## Empfohlene nächste Erweiterungen
Falls gewünscht, kann als nächste Version noch ergänzt werden:
- Debug-Panel für Team-Mapping aus der API
- Umschalter **Nur Live / Nur Snapshot**
- Exportfunktion für Tabellen
- Zusätzliche Kennzahlen je Gruppe
- Anzeige der letzten erfolgreichen API-Antwort getrennt nach Games und Groups im Header

---

## Kurzfazit
Die Version **v5** verbessert gegenüber der ursprünglichen Datei insbesondere:
- robustere Datenlogik
- bessere Transparenz über Datenquellen
- Erkennung veralteter Snapshot-Daten
- konsistente Flaggenanzeige
- modernere und übersichtlichere UI
