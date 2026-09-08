# CLAUDE.md

Guidance for Claude Code when working in the **cover-designer** repo.

## Was das ist

Ein **einzelnes `index.html`** — Cover-Designer für Selfpublisher (KDP/Etsy). Single-File
React-App via **Babel Standalone** (JSX im Browser), **kein Build-Step**, kein Server, kein
Package-Manager. Öffnen = `index.html` im Browser. Abhängigkeiten (React, ReactDOM, Babel,
html2canvas, jsPDF, JSZip) kommen zur Laufzeit per CDN → der erste Aufruf braucht Internet.

## ⚠️ Zwei synchron zu haltende Kopien

Dieselbe App liegt **zweimal, inhaltlich identisch**:

- `D:\03_DEV\cover-designer\index.html` — **kanonisch** (dieses public Repo, MIT).
- `D:\03_DEV\malbuch-tools\cover-designer.html` — Kopie im internen Tools-Repo.

Änderungen zuerst hier machen, dann spiegeln:

```bash
cp /d/03_DEV/cover-designer/index.html /d/03_DEV/malbuch-tools/cover-designer.html
```

Nach dem Sync `diff -q` gegenprüfen. Public-Repo-Commits laufen auf `main`; **nur auf
ausdrückliche Ansage pushen**.

## Sprach-Regel (wichtig)

- **Text, der AUF das Cover / einen Artboard / ein Badge gerendert wird → Englisch**
  (das Produkt wird auf dem englischen Markt verkauft). Beispiel: Schwierigkeit heißt
  **Easy / Medium / Expert**, nicht Leicht/Mittelschwer/Experte.
- Die **Config-Panel-UI** (Abschnittstitel, Steuerungs-Beschriftungen) bleibt **Deutsch**.

## Architektur-Kurzabriss

- Ein `t`-State-Objekt (Spread aus `DEFAULTS`) hält alle Text-/Toggle-Einstellungen;
  Per-Theme-Overrides in `colorsByTheme` / `blurbByTheme` / `hookByTheme` / `fontByTheme` /
  `imagesByTheme`. Auto-Save nach localStorage (`cd2-settings`).
- **Layout:** Header (Tabs · Export- + Projekt-Buttons · Basis/Voll) über zwei Ansichten.
  `tab` = `'design' | 'base'`; **beide bleiben gemountet** — die inaktive liegt per
  `.view:not(.on)` off-screen, sonst fehlen ihre Artboards beim Export.
  Design-Ansicht = linke Sidebar **Inhalt** (`panelW`) · Stage mit **Bild-Leiste**
  (`.imagebar`, alle Drop-Slots) + Boards · rechte Sidebar **Template** (`panelRW`).
- **Panel-Modi:** `uiMode` = `'basis' | 'voll'`. Der `Sec({tier,title,children})`-Wrapper
  rendert eine Box nur, wenn `uiMode==='voll' || tier==='basis'`. Neue Boxen als
  `<Sec tier="basis|voll">` einhängen — häufig genutzt = `basis`, einmalig festgelegt = `voll`.
- **Badges/Overlays:** `Overlays` platziert Vol/Variant/Promo/Level via `cornerStyle`/`BADGE_POS`.
  Positionsfelder `posVol`/`posVariant`/`posPromo`/`posLevel`. `showBadges` ist der Master-Schalter.
- **Serien-Ampel:** `SERIES_LEVELS` (easy/medium/expert) + `LevelBadge`; gesteuert über
  `seriesLevel` (Basis-Select) sowie `showLevelBadge`/`posLevel` (in „Badges & Stempel", Voll).
- **Export:** html2canvas → PDF (A4, US-Letter, KDP-Einzel), PNG einzeln und `exportZipAll`
  (ein ZIP mit `PNG/` **und** badge-freien `WEB/`-WebPs). Alles im Header; `run(label, fn)`
  setzt `busy` und sperrt die Buttons. `allJobs = [...EXPORT_JOBS, ...SHOP_JOBS.filter(sichtbar)]`,
  `EXPORT_JOBS` lässt Thumb/Gallery/Teaser im Basis-Modus weg (dort nicht gerendert).
- **Bild-Auto-Import:** `autoSlotFor` bildet Dateinamen auf Slots ab, `scanAutoDir` liest
  `reference/auto/` (nur über http(s), unter `file://` leer), `fillAutoImages` füllt **nur
  leere** Slots. `reference/` ist git-ignoriert.
- **Tablet-Mockup:** `detectScreenRect` findet das transparente Displayloch (Flood-Fill vom
  Bildrand = Hintergrund, größte übrige transparente Region = Display); `MockupCover` legt
  das Cover hinter das PNG. `t.mockupManual` + `mockupScr*` sind der Hand-Override.
- **Base Infos:** Felder aus `BASE_INFO_KEYS` (Autor/Webseite + fest gepflegte Etsy-Assets),
  „⧉ Als Code kopieren" erzeugt daraus ein `DEFAULTS`-Snippet.

## Arbeiten in diesem Repo

- Kein Build/Lint/Test → **manuell im Browser verifizieren** (`index.html` öffnen, betroffene
  Boxen in Basis **und** Voll prüfen, Export testen, Konsole auf Fehler checken).
- `file://`-Navigation in Chrome-Automation ist blockiert → im Repo
  `python -m http.server 8777 --bind 127.0.0.1` starten und
  `http://127.0.0.1:8777/index.html` öffnen (steht so auch in der README).
  Achtung: `img.decode()` hängt im Automations-Kontext — im Tool-Code `onload` benutzen.
- Alte JSON-Projekte ohne neue Felder müssen ohne Crash laden (`{ ...DEFAULTS, ...data.t }`).

Siehe [ROADMAP.md](ROADMAP.md) für offene Punkte und [CHANGELOG.md](CHANGELOG.md) für die Historie.
