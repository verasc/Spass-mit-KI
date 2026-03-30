# spassmitki.de – Setup-Anleitung für GitHub Pages mit Claude Code

## Was du hast
- GitHub-Account ✅
- Repository angelegt ✅
- Domain spassmitki.de bei Strato registriert ✅
- Website als HTML-Datei (vera-website-v6.html) ✅

## Was du brauchst
- **Claude Code** installiert (Terminal-Tool von Anthropic)
- **Git** auf deinem Rechner installiert

---

## Schritt 1: Claude Code installieren

Falls noch nicht geschehen, öffne dein Terminal (Mac: "Terminal"-App, Windows: "PowerShell") und tippe:

```
npm install -g @anthropic-ai/claude-code
```

Falls npm nicht installiert ist, brauchst du zuerst Node.js: https://nodejs.org (LTS-Version runterladen und installieren).

Danach `claude` eintippen – beim ersten Mal wirst du nach deinem Anthropic API-Key gefragt.

---

## Schritt 2: Repository auf deinen Rechner klonen

Im Terminal:

```
cd ~/Desktop
git clone https://github.com/DEIN-USERNAME/DEIN-REPO-NAME.git
cd DEIN-REPO-NAME
```

(Ersetze DEIN-USERNAME und DEIN-REPO-NAME mit deinen echten Werten)

---

## Schritt 3: Dateien ins Repository kopieren

Kopiere diese Dateien (aus dem ZIP oder einzeln) in den Repo-Ordner auf deinem Desktop:

```
DEIN-REPO-NAME/
├── index.html          ← die vera-website-v6.html (umbenannt!)
├── impressum.html
├── datenschutz.html
└── CNAME               ← enthält nur: spassmitki.de
```

**Wichtig:** Die Hauptseite MUSS `index.html` heißen, nicht vera-website-v6.html.

---

## Schritt 4: Claude Code starten

Im Terminal, im Repo-Ordner:

```
claude
```

Dann sagst du Claude Code z.B.:

> "Bitte hilf mir, diese Website auf GitHub Pages zu deployen. 
> Die Datei index.html ist meine Startseite, CNAME enthält meine Domain spassmitki.de.
> Bitte füge alle Dateien zum Git-Repository hinzu, committe sie und pushe sie zu GitHub."

Claude Code wird dann die Git-Befehle für dich ausführen:
- `git add .`
- `git commit -m "Erste Version der Website"`  
- `git push origin main`

---

## Schritt 5: GitHub Pages aktivieren

Das machst du einmalig im Browser:

1. Gehe zu github.com → dein Repository
2. Klicke auf **Settings** (Zahnrad-Tab oben)
3. Links im Menü: **Pages**
4. Unter "Source": Branch **main** auswählen, Ordner **/ (root)**
5. **Save** klicken
6. Unter "Custom domain": `spassmitki.de` eintragen → **Save**

GitHub zeigt dir dann eine Meldung, dass die Domain konfiguriert wird.

---

## Schritt 6: DNS bei Strato konfigurieren

Bei Strato einloggen → Domains → DNS-Einstellungen für spassmitki.de:

**A-Records anlegen** (4 Stück, Host leer oder @):
- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

**CNAME-Record anlegen:**
- Host: www
- Ziel: DEIN-USERNAME.github.io

**Wichtig:** Falls bestehende A-Records vorhanden sind (z.B. auf Strato-Webspace), diese vorher löschen.

DNS-Änderungen brauchen bis zu 24 Stunden.

---

## Schritt 7: HTTPS aktivieren

Sobald die DNS-Einträge greifen (meistens nach 1-2 Stunden):

1. GitHub → Repository → Settings → Pages
2. Haken bei **Enforce HTTPS** setzen

---

## Ab jetzt: Website mit Claude Code pflegen

Jedes Mal wenn du etwas ändern willst:

```bash
cd ~/Desktop/DEIN-REPO-NAME
claude
```

Dann sagst du z.B.:

- "Ändere den Claim im Hero zu 'KI-Neugier ist trainierbar.'"
- "Füge einen neuen Blogpost hinzu über KI-Angst im Team"
- "Erstelle eine neue Unterseite für mein Workshop-Angebot"
- "Pushe die Änderungen zu GitHub"

Claude Code bearbeitet die Dateien und pushed – wenige Sekunden später ist die Änderung live.

---

## Kontext für Claude Code

Wenn du Claude Code das erste Mal in deinem Repo startest, kannst du ihm diesen Kontext geben:

> "Das ist meine Website spassmitki.de, gehostet auf GitHub Pages.
> Ich bin Vera Schiecke, Diplom-Psychologin und KI-Trainerin in Berlin.
> 
> Brand-Regeln:
> - Farben: Blush (#FFF0F3), Midnight (#0D0221), Majorelle Light (#4A4FE0), Majorelle Glow (#8678FF)
> - Schrift: Outfit Bold (700) für Headlines, DM Sans für Body
> - Wortmarke: 'Vera Schiecke.' mit übergroßem Majorelle-Punkt
> - Hashtag: #SpaßMitKI als Branded Element
> - Domain: spassmitki.de
> - Ton: Direkt, kurze Sätze, trockener Humor, 'du' statt 'Sie'
> 
> Bitte halte dich bei allen Änderungen an diese Brand-Regeln."

Tipp: Du kannst das auch in eine Datei `.claude` oder `CLAUDE.md` im Repo speichern – dann hat Claude Code den Kontext automatisch bei jedem Start.

---

## Dateien in diesem Paket

| Datei | Was ist das | Was tun |
|-------|-------------|---------|
| vera-website-v6.html | Deine Startseite | Umbenennen zu `index.html` |
| impressum.html | Impressum (Platzhalter) | Mit echten Daten ergänzen |
| datenschutz.html | Datenschutz (Platzhalter) | Von Anwalt prüfen lassen |
| CNAME | Domain-Zuordnung | So lassen |
| CLAUDE.md | Brand-Kontext für Claude Code | So lassen |
