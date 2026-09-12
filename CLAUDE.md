# CLAUDE.md – Regelwerk für gutmannholding.com

Dieses Repository ist die öffentliche Website der Gutmann Holding Group.
Der Ordner ist 1:1 das Deployment-Artefakt (Vercel, statisch).
Die folgenden Regeln gelten in jeder Session, ohne Ausnahme.

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
   - Farbkontrast mindestens 4.5:1 für Text (Light- und Dark-Mode)
   - Skip-Link als erstes fokussierbares Element
   - `<html lang="de">`
   - jedes `<img>` hat ein `alt`-Attribut (leer nur bei rein dekorativen Bildern)
   - `prefers-reduced-motion` wird respektiert: jede Animation/Transition wird
     unter `(prefers-reduced-motion: reduce)` deaktiviert

6. **Rechtstexte werden NIE erfunden, geschätzt oder aus dem Netz kopiert.**
   Fehlt ein Rechtstext (Impressum, Datenschutz, AGB o. ä.), enthält die
   betreffende Seite ausschliesslich den Text `TODO: Text ausstehend` und
   der Zustand wird im Output der Session gemeldet. Kein Lorem Ipsum, keine
   Vorlagen, keine "typischen" Formulierungen.

7. **Vor jedem Commit: keine Secrets, keine internen Dokumente.**
   Das Repository ist öffentlich. Keine API-Keys, keine Tokens, keine
   Verträge, keine internen Notizen, keine personenbezogenen Daten ausser
   den gesetzlich verpflichtenden Angaben im Impressum.

## Design-System

- Ästhetik: seriös, zurückhaltend, Beratungs-/Holding-Charakter.
  Kein Startup-Look, keine Verläufe, keine Schatteneffekte, keine Animationen
  ausser dem dezenten Fade des Hero-Texts auf der Startseite.
- Grundton: reines Weiss im Light-Mode, dunkles neutrales Anthrazit im
  Dark-Mode (`prefers-color-scheme`). Begründung siehe `README.md`.
- Maximal zwei Akzentfarben: Marineblau (`--color-accent`) und gedämpftes
  Messing (`--color-accent-2`). Alle Farben sind als Custom Properties in
  `assets/css/main.css` definiert und werden nur dort geändert.
- Typografie: System-Font-Stack, ruhige Hierarchie, viel Weissraum.
  Schriftgrössen über `clamp()` fluid, mobile-first.
- Layout: eine zentrierte Spalte mit `max-width`, Abstände über die
  Spacing-Tokens (`--space-*`).

## Struktur

```
/index.html                  Startseite
/impressum.html              Impressum (Rechtstext, Regel 6)
/datenschutz.html            Datenschutzerklärung (Rechtstext, Regel 6)
/404.html                    Fehlerseite (wird von Vercel automatisch genutzt)
/assets/css/main.css         gesamtes CSS
/assets/img/                 Bilder (nur eigene, lokal)
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
  wie jetzt. Nie `'unsafe-inline'`, nie `script-src`.
- Umlaute werden als echte Zeichen geschrieben (UTF-8), nicht als
  HTML-Entities und nicht als ae/oe/ue.
- Zeilenenden LF (siehe `.gitattributes`).
- Dateien unter Windows nicht per Bash-Heredoc schreiben (CRLF-Problem),
  sondern mit dem Write-Tool.

## Vor jedem Commit prüfen

- [ ] Kein `<script>` ausser JSON-LD, kein `style=""`, kein `<style>`
- [ ] Keine URL zu fremden Hosts in HTML/CSS (ausser Canonical/OG-URLs auf
      die eigene Domain und die Schema-/Sitemap-Namespaces)
- [ ] Jede Seite: `lang="de"`, eine `h1`, Skip-Link, `<title>`, Meta-Description
- [ ] Keine Secrets, keine internen Dokumente
- [ ] Rechtstexte nur aus freigegebener Quelle, sonst `TODO: Text ausstehend`
