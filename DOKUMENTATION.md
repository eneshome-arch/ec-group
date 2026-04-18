# EC GROUP – Technische Dokumentation

## Inhaltsverzeichnis

1. [Theme-System](#theme-system)
2. [Navigation](#navigation)
3. [Animationen](#animationen)
4. [Komponenten](#komponenten)
5. [Mobile](#mobile)
6. [Farbpalette](#farbpalette)
7. [Schriften](#schriften)
8. [Hosting](#hosting)
9. [Kontaktdaten](#kontaktdaten)

---

## Theme-System

### Dark / Light Mode

Alle Seiten unterstützen Dark und Light Mode über ein `data-theme`-Attribut auf dem `<html>`-Element.

```js
// Theme setzen
document.documentElement.setAttribute('data-theme', 'light');
document.documentElement.removeAttribute('data-theme'); // → dark

// Gespeichert in localStorage
localStorage.setItem('ace-theme', 'light' | 'dark');
```

### FOUC-Prävention

Jede Seite enthält direkt im `<head>` folgenden Inline-Script:

```html
<script>
  if(localStorage.getItem('ace-theme')==='light')
    document.documentElement.setAttribute('data-theme','light');
</script>
```

### CSS-Variablen

```css
/* Dark Mode (Standard) */
:root {
  --bg:       #000000;
  --bg2:      #080808;
  --surface:  #0f0f0f;
  --surface2: #161616;
  --border:   rgba(255,255,255,0.07);
  --border2:  rgba(255,255,255,0.12);
  --text:     #ffffff;
  --text2:    #888888;
  --text3:    #444444;
  --accent:   #6c63ff;
  --accent2:  #a78bfa;
  --gradient: linear-gradient(135deg, #6c63ff 0%, #a78bfa 100%);
}

/* Light Mode */
[data-theme="light"] {
  --bg:      #ffffff;
  --bg2:     #f5f5f5;
  --surface: #eeeeee;
  --text:    #0a0a0a;
  --text2:   #555555;
}
```

---

## Navigation

### Struktur

```html
<nav id="navbar">
  <a href="index.html" class="nav-logo">…Logo…</a>
  <ul class="nav-links">
    <li><a href="leistungen.html">Leistungen</a></li>
    <li><a href="ueber-uns.html">Über uns</a></li>
    <li><a href="prozess.html">Prozess</a></li>
    <li><a href="preise.html">Preise</a></li>
    <li><a href="karriere.html">Karriere</a></li>
    <li><a href="#contact">Kontakt</a></li>
  </ul>
</nav>
```

### Scroll-Verhalten

```js
function updateNavBg() {
  const light = document.documentElement.getAttribute('data-theme') === 'light';
  navbar.style.background = window.scrollY > 60
    ? (light ? 'rgba(255,255,255,0.97)' : 'rgba(0,0,0,0.97)')
    : (light ? 'rgba(255,255,255,0.88)' : 'rgba(0,0,0,0.75)');
}
```

---

## Animationen

### Scroll-Reveal

```css
.reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.7s, transform 0.7s; }
.reveal.in { opacity: 1; transform: none; }
```

Verzögerungsklassen: `.reveal-delay-1` bis `.reveal-delay-5` (je +0.1s)

### Hero-Partikel (Canvas)

- **60 Punkte** mit zufälliger Startposition und Bewegungsvektor
- **Verbindungslinien** zwischen Punkten < 110px Abstand
- **Theme-aware:** weiß im Dark Mode, schwarz im Light Mode

### Ticker / Marquee

```css
@keyframes marquee {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
```

---

## Komponenten

### Buttons

```html
<a href="#" class="btn-primary">Text</a>
<a href="#" class="btn-ghost">Text</a>
```

### Karten

```html
<div class="service-card reveal">
  <div class="svc-icon"><svg>…</svg></div>
  <h3>Titel</h3>
  <p>Beschreibung</p>
</div>
```

---

## Mobile

### Hamburger-Menü (≤900px)

Der "Projekt starten" Button wird auf Mobile ausgeblendet und durch einen KI-styled Hamburger ersetzt.

```css
/* KI-Ästhetik: Gradient-Linien mit unterschiedlichen Breiten */
.nav-hamburger span:nth-child(1) { width: 14px; }
.nav-hamburger span:nth-child(2) { width: 22px; }  /* Haupt-Linie */
.nav-hamburger span:nth-child(3) { width: 18px; }
/* Hover: alle Linien auf 22px, lila Glow */
/* Open: morph zu X, Rand leuchtet auf */
```

Das Mobile-Menü (`#mobileMenu`) enthält alle Nav-Links + "Projekt starten" CTA als letzten Eintrag.

### Services-Karussell (Mobile)

Auf ≤900px wird `.services-grid` zu einem horizontalen Swipe-Karussell:
- `scroll-snap-type: x mandatory` — rastet auf jeder Karte ein
- Dot-Indikatoren (`#svcDots`) synchronisieren sich per Scroll-Event
- Karten animieren beim ersten Einblenden von rechts rein (`.svc-visible`)

### Breakpoints

| Breakpoint | Änderungen |
|---|---|
| `≤900px` | Nav-Links ausgeblendet, Hamburger sichtbar, CTA versteckt |
| `≤540px` | Section-Padding reduziert, Stats 4-spaltig, Buttons full-width |

### Homepage

- Portfolio-Section entfernt (eigene Seite `leistungen.html` / Portfolio-Seite vorhanden)
- Hero-Buttons: "Preise ansehen" (Gradient) + "Unser Prozess" (Weiß)

---

## Farbpalette

| Name | Hex | Verwendung |
|---|---|---|
| Accent | `#6c63ff` | Buttons, Highlights |
| Accent 2 | `#a78bfa` | Gradient-Ende, Icons |
| Cyan | `#22d3ee` | Badge-Dot |
| Dark BG | `#000000` | Hintergrund Dark |
| Light BG | `#ffffff` | Hintergrund Light |

---

## Schriften

- **Familie:** Inter (Google Fonts)
- **Gewichte:** 300, 400, 500, 600, 700, 800, 900
- **Headlines:** 900 weight, `letter-spacing: -0.045em`
- **Body:** 400–500 weight, `line-height: 1.75–1.85`

---

## Hosting

- **Plattform:** GitHub Pages
- **Repo:** [github.com/eneshome-arch/ec-group](https://github.com/eneshome-arch/ec-group)
- **Live URL:** [eneshome-arch.github.io/ec-group](https://eneshome-arch.github.io/ec-group/)
- **Deployment:** automatisch bei jedem `git push origin main`

---

## Kontaktdaten

| Art | Wert |
|---|---|
| E-Mail | info@ecgroup.de |
| Festnetz | 0511 866 47763 |
| Mobil (Enes) | 0151 546 28224 |
| Support (Ali) | 0176 608 08641 |

---

*EC GROUP – Kreative Medienagentur · © 2026*
