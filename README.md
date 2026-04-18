# EC GROUP – Website

Offizielle Website der EC GROUP, einer kreativen Medienagentur mit Fokus auf Webdesign, App-Entwicklung, Photoshooting und digitale Lösungen.

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
| Startseite | `index.html` | Hero, Leistungen, Stats, Über uns, Prozess, Kontakt |
| Leistungen | `leistungen.html` | Alle Services mit Filteransicht |
| Preise | `preise.html` | Pakete, Pflegepläne, FAQ |
| Prozess | `prozess.html` | Workflow-Erklärung mit Animation |
| Über uns | `ueber-uns.html` | Team, Werte, Geschichte |
| Karriere | `karriere.html` | Offene Stellen, Benefits |

## Mobile

- **Hamburger-Menü** (≤900px): KI-styled Button (Gradient-Linien, Glow) mit Slide-Down-Panel
- **Services-Karussell**: Horizontal swipebar mit Dot-Indikatoren + Slide-in-Animation
- **Stats-Row**: 4 Werte in einer Zeile (kompakte Schrift)
- **Breakpoints**: 900px (Tablet), 540px (Phone)
- Portfolio-Section auf Homepage entfernt — eigene Seite vorhanden

## Technologie

- **Reines HTML/CSS/JavaScript** – kein Framework, keine Dependencies
- **Google Fonts** – Inter (300–900)
- **CSS Custom Properties** – vollständiges Theme-System
- **Dark / Light Mode** – iOS-Toggle, gespeichert via `localStorage`
- **Intersection Observer** – Scroll-Reveal-Animationen
- **Canvas API** – Partikel-Animation im Hero-Bereich

## Hosting

Gehostet via **GitHub Pages** – automatisches Deployment bei jedem `git push` auf `main`.

## Design

- **Primärfarbe:** `#6c63ff` → `#a78bfa` (Lila-Gradient)
- **Dark Mode:** Hintergrund `#000000`, Text `#ffffff`
- **Light Mode:** Hintergrund `#ffffff`, Text `#0a0a0a`
- **Schrift:** Inter, 900 weight für Headlines

## Kontakt

- **E-Mail:** info@ecgroup.de
- **Telefon:** 0511 866 47763
- **Mobil:** 0151 546 28224
- **Support:** 0176 608 08641

---

© 2026 EC GROUP. Alle Rechte vorbehalten.
