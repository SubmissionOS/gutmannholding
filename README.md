# gutmannholding.com

Statische Website der Gutmann Holding Group. Reines HTML5 + CSS, kein
JavaScript, keine Dependencies, kein Build-Step. Der Repository-Inhalt ist
1:1 das Deployment-Artefakt.

Die verbindlichen Projektregeln stehen in [CLAUDE.md](CLAUDE.md).

## Status

Die Gutmann Holding Group FlexCo befindet sich in Gründung. Betreiber der
Website ist derzeit Rafael Gutmann, Einzelunternehmen.

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
sind in `vercel.json` definiert.

## Design-Entscheidung: Weiss statt dunkler Grundton

Der Light-Mode nutzt reines Weiss als Grundfläche, der Dark-Mode ein
neutrales Anthrazit über `prefers-color-scheme`. Weiss wurde als Standard
gewählt, weil es der Erwartung an eine Holding-/Beratungswebsite entspricht
(Briefpapier-Anmutung, hohe Lesbarkeit, druckähnliche Ruhe) und weil
Marineblau als Akzent auf Weiss den besten Kontrast bei geringster
visueller Lautstärke liefert. Ein dunkler Grundton wirkt schnell nach
Tech-Startup und erschwert einen ruhigen, textlastigen Auftritt.

Akzentfarben: Marineblau (Wortmarke, Links) und gedämpftes Messing
(Statuslinie). Mehr gibt es nicht.

## Offene Punkte

- `impressum.html`: Text ausstehend
- `datenschutz.html`: Text ausstehend
- `.well-known/security.txt`: Kontaktadresse ausstehend
- Open-Graph-/Twitter-Bild unter `assets/img/` ausstehend
