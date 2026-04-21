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
├── anfragen.html       # Kostenlos-Anfrage Formular
├── logo.svg            # Logo (Volltext)
├── logo-mark.svg       # Logo-Symbol
├── logo-bloom.svg      # Bloom-Variante
├── logo-mark-black.svg # Logo-Symbol schwarz
├── EC_GROUP_Logo.pdf   # Logo PDF
└── EC_GROUP_Symbol.pdf # Symbol PDF
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
| Anfragen | `anfragen.html` | Mehrstufiges Anfrageformular |

## Features

- **Dark / Light Mode** – Toggle-Schalter, gespeichert via `localStorage`
- **DE / EN Sprachumschalter** – vollständige Übersetzung aller Seiten, gespeichert via `localStorage`
- **Service Cycler** – Leistungsbezeichnungen wechseln mit 3D-Tiefenanimation
- **Scroll-Reveal** – Elemente blenden beim Scrollen ein (IntersectionObserver)
- **Canvas-Partikel** – vernetzte Partikel-Animation im Hero-Bereich
- **Prozess-Karussell** – 5-Schritte-Karussell mit CSS scroll-snap, Magic Mouse & Touch
- **Anatomie-Animation** – Wireframe-Diagramm mit staggered Einblend-Animation, zoom-skaliert für Mobile
- **Kostenlos-Anfragen Button** – mehrstufiges Anfrageformular mit mailto-Übergabe

## Mobile

- **Hamburger-Menü** (≤900px): Button mit Slide-Down-Panel
- **Services-Karussell**: Horizontal swipebar mit Dot-Indikatoren
- **Prozess-Karussell** (`prozess.html`): 5 Schritte als native CSS scroll-snap Karussell mit Apple Magic Mouse Support
- **Anatomie-Diagramm**: Zoom-skaliert für alle Bildschirmgrößen (zoom: 0.82 → 0.42)
- **Breakpoints**: 900px (Tablet), 540px, 430px, 390px (Phone)

## Technologie

- **Reines HTML/CSS/JavaScript** – kein Framework, keine Dependencies
- **Google Fonts** – Inter (300–900)
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

## Kontakt

- **E-Mail:** info@vyomedia.de

---

© 2026 VYO Media. Alle Rechte vorbehalten.
