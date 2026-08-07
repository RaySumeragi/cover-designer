# Cover Designer

Ein kostenloses, browserbasiertes Tool zum Gestalten von Buch-Covers — gedacht für
alle, die selbst Bücher veröffentlichen (KDP, Etsy & Co.). Keine Installation, keine
Anmeldung, keine Cloud: alles läuft lokal im Browser.

> Von [Ria's Color Labs](https://github.com/RaySumeragi) · Open Source unter MIT.

## ➡️ Direkt loslegen

**[Tool öffnen](https://raysumeragi.github.io/cover-designer/)** — einfach im Browser starten.

Oder lokal: dieses Repo herunterladen und die `index.html` doppelklicken.

## Was es kann

- **Themes** als Startpunkt — fertige Cover-Looks, frei anpassbar.
- **Aufgeräumte Oberfläche:** links der **Inhalt** dieses Covers (Texte, Badges, Assets),
  rechts die **Template-Einstellungen** (Theme, Farben, Schrift, Layout & Muster), dazwischen
  die Vorschau mit allen Bild-Slots direkt darüber.
- **Basis-/Voll-Modus:** Umschalter, der die Panels schlank hält — *Basis* zeigt nur die
  täglich genutzten Felder, *Voll* alle „einmal festlegen"-Einstellungen. Der Modus wird
  gemerkt.
- **Texte, Farben & Schriften** vollständig editierbar (pro Theme), jederzeit zurücksetzbar.
- **Eigene Bilder** hochladen und einsetzen.
- **Cover-Layout & Muster**, Band-/Volume-Nummer, Variant-Badge, Promo-Stempel und ein
  **Schwierigkeits-Badge** (Easy / Medium / Expert) als Ampel auf dem Cover.
- **Feature-Pills & USPs** für Vorder- und Rückseite.
- **Base Infos** als eigener Tab: einmal gepflegte Angaben (Autor, Webseite, Shop-Texte),
  die für alle Cover gelten.
- **Export** — komplett in der Kopfleiste:
  - **ZIP komplett** — alle Assets in einer Datei: druckfertige PNGs *und* cleane
    Web-Bilder (~1200 px WebP, ohne Badges)
  - **PDF** druckfertig: **A4**, **US-Letter** und **KDP-Einzelseiten**
  - **PNG** einzeln je Element
  - **Shop-Assets** im 1:1-Format (z. B. für Etsy) sind überall mit dabei
- **Projekt speichern/laden** als JSON — dein Cover lässt sich wiederherstellen.

## Datenschutz

Es werden **keine Daten hochgeladen**. Bilder, Texte und Exporte bleiben auf deinem
Gerät. Beim ersten Laden werden lediglich die benötigten Bibliotheken und Schriften
von öffentlichen CDNs geholt (siehe unten).

## Technik

Eine einzige `index.html` — kein Build-Step, kein Server, kein Package-Manager.
Abhängigkeiten werden zur Laufzeit per CDN geladen:

- [React](https://react.dev/) + ReactDOM (UI)
- [Babel Standalone](https://babeljs.io/docs/babel-standalone) (JSX im Browser)
- [html2canvas](https://html2canvas.hertzen.com/) (Element → Bild)
- [jsPDF](https://github.com/parallax/jsPDF) (PDF-Export)
- [JSZip](https://stuk.github.io/jszip/) (ZIP-Export)

Dadurch braucht der erste Aufruf eine Internetverbindung. Eine spätere Version kann
die Abhängigkeiten lokal bündeln (echtes Offline-Standalone) und Babel durch
vorkompiliertes JSX ersetzen.

## Lizenz

[MIT](LICENSE) © Ray Sumeragi / Ria's Color Labs
