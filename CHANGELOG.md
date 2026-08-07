# Changelog

Nennenswerte Änderungen am Cover Designer. Neueste zuerst.

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
