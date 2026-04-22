# VYO Media – Technische Dokumentation

## Inhaltsverzeichnis

1. [Theme-System](#theme-system)
2. [Sprachsystem](#sprachsystem)
3. [Navigation](#navigation)
4. [Animationen](#animationen)
5. [Hintergrundbilder](#hintergrundbilder)
6. [Sektions-Übergänge](#sektions-übergänge)
7. [Komponenten](#komponenten)
8. [Mobile](#mobile)
9. [SEO](#seo)
10. [Schriften](#schriften)
11. [DSGVO](#dsgvo)
12. [Farbpalette](#farbpalette)
13. [Hosting](#hosting)
14. [Kontaktdaten](#kontaktdaten)

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
  --surface: #ffffff;
  --surface2:#edf7f2;
  --border:  rgba(0,80,40,0.1);
  --border2: rgba(0,80,40,0.18);
  --text:    #0a2118;
  --text2:   #3a6b52;
  --text3:   #7aab90;
}
```

---

## Sprachsystem

### DE / EN Umschalter

Alle Seiten unterstützen eine vollständige Übersetzung zwischen Deutsch und Englisch. Die gewählte Sprache wird in `localStorage` gespeichert.

```js
localStorage.setItem('ace-lang', 'en' | 'de');
```

### Implementierung

Jedes übersetzbare Element erhält ein `data-i18n`-Attribut:

```html
<h2 data-i18n="hero-title">Design, das bewegt.</h2>
<p data-i18n="hero-sub">VYO Media ist deine Medienagentur…</p>
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
    <a href="anfragen.html" class="nav-cta">kostenlos Anfragen</a>
  </div>
</nav>
```

### Anfragen-Buttons

**Wichtig:** Alle CTA- und Anfragen-Buttons auf sämtlichen Seiten verlinken auf `anfragen.html` – nicht auf `mailto:` oder `#contact`. Die einzige Ausnahme sind Job-Bewerbungslinks in `karriere.html` (dort bleibt `mailto:`).

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

Verzögerungsklassen: `.reveal-delay-1` bis `.reveal-delay-4` (je +0.1s)

### Hero-Partikel (Canvas)

- **60 Punkte** mit zufälliger Startposition und Bewegungsvektor
- **Verbindungslinien** zwischen Punkten < 110px Abstand, Farbe `rgba(126,200,160,…)`
- **Theme-aware:** weiß im Dark Mode, schwarz im Light Mode

### Service Cycler

Zeigt eine Leistung nach der anderen mit einer 3D-Tiefenanimation: Das Wort kommt von hinten (klein, transparent) nach vorne (normale Größe, sichtbar) und verschwindet wieder nach hinten.

```css
.cycler-word {
  opacity: 0; transform: translateZ(-80px) scale(0.6);
  transition: opacity 0.55s ease, transform 0.55s ease;
}
.cycler-word.active { opacity: 1; transform: translateZ(0) scale(1); }
.cycler-word.exit   { opacity: 0; transform: translateZ(-80px) scale(0.6); }
```

Wechselintervall: 2400ms

### Prozess-Karussell (`prozess.html`)

5 Schritte als natives CSS scroll-snap Karussell. Unterstützt Touch, Apple Magic Mouse (wheel deltaX) und Prev/Next-Buttons.

```css
.steps-track-wrap {
  overflow-x: scroll;
  scroll-snap-type: x mandatory;
}
.step-card { flex: 0 0 100%; scroll-snap-align: start; }
```

### Anatomie-Diagramm (`prozess.html`)

840px breites Wireframe-Diagramm mit Annotationen. Auf Mobile via CSS `zoom` proportional skaliert:

```css
@media (max-width: 900px) { .anatomy-diagram { zoom: 0.82; } }
@media (max-width: 720px) { .anatomy-diagram { zoom: 0.66; } }
@media (max-width: 560px) { .anatomy-diagram { zoom: 0.52; } }
@media (max-width: 430px) { .anatomy-diagram { zoom: 0.42; } }
```

Animation wird per IntersectionObserver auf `.anatomy-section` ausgelöst (nicht auf dem Diagramm selbst, da es auf schmalen Viewports überlaufen kann).

### Bekannte CSS-Falle: `.cta-glow`

```css
/* FALSCH – wird durch .cta-section > * { position: relative } überschrieben */
.cta-glow { position: absolute; … }

/* RICHTIG */
.cta-glow { position: absolute !important; … }
```

`.cta-section > * { position: relative; z-index: 1; }` hat dieselbe Spezifität wie `.cta-glow { position: absolute; }` und steht weiter unten im CSS → überschreibt es. Ohne `!important` wird `.cta-glow` (400px hoch) als Block-Element gerendert und erzeugt einen 400px Leerraum vor dem CTA-Inhalt.

---

## Hintergrundbilder

### Übersicht

Alle 18 Bilder stammen von [Unsplash](https://unsplash.com) (freie kommerzielle Lizenz, keine Namensnennung nötig). Jedes Bild wird sitewide **genau einmal** verwendet.

| Datei | Seite / Section |
|---|---|
| `teal-waves.jpg` | index.html CTA |
| `code-screen.jpg` | index.html Prozess-Section |
| `hannover.jpg` | ueber-uns.html CTA |
| `workspace.jpg` | leistungen.html CTA |
| `conference-room.jpg` | prozess.html Karussell Schritt 1 |
| `wireframe.jpg` | prozess.html Karussell Schritt 2 |
| `ux-tablet.jpg` | prozess.html Karussell Schritt 3 |
| `code-monitor.jpg` | prozess.html Karussell Schritt 4 |
| `neon-rocket.jpg` | prozess.html Karussell Schritt 5 |
| `abstract-green.jpg` | prozess.html Timeline |
| `neon-code.jpg` | preise.html Hero |
| `laptop-abstract.jpg` | preise.html Wartungs-Section |
| `neon-green.jpg` | preise.html CTA |
| `keyboard.jpg` | karriere.html Hero |
| `team-brainstorm.jpg` | karriere.html Benefits |
| `modern-office.jpg` | karriere.html Culture |
| `city-neon.jpg` | karriere.html Jobs |
| `neon-streaks.jpg` | karriere.html CTA |

### CSS-Muster (Standard)

```css
.section {
  background-image:
    linear-gradient(rgba(0,0,0,1) 0%, transparent 18%, transparent 82%, rgba(0,0,0,1) 100%),
    linear-gradient(rgba(0,0,0,0.84), rgba(0,0,0,0.84)),
    url('images/example.jpg');
  background-size: cover;
  background-position: center;
}
[data-theme="light"] .section { background-image: none; }
```

Der erste Layer erzeugt Kanten-Fades (Schwarz oben/unten), der zweite dunkelt das Bild ab. Im Light Mode werden alle Bilder deaktiviert.

**Ausnahme:** `ueber-uns.html` CTA (hannover.jpg) hat keinen Kanten-Fade-Layer und keine `::before`/`::after` Pseudo-Elemente, damit das Bild vollständig wirkt.

---

## Sektions-Übergänge

Weiche Übergänge zwischen Sektionen über zwei Ebenen:

### 1. Kanten-Fade in background-image

Für alle Sektionen mit Hintergrundbild wird ein zusätzlicher Gradient-Layer als erster Layer eingebunden:

```css
linear-gradient(rgba(0,0,0,1) 0%, transparent 18%, transparent 82%, rgba(0,0,0,1) 100%)
```

Das Bild löst sich oben und unten in Schwarz auf, statt abrupt zu enden.

### 2. Universelle section::before / ::after

Für alle Sektionen (auch ohne Hintergrundbild):

```css
section { position: relative; }
section::before, section::after {
  content: ''; position: absolute;
  left: 0; right: 0; height: 80px;
  pointer-events: none; z-index: 2;
}
section::before { top: 0; background: linear-gradient(to bottom, var(--bg), transparent); }
section::after  { bottom: 0; background: linear-gradient(to top, var(--bg), transparent); }
```

Diese Regel ist in jeder HTML-Datei im `<style>`-Block nach `.section-dark` eingefügt.

### Ausnahme deaktivieren

```css
/* Fades für eine spezifische Section deaktivieren */
.cta-section::before, .cta-section::after { content: none; }
```

---

## Komponenten

### Buttons

```html
<a href="anfragen.html" class="btn-primary">Text</a>
<a href="anfragen.html" class="btn-ghost">Text</a>
```

### Lang-Toggle

```html
<button class="lang-toggle" id="langToggle">EN</button>
```

### Karten (Service / Value / Expertise)

```html
<div class="value-card reveal">
  <div class="value-icon"><svg>…</svg></div>
  <h3>Titel</h3>
  <p>Beschreibung</p>
</div>
```

### Anfrageformular (`anfragen.html`)

9-stufiges Formular:
1. Projekttyp
2. Branche
3. Zielgruppe
4. Design-Stil
5. Farbwelt
6. Seitenstruktur
7. Funktionen
8. Budget & Zeitplan
9. Kontaktdaten

Übermittlung via `mailto:`-Link mit vorausgefülltem Betreff und Body:

```js
window.location.href = 'mailto:info@vyomedia.de?subject=' + subject + '&body=' + body;
```

---

## Mobile

### Hamburger-Menü (≤900px)

Der CTA-Button wird auf Mobile ausgeblendet und durch einen Hamburger ersetzt.

```css
.nav-hamburger span:nth-child(1) { width: 14px; }
.nav-hamburger span:nth-child(2) { width: 22px; }
.nav-hamburger span:nth-child(3) { width: 18px; }
```

Das Mobile-Menü (`#mobileMenu`) enthält alle Nav-Links + CTA.

### Services-Karussell (Mobile)

Auf ≤900px wird `.services-grid` zu einem horizontalen Swipe-Karussell:
- `scroll-snap-type: x mandatory`
- Dot-Indikatoren (`#svcDots`) synchronisieren sich per Scroll-Event

### Breakpoints

| Breakpoint | Änderungen |
|---|---|
| `≤900px` | Nav-Links ausgeblendet, Hamburger sichtbar, CTA versteckt |
| `≤720px` | Anatomie-Diagramm zoom: 0.66 |
| `≤560px` | Anatomie-Diagramm zoom: 0.52 |
| `≤540px` | Section-Padding reduziert, Buttons full-width, overflow-x hidden |
| `≤430px` | Anatomie-Diagramm zoom: 0.42 |
| `≤390px` | Minimales Padding, Timeline-Abstände reduziert |
| `hover: none` | Hover-Transforms deaktiviert (Touch-Geräte) |

---

## SEO

### Implementierung

Jede Seite enthält:

```html
<title>Keyword-optimierter Titel – VYO Media Hannover</title>
<meta name="description" content="…max. 160 Zeichen…">
<meta name="keywords" content="Webdesign Hannover, Medienagentur Hannover, …">
<link rel="canonical" href="https://vyomedia.de/seite.html">
<meta property="og:type" content="website">
<meta property="og:title" content="…">
<meta property="og:description" content="…">
<meta property="og:url" content="…">
<meta property="og:site_name" content="VYO Media">
<meta property="og:locale" content="de_DE">
```

### Schema.org (`index.html`)

```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "VYO Media",
  "address": { "addressLocality": "Hannover", "addressCountry": "DE" },
  "areaServed": { "@type": "City", "name": "Hannover" }
}
```

### sitemap.xml

Enthält alle 6 öffentlichen Seiten (anfragen, datenschutz, impressum ausgeschlossen). Bei Domain-Wechsel URLs anpassen.

### robots.txt

```
User-agent: *
Allow: /
Disallow: /anfragen.html
Sitemap: https://vyomedia.de/sitemap.xml
```

---

## Schriften

- **Familie:** Inter – **self-hosted** in `/fonts/` (DSGVO-konform, kein Google CDN)
- **Gewichte:** 300–900 (variable font, normal + italic 400)
- **Dateien:** 14 woff2-Dateien + `fonts/inter.css`
- **Einbindung:** `<link rel="stylesheet" href="fonts/inter.css">` auf allen Seiten
- **Headlines:** 900 weight, `letter-spacing: -0.045em`
- **Body:** 400–500 weight, `line-height: 1.75–1.85`

> **Hinweis:** Kein `<link rel="preconnect" href="https://fonts.googleapis.com">` mehr nötig – alle Fonts sind lokal.

---

## DSGVO

### Cookies

Diese Website setzt **keine Cookies**. Es wird ausschließlich `localStorage` für funktionale Einstellungen verwendet:

| Key | Inhalt |
|---|---|
| `ace-theme` | `'light'` oder `'dark'` |
| `ace-lang` | `'de'` oder `'en'` |

Kein Cookie-Banner nötig.

### Tracking

Kein Google Analytics, kein Meta Pixel, keine externen Tracker.

### Hosting (GitHub Pages)

GitHub Inc. (USA) verarbeitet Server-Logs. Rechtsgrundlage für Drittlandübermittlung: EU-Standardvertragsklauseln + EU-US Data Privacy Framework. Details in `datenschutz.html`.

### Impressum

`impressum.html` ist angelegt. Fehlende Pflichtangaben (Adresse, Steuernummer) sind gelb markiert und nach Gewerbeanmeldung einzutragen.

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

## Hosting

- **Plattform:** GitHub Pages
- **Repo:** [github.com/eneshome-arch/ec-group](https://github.com/eneshome-arch/ec-group)
- **Live URL:** [eneshome-arch.github.io/ec-group](https://eneshome-arch.github.io/ec-group/)
- **Custom Domain:** [vyomedia.de](https://vyomedia.de) (DNS via Ionos)
- **Deployment:** automatisch bei jedem `git push origin main`

### DNS-Konfiguration (Ionos)

| Typ | Host | Wert |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `eneshome-arch.github.io` |

---

## Kontaktdaten

| Art | Wert |
|---|---|
| E-Mail | info@vyomedia.de |
| Telefon | 0511 866 47763 |
| Mobil | 0151 546 28224 |
| Support | 0176 608 08641 |

---

*VYO Media – Kreative Medienagentur · © 2026*
