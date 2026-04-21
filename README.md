# EC GROUP – Website

Offizielle Website der EC GROUP, einer kreativen Medienagentur mit Fokus auf Webdesign, Branding, Photoshooting und digitale Lösungen. Weltweit tätig.

## Live

[eneshome-arch.github.io/ec-group](https://eneshome-arch.github.io/ec-group/)

## Projektstruktur

```
ec-group-website/
├── index.html          # Startseite
├── leistungen.html     # Leistungen & Services
├── preise.html         # Preisübersicht
├── prozess.html        # Unser Arbeitsprozess
├── ueber-uns.html      # Über das Team
├── karriere.html       # Jobs & Karriere
├── EC_GROUP_Logo.pdf   # Logo (hell & dunkel)
└── EC_GROUP_Symbol.pdf # Logo-Symbol (weiß, A4)
```

## Seiten

| Seite | Datei | Beschreibung |
|---|---|---|
| Startseite | `index.html` | Hero, Leistungen, Stats, Prozess, Kontakt |
| Leistungen | `leistungen.html` | Alle Services mit Filteransicht |
| Preise | `preise.html` | Pakete, Pflegepläne, FAQ |
| Prozess | `prozess.html` | Workflow-Erklärung mit Animation |
| Über uns | `ueber-uns.html` | Team, Werte, Geschichte |
| Karriere | `karriere.html` | Offene Stellen, Benefits |

## Features

- **Dark / Light Mode** – Toggle-Schalter, gespeichert via `localStorage`
- **DE / EN Sprachumschalter** – vollständige Übersetzung aller Seiten, gespeichert via `localStorage`
- **Service Cycler** – Leistungsbezeichnungen wechseln mit 3D-Tiefenanimation (von hinten nach vorne)
- **Internationaler Auftritt** – "Weltweit verfügbar" im Hero, internationale Stat-Box
- **Scroll-Reveal** – Elemente blenden beim Scrollen ein (IntersectionObserver, threshold 0)
- **Canvas-Partikel** – vernetzte Partikel-Animation im Hero-Bereich
- **Prozess-Karussell** – 5-Schritte-Karussell mit CSS scroll-snap, Magic Mouse & Touch
- **Anatomie-Animation** – Wireframe-Diagramm mit staggered Einblend-Animation, zoom-skaliert für Mobile

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

## Kontakt

- **E-Mail:** info@ecgroup.de
- **Telefon:** 0511 866 47763
- **Mobil:** 0151 546 28224
- **Support:** 0176 608 08641

---

© 2026 EC GROUP. Alle Rechte vorbehalten.
