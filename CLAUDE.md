# CLAUDE.md – Regelwerk für gutmannholding.com

Dieses Repository ist die öffentliche Website der Gutmann Holding Group.
Der Ordner ist 1:1 das Deployment-Artefakt (Vercel, statisch).
Die folgenden Regeln gelten in jeder Session, ohne Ausnahme.

**DESIGN.md ist verbindlich. Bei Konflikt zwischen CLAUDE.md und DESIGN.md
gilt DESIGN.md.**

## Harte Regeln

1. **Kein JavaScript. Keine npm-Dependencies. Kein Build-Step. Kein Framework.**
   Reines HTML5 + CSS. Es gibt keine `package.json`, keine `node_modules`,
   keine Bundler, keine Preprocessor. Was im Repo liegt, wird ausgeliefert.
   Einzige Ausnahme: `<script type="application/ld+json">` für strukturierte
   Daten (JSON-LD). Das ist Datenmarkup, kein ausführbarer Code.

2. **Null externe Requests.** Keine CDNs, keine Webfonts, keine Icon-Libraries,
   keine Tracker, keine Analytics, keine iFrames, keine externen Bilder.
   Ausschliesslich der System-Font-Stack aus `assets/css/main.css`.
   Alle Assets liegen unter `/assets/` und werden root-relativ referenziert.

3. **Keine Cookies, kein localStorage, kein sessionStorage.**
   Die Seite darf nichts auf dem Endgerät speichern oder auslesen.

4. **Kein Inline-CSS und kein `style`-Attribut.** Alles CSS liegt in
   `assets/css/main.css`. Grund: Content-Security-Policy mit
   `style-src 'self'` (siehe `vercel.json`).

5. **Semantisches HTML, WCAG 2.1 AA.**
   - Landmarks: `header`, `main`, `footer` (ggf. `nav`)
   - genau eine `h1` pro Seite, logische Heading-Hierarchie ohne Sprünge
   - sichtbarer Focus-State (`:focus-visible`), niemals `outline: none` ohne Ersatz
   - Farbkontrast mindestens 4.5:1 für Text
   - Skip-Link als erstes fokussierbares Element
   - `<html lang="de">`
   - jedes `<img>` hat ein `alt`-Attribut (leer nur bei rein dekorativen Bildern)
     sowie `width` und `height` (CLS 0)
   - `prefers-reduced-motion` wird respektiert: jede Transition wird
     unter `(prefers-reduced-motion: reduce)` deaktiviert

6. **Rechtstexte werden NIE erfunden, geschätzt oder aus dem Netz kopiert.**
   Fehlt ein Rechtstext (Impressum, Datenschutz, AGB o. ä.), enthält die
   betreffende Seite ausschliesslich den Text `TODO: Text ausstehend` und
   der Zustand wird im Output der Session gemeldet. Kein Lorem Ipsum, keine
   Vorlagen, keine "typischen" Formulierungen. Vorhandene Prüfstellen
   (`<mark class="todo">`) in Rechtstexten werden nur vom Betreiber
   ausgefüllt, nie von Claude.

7. **Vor jedem Commit: keine Secrets, keine internen Dokumente.**
   Das Repository ist öffentlich. Keine API-Keys, keine Tokens, keine
   Verträge, keine internen Notizen, keine personenbezogenen Daten ausser
   den gesetzlich verpflichtenden Angaben im Impressum und in der
   Datenschutzerklärung.

## Design-System

- Verbindlich ist `DESIGN.md` im Projektwurzelverzeichnis. Sie wird nicht
  interpretiert, sondern angewendet. Bei Konflikt gilt DESIGN.md.
- Kurzfassung: seriös, zurückhaltend, Beratungs-/Holding-Charakter. Ein
  einziges helles Farbschema auf `--paper` (#FFFFFF), kein Dark Mode.
  Genau zehn Farb-Tokens, keine weiteren. Überschriften in `--font-display`
  (Georgia-Stack) in Gewicht 400, nie 600, nie bold. Fliesstext, Labels und
  Kopfzeile in `--font-text`. Feste Typo-Skala 13/14/16/19/24/32/48 px ohne
  `clamp()`; unter 480px h1 32px, h2 24px. Abstände nur 8/16/24/32/48/64 px.
  Radius 0 ausnahmslos, keine Schatten, keine Verläufe, alles linksbündig,
  Trennung nur über 1px-Linien. Keine Animationen, keine Einblendungen;
  Bewegung nur 120ms ease auf Farb- und Randwechsel. Zeilenlänge Fliesstext
  max. 68 Zeichen, Einleitung 62.
- Bausteine der Startseite: Farbband 6px `--navy-700`, Kopfzeile 72px mit
  1px `--rule` unten (links Wortmarke, rechts Textlink Impressum),
  Seitenanfang aus h1 + Absatz + `<dl>` + Textlink, Footer auf `--ink` mit
  `--blue-400` für Links. Keine weiteren Bausteine, keine farbigen
  Abzeichen.
- Alle Farben, Schriftgrössen und Abstände sind als Custom Properties in
  `assets/css/main.css` definiert und werden nur dort geändert.

## Struktur

```
/index.html                  Startseite
/impressum.html              Impressum (Rechtstext, Regel 6)
/datenschutz.html            Datenschutzerklärung (Rechtstext, Regel 6)
/404.html                    Fehlerseite (wird von Vercel automatisch genutzt)
/assets/css/main.css         gesamtes CSS
/assets/img/                 Bilder (nur eigene, lokal), favicon.svg
/DESIGN.md                   verbindliche Gestaltungsrichtung
/robots.txt
/sitemap.xml                 nur öffentliche Seiten
/.well-known/security.txt    RFC 9116
/vercel.json                 cleanUrls, trailingSlash, Security-Header
```

## Konventionen

- Interne Links ohne `.html`-Endung (`/impressum`, `/datenschutz`), weil
  `cleanUrls: true` in `vercel.json` gesetzt ist. Kein Trailing Slash.
- Canonical-URL ist immer `https://gutmannholding.com/<pfad>`.
- Neue Seiten: Kopf- und Fussbereich aus `index.html` übernehmen, in
  `sitemap.xml` eintragen (nur wenn öffentlich), Canonical setzen.
- Bei Änderungen an `vercel.json`-Headern: CSP bleibt mindestens so streng
  wie jetzt. `default-src 'none'` und `script-src 'none'` bleiben, nie
  `'unsafe-inline'`. Eine Aufweichung nur nach ausdrücklicher Freigabe.
- Umlaute werden als echte Zeichen geschrieben (UTF-8), nicht als
  HTML-Entities und nicht als ae/oe/ue.
- Zeilenenden LF (siehe `.gitattributes`).
- Dateien unter Windows nicht per Bash-Heredoc schreiben (CRLF-Problem),
  sondern mit dem Write-Tool.
- Git-Autor: `SubmissionOS <rafaelgutmann@gutmannholding.com>`.

## Vor jedem Commit prüfen

- [ ] Kein `<script>` ausser JSON-LD, kein `style=""`, kein `<style>`
- [ ] Keine URL zu fremden Hosts in HTML/CSS (ausser Canonical/OG-URLs auf
      die eigene Domain und die Schema-/Sitemap-Namespaces)
- [ ] Jede Seite: `lang="de"`, eine `h1`, Skip-Link, `<title>`, Meta-Description
- [ ] Verbotsliste aus DESIGN.md Punkt für Punkt: null Treffer
- [ ] Keine Secrets, keine internen Dokumente
- [ ] Rechtstexte nur aus freigegebener Quelle, sonst `TODO: Text ausstehend`
