# EC GROUP – Technische Dokumentation

## Inhaltsverzeichnis

1. [Theme-System](#theme-system)
2. [Sprachsystem](#sprachsystem)
3. [Navigation](#navigation)
4. [Animationen](#animationen)
5. [Komponenten](#komponenten)
6. [Mobile](#mobile)
7. [Farbpalette](#farbpalette)
8. [Schriften](#schriften)
9. [Hosting](#hosting)
10. [Kontaktdaten](#kontaktdaten)

---

## Theme-System

### Dark / Light Mode

Alle Seiten unterstützen Dark und Light Mode über ein `data-theme`-Attribut auf dem `<html>`-Element. Der Light Mode verwendet ein helles Pastellgrün statt Weiß.

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
  --accent:   #7ec8a0;
  --accent2:  #b5e8cc;
  --gradient: linear-gradient(135deg, #7ec8a0 0%, #b5e8cc 100%);
  --glow:     rgba(126,200,160,0.15);
}

/* Light Mode (Pastellgrün) */
[data-theme="light"] {
  --bg:      #f0faf5;
  --bg2:     #e3f5eb;
  --surface: #d4eddf;
  --surface2:#c5e6d3;
  --border:  rgba(0,80,40,0.1);
  --border2: rgba(0,80,40,0.18);
  --text:    #0a2118;
  --text2:   #3a6b52;
  --text3:   #7aab90;
  --glow:    rgba(126,200,160,0.12);
}
```

---

## Sprachsystem

### DE / EN Umschalter

Alle Seiten unterstützen eine vollständige Übersetzung zwischen Deutsch und Englisch. Die gewählte Sprache wird in `localStorage` gespeichert.

```js
// Sprache setzen
localStorage.setItem('ace-lang', 'en' | 'de');
```

### Implementierung

Jedes übersetzbare Element erhält ein `data-i18n`-Attribut:

```html
<h2 data-i18n="hero-title">Design, das bewegt.</h2>
<p data-i18n="hero-sub">EC GROUP ist deine Medienagentur…</p>
```

Die `applyLang()`-Funktion wechselt alle Texte:

```js
const translations = {
  de: { 'hero-title': 'Design, das bewegt.', … },
  en: { 'hero-title': 'Design that moves.', … }
};

function applyLang(lang) {
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.getAttribute('data-i18n');
    if (translations[lang][key] !== undefined)
      el.textContent = translations[lang][key];
  });
  langToggleBtn.textContent = lang === 'de' ? 'EN' : 'DE';
  localStorage.setItem('ace-lang', lang);
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
  <div class="nav-right">
    <!-- Reihenfolge: Theme-Toggle → Lang-Toggle → Hamburger → CTA -->
    <label class="theme-toggle">…</label>
    <button class="lang-toggle" id="langToggle">EN</button>
    <button class="nav-hamburger" id="navHamburger">…</button>
    <a href="#contact" class="nav-cta">Projekt starten</a>
  </div>
</nav>
```

### Scroll-Verhalten

```js
function updateNavBg() {
  const light = document.documentElement.getAttribute('data-theme') === 'light';
  navbar.style.background = window.scrollY > 60
    ? (light ? 'rgba(240,250,245,0.97)' : 'rgba(0,0,0,0.97)')
    : (light ? 'rgba(240,250,245,0.88)' : 'rgba(0,0,0,0.75)');
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
- **Verbindungslinien** zwischen Punkten < 110px Abstand, Farbe `rgba(126,200,160,…)`
- **Theme-aware:** weiß im Dark Mode, schwarz im Light Mode

### Service Cycler

Ersetzt den alten Marquee-Ticker. Zeigt eine Leistung nach der anderen mit einer 3D-Tiefenanimation: Das Wort kommt von hinten (klein, transparent) nach vorne (normale Größe, sichtbar) und verschwindet wieder nach hinten.

```css
.cycler-word {
  opacity: 0; transform: translateZ(-80px) scale(0.6);
  transition: opacity 0.55s ease, transform 0.55s ease;
}
.cycler-word.active { opacity: 1; transform: translateZ(0) scale(1); }
.cycler-word.exit   { opacity: 0; transform: translateZ(-80px) scale(0.6); }
```

Wechselintervall: 2400ms

---

## Komponenten

### Buttons

```html
<a href="#" class="btn-primary">Text</a>
<a href="#" class="btn-ghost">Text</a>
```

### Lang-Toggle

```html
<button class="lang-toggle" id="langToggle">EN</button>
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

Der "Projekt starten" Button wird auf Mobile ausgeblendet und durch einen Hamburger ersetzt.

```css
.nav-hamburger span:nth-child(1) { width: 14px; }
.nav-hamburger span:nth-child(2) { width: 22px; }
.nav-hamburger span:nth-child(3) { width: 18px; }
```

Das Mobile-Menü (`#mobileMenu`) enthält alle Nav-Links + "Projekt starten" CTA.

### Services-Karussell (Mobile)

Auf ≤900px wird `.services-grid` zu einem horizontalen Swipe-Karussell:
- `scroll-snap-type: x mandatory`
- Dot-Indikatoren (`#svcDots`) synchronisieren sich per Scroll-Event

### Breakpoints

| Breakpoint | Änderungen |
|---|---|
| `≤900px` | Nav-Links ausgeblendet, Hamburger sichtbar, CTA versteckt |
| `≤540px` | Section-Padding reduziert, Buttons full-width |

---

## Farbpalette

| Name | Hex | Verwendung |
|---|---|---|
| Accent (Pastellgrün) | `#7ec8a0` | Buttons, Highlights, Labels |
| Accent 2 | `#b5e8cc` | Gradient-Ende, Icons |
| Cyan | `#22d3ee` | Badge-Dot (animiert) |
| Dark BG | `#000000` | Hintergrund Dark Mode |
| Light BG | `#f0faf5` | Hintergrund Light Mode (Pastellgrün) |

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
