# VYO Media – Website

Offizielle Website der VYO Media (**Visualize Your Online**), einer kreativen Medienagentur mit Fokus auf Webdesign, Branding, Photoshooting und digitale Lösungen.

## Live

- **GitHub Pages:** [eneshome-arch.github.io/ec-group](https://eneshome-arch.github.io/ec-group/)
- **Custom Domain:** [vyomedia.de](https://vyomedia.de)

## Projektstruktur

```
ec-group-website/
├── index.html          # Startseite
├── leistungen.html     # Leistungen & Services
├── preise.html         # Preisübersicht
├── prozess.html        # Unser Arbeitsprozess
├── ueber-uns.html      # Über die Agentur
├── karriere.html       # Jobs & Karriere
├── anfragen.html       # Kostenlos-Anfrage Formular (9-stufig)
├── datenschutz.html    # Datenschutzerklärung (DSGVO)
├── impressum.html      # Impressum (§ 5 TMG)
├── sitemap.xml         # XML-Sitemap für Suchmaschinen
├── robots.txt          # Crawler-Anweisungen
├── fonts/              # Self-hosted Inter Schriftart (woff2)
│   ├── inter.css       # @font-face Deklarationen
│   └── *.woff2         # 14 Schriftdateien (normal + italic)
├── images/             # Hintergrundbilder (Unsplash, freie Lizenz)
│   ├── teal-waves.jpg        # index.html CTA
│   ├── code-screen.jpg       # index.html Prozess-Section
│   ├── hannover.jpg          # ueber-uns.html CTA
│   ├── workspace.jpg         # leistungen.html CTA
│   ├── conference-room.jpg   # prozess.html Karussell Schritt 1
│   ├── wireframe.jpg         # prozess.html Karussell Schritt 2
│   ├── ux-tablet.jpg         # prozess.html Karussell Schritt 3
│   ├── code-monitor.jpg      # prozess.html Karussell Schritt 4
│   ├── neon-rocket.jpg       # prozess.html Karussell Schritt 5
│   ├── abstract-green.jpg    # prozess.html Timeline-Section
│   ├── neon-code.jpg         # preise.html Hero
│   ├── laptop-abstract.jpg   # preise.html Wartungs-Section
│   ├── neon-green.jpg        # preise.html CTA
│   ├── keyboard.jpg          # karriere.html Hero
│   ├── team-brainstorm.jpg   # karriere.html Benefits-Section
│   ├── modern-office.jpg     # karriere.html Culture-Section
│   ├── city-neon.jpg         # karriere.html Jobs-Section
│   └── neon-streaks.jpg      # karriere.html CTA
├── logo.svg
├── logo-mark.svg
├── logo-bloom.svg
├── logo-mark-black.svg
├── EC_GROUP_Logo.pdf
└── EC_GROUP_Symbol.pdf
```

## Seiten

| Seite | Datei | Beschreibung |
|---|---|---|
| Startseite | `index.html` | Hero, Leistungen, Stats, Prozess, Kontakt |
| Leistungen | `leistungen.html` | Alle Services mit Filteransicht |
| Preise | `preise.html` | Pakete, Pflegepläne, FAQ |
| Prozess | `prozess.html` | Workflow-Karussell, Anatomie-Diagramm, Timeline |
| Über uns | `ueber-uns.html` | Agentur-Profil, Expertise, Werte, Geschichte |
| Karriere | `karriere.html` | Offene Stellen, Benefits, Kultur |
| Anfragen | `anfragen.html` | 9-stufiges Anfrageformular mit mailto-Übergabe |
| Datenschutz | `datenschutz.html` | DSGVO-konforme Datenschutzerklärung |
| Impressum | `impressum.html` | Impressum gemäß § 5 TMG |

## Features

- **Dark / Light Mode** – Toggle-Schalter, gespeichert via `localStorage`
- **DE / EN Sprachumschalter** – vollständige Übersetzung aller Seiten, gespeichert via `localStorage`
- **Service Cycler** – Leistungsbezeichnungen wechseln mit 3D-Tiefenanimation
- **Scroll-Reveal** – Elemente blenden beim Scrollen ein (IntersectionObserver)
- **Canvas-Partikel** – vernetzte Partikel-Animation im Hero-Bereich
- **Prozess-Karussell** – 5-Schritte-Karussell mit CSS scroll-snap, Magic Mouse & Touch
- **Anatomie-Animation** – Wireframe-Diagramm mit staggered Einblend-Animation, zoom-skaliert für Mobile
- **Anfragen-Formular** – 9-stufiges Fragebogen-Formular, alle Buttons sitewide verlinken hierauf
- **Hintergrundbilder** – 18 einzigartige Unsplash-Fotos als subtile Sektions-Hintergründe (dunkler Overlay)
- **Weiche Sektions-Übergänge** – Gradient-Fades an allen Section-Rändern für fließende Übergänge

## Hintergrundbilder

Alle Bilder stammen von [Unsplash](https://unsplash.com) und sind zur freien kommerziellen Nutzung ohne Namensnennung lizenziert. Jedes Bild wird sitewide **genau einmal** verwendet.

### Technische Umsetzung

Bilder werden als CSS `background-image` mit einem dunklen Overlay eingebunden:

```css
background-image:
  linear-gradient(rgba(0,0,0,1) 0%, transparent 18%, transparent 82%, rgba(0,0,0,1) 100%),
  linear-gradient(rgba(0,0,0,0.84), rgba(0,0,0,0.84)),
  url('images/example.jpg');
background-size: cover;
background-position: center;
```

Der erste Gradient-Layer erzeugt weiche Kanten (Schwarz → transparent → Schwarz), der zweite dunkelt das Bild einheitlich ab. Im Light Mode werden alle Bilder deaktiviert (`background-image: none`).

**Ausnahme:** Die CTA-Section auf `ueber-uns.html` (Hannover-Foto) hat keine Kanten-Fades, um das Bild vollständig sichtbar zu lassen.

## Sektions-Übergänge

Weiche Übergänge zwischen Sektionen via zwei Methoden:

1. **Sections mit Hintergrundbild** – Edge-Fade-Gradient direkt im `background-image` (Schwarz an Top/Bottom)
2. **Alle Sections** – Universelle `section::before`/`::after` Pseudo-Elemente (80px, `var(--bg)` Gradient)

```css
section::before { top: 0; background: linear-gradient(to bottom, var(--bg), transparent); }
section::after  { bottom: 0; background: linear-gradient(to top, var(--bg), transparent); }
```

## SEO

- **Title-Tags** – keywordoptimiert mit „Webdesign Hannover" auf allen Seiten
- **Meta Descriptions** – individuelle Beschreibungen pro Seite
- **Open Graph Tags** – für Social-Media-Previews
- **Schema.org LocalBusiness** – strukturierte Daten auf `index.html`
- **sitemap.xml** – alle 6 öffentlichen Seiten, eingereicht in Google Search Console
- **robots.txt** – Formulare und rechtliche Seiten von Indexierung ausgeschlossen
- **Canonical URLs** – auf jeder Seite gesetzt

## DSGVO / Datenschutz

- **Keine Cookies** – nur `localStorage` für funktionale Einstellungen (Theme, Sprache)
- **Kein Tracking** – kein Google Analytics, kein Meta Pixel, keine externen Tracker
- **Self-hosted Fonts** – Inter lokal gehostet, kein Google Fonts CDN-Aufruf
- **Datenschutzerklärung** – inkl. GitHub Pages (Hosting), localStorage, E-Mail-Kontakt, Betroffenenrechte, Aufsichtsbehörde Niedersachsen
- **Impressum** – angelegt, vollständige Angaben nach Gewerbeanmeldung zu ergänzen

## Mobile

- **Hamburger-Menü** (≤900px): Button mit Slide-Down-Panel
- **Services-Karussell**: Horizontal swipebar mit Dot-Indikatoren
- **Prozess-Karussell** (`prozess.html`): 5 Schritte als native CSS scroll-snap Karussell mit Apple Magic Mouse Support
- **Anatomie-Diagramm**: Zoom-skaliert für alle Bildschirmgrößen (zoom: 0.82 → 0.42)
- **Breakpoints**: 900px (Tablet), 540px, 430px, 390px (Phone)

## Technologie

- **Reines HTML/CSS/JavaScript** – kein Framework, keine Dependencies
- **Self-hosted Fonts** – Inter (300–900), lokal gespeichert in `/fonts/`
- **CSS Custom Properties** – vollständiges Theme-System
- **Intersection Observer** – Scroll-Reveal-Animationen
- **Canvas API** – Partikel-Animation im Hero-Bereich

## Design

- **Primärfarbe:** `#7ec8a0` → `#b5e8cc` (Pastellgrün-Gradient)
- **Dark Mode:** Hintergrund `#000000`, Text `#ffffff`
- **Light Mode:** Hintergrund `#f0faf5` (helles Pastellgrün), Text `#0a2118`
- **Schrift:** Inter, 900 weight für Headlines

## Hosting

Gehostet via **GitHub Pages** – automatisches Deployment bei jedem `git push` auf `main`.  
Custom Domain: **vyomedia.de** (DNS via Ionos, 4× A-Record + CNAME www)

## Offene TODOs

- [ ] Impressum: vollständige Adresse nach Gewerbeanmeldung eintragen
- [ ] Impressum: Steuernummer / USt-IdNr. nach Finanzamt-Zuteilung ergänzen
- [ ] Google Search Console: Domain verifizieren + sitemap.xml einreichen
- [ ] Google Business Profil erstellen (Hannover)
- [ ] Social-Media-Links im Footer ergänzen (Instagram, LinkedIn, Behance)

## Kontakt

- **E-Mail:** info@vyomedia.de
- **Telefon:** 0511 866 47763

---

© 2026 VYO Media. Alle Rechte vorbehalten.
