# Changelog

Nennenswerte Änderungen am Cover Designer. Neueste zuerst.

## 2026-09-08 — Projekt-Config im Komplett-ZIP, Bild-Auto-Import, Tablet-Mockup

- **ZIP komplett** legt zusätzlich zu `PNG/` und `WEB/` die **Projekt-Config**
  (`… — Cover-Projekt.json`) ins ZIP-Root — derselbe Stand, den „💾 Speichern" schreibt
  (alle Themes, Texte, Farben, Schriften und eingebettete Bilder). Der Snapshot entsteht
  **nach** dem Zurücksetzen der WEB-Abschaltung, enthält also die echten Badge-Einstellungen.
  Ein Assets-Paket ist damit für sich reproduzierbar.
- **Bild-Auto-Import:** Bilder aus `reference/auto/` werden auf `localhost` beim Start
  automatisch eingelesen, alternativ per Knopf **„📁 Ordner laden"**. Zuordnung über den
  Dateinamen (`hero.png`, `page-1.png`, `ba-1-line.png` …); es werden ausschließlich
  **leere** Slots gefüllt.
- **Tablet-Mockup:** ein PNG mit transparent ausgestanztem Display genügt — der
  Displaybereich wird per Alpha-Analyse gefunden und das Cover dahintergelegt.
  Hand-Override über die Mockup-Felder.

## 2026-08-09 — PNG-Export auf den Rahmen des PDF-Tools

- Neuer Header-Select **„PNG-Ziel"**: `aus (nativ)` · `Freebie · LETTER` (2432×3182) ·
  `KDP · LETTER` (2267×3088). Mit aktivem Ziel rastert `captureForTarget()` jedes Board
  **direkt in Rahmen-Pixeln @300 DPI** statt mit den festen Scales 4.85/2 — das
  nachgelagerte PDF-Tool (Export-Cap 3508 px Langkante) muss danach nicht mehr
  herunterrechnen, also kein zweites Resampling und keine weichen Kanten.
- **Print-Seiten** (Front/Back/What's Inside) werden proportional eingepasst und das Canvas
  exakt aufs Rahmenmaß gepolstert (Ground-Farbe des Themes) — das Board-Ratio 0.773 trifft
  die Rahmen 0.764/0.734 nicht. Alle übrigen Boards (1:1-Shop-Assets, 16:9, Thumb) bekommen
  nur die Zielauflösung, **kein** Padding.
- Bei aktivem Ziel tragen die Dateien ein Suffix (`… Cover [kdp].png`, `… Assets [kdp].zip`),
  damit Freebie- und KDP-Läufe sich nicht überschreiben. Gilt für ZIP komplett (Ordner
  `PNG/`), PNG einzeln und den PNG-Knopf am einzelnen Board; `WEB/` und die PDF-Exporte
  bleiben unverändert. Die Auswahl wird in `localStorage` mitgesichert.

## 2026-08-07 — „Human in the Loop" als Prozess-Slide

- Aus dem 10-Schritte-Prozess-Poster (`reference/human-in-the-loop.png`) wird eine
  **verdichtete 3–5-Schritt-Fassung**, die auf 1080×1080 lesbar bleibt: nummerierte
  Karten auf einer Schiene, je Karte „was passiert" + ein **„My call"**-Kasten mit der
  Entscheidung. Darunter ein dunkles Fußband mit Claim und Werte-Chips.
- Neue Felder in den Base Infos: `hilTagline`, `hilSteps` (je Zeile
  `Titel :: was passiert :: meine Entscheidung`), `hilClaim`, `hilValues`.
  `hilText`/`hilBullets` entfallen — alte Projekte laden weiter, die Felder werden
  nur nicht mehr gerendert.
- Default-Schritte (Englisch): Idea & market check · Generate & curate · Hand finish ·
  Ship with care.

## 2026-08-07 — UI-Umbau: zwei Sidebars, Bild-Leiste, Header-Exporte

- **Zwei Sidebars.** Links **Inhalt** (Texte, Badges & Stempel, Shop-Assets, Feature-Pills,
  USPs, Before-&-After-Texte), rechts **Template** (Theme, Farben, Schrift, Layout & Muster,
  Einstellungen). Beide per Griff in der Breite ziehbar.
- **Base Infos ist ein eigener Tab** statt Overlay (Header: Design ↔ ✎ Base Infos). Der
  inaktive Tab bleibt off-screen gemountet, damit alle Artboards exportierbar bleiben.
  **Autor & Webseite** sind dorthin gewandert; im Design-Tab bleibt nur der Ein/Aus-Schalter.
- **Bild-Leiste über der Vorschau** — alle Slots des Themes in drei Spalten (Hero/Color ·
  Back/Gallery · 4 Before-&-After-Paare), darunter Reset + Asset-Format/Anpassung.
  Einklappbar, zeigt „x / 18 Slots belegt".
- **Exporte & Projekt in den Header.** Ein **„ZIP komplett"**-Button liefert PNG *und*
  cleane WebPs in einer Datei (Ordner `PNG/` + `WEB/`); daneben A4 · US-Letter · KDP ·
  PNG einzeln sowie Speichern/Laden. Laufender Export wird angezeigt und sperrt die Buttons.
- **Variant-Presets** Free · Starter · Full Pack · Paid (plus eigener Text).
- Badges & Stempel sowie Farben/Schrift sind jetzt im Basis-Modus sichtbar; Basis-Modus
  exportiert nur noch die Boards, die er auch rendert (kein Zählen von Thumb/Gallery/Teaser).
- **Fix:** Export hing endlos, wenn man während des Laufs das Fenster wechselte
  (`requestAnimationFrame` pausiert in Hintergrund-Tabs) — jetzt mit Timeout-Fallback.

## 2026-07-31 — Etsy-Asset „Before & After"

- **Neues Shop-Asset (1:1):** mehrere Vorlage→koloriert-Paare mit Pfeil, wahlweise
  **3 Reihen** (je 1 Paar) oder **2×2** (4 Paare). An/Aus in „Shop-Assets", Details in
  der neuen Voll-Box „Before & After (Raster)".
- **Eigene Paar-Bild-Slots** `baLine`/`baColor` (je 4) pro Theme — Vorlage links,
  koloriertes Ergebnis rechts. Paar 1 fällt auf Hero-PBN/Hero zurück. Wandern mit ins
  Projekt-JSON und in „Bilder zurücksetzen".
- **Optionale Extras, per Default aus:** Icon-Spalte (300 DPI / PDF / Seiten / Download,
  `{pages}` zieht Seitenzahl + Seiten-Wort) und Zielgruppen-Band unten. Default ist die
  ruhige Variante mit nur den Bildpaaren.

## 2026-07-24 — UI entschlackt + Serien-Ampel

- **Basis/Voll-Modus.** Umschalter oben im Panel. *Basis* zeigt nur die häufig genutzten
  Felder (Theme, Texte, Cover-Layout, Bilder, Shop-Assets, Export); *Voll* blendet die
  „einmal festlegen"-Boxen ein (Farben, Schrift, Autor & Webseite, Badges & Stempel,
  Feature-Pills, USPs, Human-in-the-Loop, About, Einstellungen). Modus überlebt Reload.
- **Serien-Ampel statt „Alter".** Das wirkungslose Alter-Feld ist raus (inkl. `Ages {age}`-Pill).
  Neu: ein Schwierigkeits-Badge **Easy / Medium / Expert** (drei Punkte in Ampelfarben) auf
  dem Cover, positionierbar. Auswahl in Basis, An/Aus + Position in „Badges & Stempel".
- **On-Cover-Labels auf Englisch** (Easy/Medium/Expert), da englischer Markt.
- **Badges zusammengefasst.** Vol/Band, Variant und Promo (+ Serien-Ampel) in einer Box
  „Badges & Stempel" gebündelt.
- **Theme & Farben gruppiert.** Farben- und Schrift-Box stehen direkt hinter dem Theme-Picker.
- **Shop-Assets abgegrenzt.** Jedes Asset hat jetzt einen Erklär-Halbsatz (wofür im Shop).
- **Difficulty-Levels-Shop-Asset entfernt** (Komponente, Felder, Export-Job, Board).
- **Export erreichbar.** Sticky Schnell-Export-Leiste unten (A4-PDF · US-Letter · ZIP);
  volle Export-Box nach Häufigkeit sortiert. Bild-Kacheln etwas größer.

## Früher

- US-Letter- + KDP-Einzel-PDF-Export ergänzt.
- Projekt speichern/laden als JSON (inkl. eingebetteter Bilder).
- 7 Etsy-Shop-Assets (1:1), 9 Themes, PBN-Split-Hero, USPs, Promo/Vol/Variant-Stempel.
- Als eigenständiges Open-Source-Repo veröffentlicht (MIT, © Ray Sumeragi / Ria's Color Labs).
