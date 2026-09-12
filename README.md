# gutmannholding.com

Statische Website der Gutmann Holding Group. Reines HTML5 + CSS, kein
JavaScript, keine Dependencies, kein Build-Step. Der Repository-Inhalt ist
1:1 das Deployment-Artefakt.

Die verbindlichen Projektregeln stehen in [CLAUDE.md](CLAUDE.md), die
verbindliche Gestaltung in `DESIGN.md`.

## Status

Die Gutmann Holding Group befindet sich in Gründung. Betreiber der
Website ist derzeit Rafael Gutmann, Einzelunternehmen, Deutschland.

## Lokal ansehen

Es gibt nichts zu bauen. `index.html` direkt im Browser öffnen oder einen
beliebigen statischen Server im Repo-Root starten, zum Beispiel:

```
python -m http.server 8000
```

Hinweis: Lokal funktionieren die Links `/impressum` und `/datenschutz` ohne
`.html`-Endung nur mit einem Server, der Clean URLs unterstützt. Auf Vercel
übernimmt das `cleanUrls: true` in `vercel.json`.

## Deployment

Vercel, statisch, ohne Framework-Preset. Security-Header und URL-Verhalten
sind in `vercel.json` definiert. Die Content-Security-Policy ist
`default-src 'none'` mit `script-src 'none'` und `connect-src 'self'`; das
JSON-LD-Markup auf der Startseite ist davon nicht betroffen, weil der
Browser `type="application/ld+json"` nicht als Skript ausführt.

## Gestaltung

Die Gestaltung folgt `DESIGN.md`. Kurzfassung: ein einziges helles
Farbschema auf Weiss, kein Dark Mode, zehn Farb-Tokens, Serifen für
Überschriften in Gewicht 400, feste Typo-Skala ohne `clamp()`, Abstände
nur 8/16/24/32/48/64 px, Radius 0, keine Schatten, keine Verläufe, keine
Bewegung ausser 120ms-Farbwechseln, alles linksbündig, Trennung nur über
1px-Linien. Das Stylesheet ist `assets/css/main.css`.

## Externe Ressourcen: keine

Kein JavaScript, keine Schriften, Bilder oder Skripte von fremden Servern,
keine Cookies. Das Favicon liegt lokal unter `assets/img/favicon.svg`.

## Offene Punkte

- `DESIGN.md` im Projektwurzelverzeichnis ablegen (liegt noch nicht vor)
- Open-Graph-Bild unter `assets/img/` ausstehend, og:image und twitter:image
  kommen erst mit dem Asset zurück
