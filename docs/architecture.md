# Kamba Hopo — Architecture Document (Lite)

## 1. Introduction

### 1.1 Starter Template / Existing Project

Este proyecto **NO es greenfield** — ya existe un sitio funcional deployado:

- **Source:** `outputs/kamba-hopo-lp/index.html` (~920 líneas, single file)
- **Deploy:** Vercel (`p18-sitio-kamba-hopo.vercel.app`)
- **Variantes descartadas:** `outputs/premium-design/forest-green/` y `obsidian-gold/`

La arquitectura documenta el sitio existente y define las guías para implementar Epic 1 (6 stories de mejora) sin romper lo que ya funciona.

### 1.2 Architectural Constraints

- Single HTML file con CSS y JS inline — no separar a menos que sea necesario
- Vanilla JS (no frameworks) — mantener
- Google Fonts como único recurso externo — mantener
- Deploy estático en Vercel — mantener
- No build step — mantener

### 1.3 Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2026-02-28 | 1.0 | Versión inicial — Architecture Lite | Aria |

---

## 2. High Level Architecture

### 2.1 Technical Summary

Sitio estático single-page servido desde Vercel Edge Network. Un único archivo HTML (~920 líneas) contiene markup semántico, CSS custom properties inline y JavaScript vanilla modular para animaciones e interacciones. Sin backend, sin API, sin base de datos. El único punto de integración externo es Google Fonts (CDN) y WhatsApp (deep link `wa.me`). La arquitectura prioriza performance extrema (zero dependencies) y simplicidad de mantenimiento (un solo archivo para editar).

### 2.2 Platform and Infrastructure

**Platform:** Vercel (Free Tier)
**Key Services:** Vercel Edge Network (CDN global), Vercel Analytics (opcional)
**Region:** Auto (edge — servido desde el nodo más cercano al visitante)

| Opción | Pros | Contras | Veredicto |
|--------|------|---------|-----------|
| **Vercel** | Ya configurado, CDN gratis, deploy automático, analytics integrado | Free tier limitado (100GB BW) | **Seleccionado** |
| GitHub Pages | Gratis, integrado con repo | Sin analytics nativo, sin edge functions, config limitada | Descartado |
| Netlify | Similar a Vercel, forms incluidos | Requiere migración, sin ventaja clara | Descartado |

### 2.3 Repository Structure

```
p18-sitio-kamba-hopo/
├── outputs/
│   └── kamba-hopo-lp/
│       ├── index.html          ← Producción (single file)
│       ├── favicon.svg         ← Story 1.3 (por crear)
│       ├── og-image.png        ← Story 1.4 (por crear)
│       ├── sitemap.xml         ← Story 1.5 (por crear)
│       └── robots.txt          ← Story 1.5 (por crear)
├── outputs/premium-design/     ← Variantes (archivo/referencia)
│   ├── forest-green/
│   └── obsidian-gold/
├── docs/
│   ├── prd.md                  ← PRD v1.1
│   └── architecture.md         ← Este documento
├── vercel.json                 ← Config: outputDirectory → outputs/kamba-hopo-lp
└── .aios-core/                 ← Framework AIOS
```

### 2.4 Architecture Diagram

```mermaid
graph TB
    subgraph User["Visitante"]
        Mobile[Mobile Browser]
        Desktop[Desktop Browser]
    end

    subgraph Vercel["Vercel Edge Network"]
        CDN[CDN Global]
        Analytics[Vercel Analytics]
    end

    subgraph Static["Static Assets"]
        HTML[index.html<br/>HTML + CSS + JS inline]
        Favicon[favicon.svg]
        OG[og-image.png]
        Sitemap[sitemap.xml]
        Robots[robots.txt]
    end

    subgraph External["External"]
        Fonts[Google Fonts CDN<br/>Playfair Display + Inter + JetBrains Mono]
        WhatsApp[WhatsApp API<br/>wa.me/595987463353]
        Instagram[Instagram<br/>@kambahopo]
    end

    Mobile --> CDN
    Desktop --> CDN
    CDN --> HTML
    CDN --> Favicon
    CDN --> OG
    CDN --> Sitemap
    CDN --> Robots
    CDN --> Analytics
    HTML --> Fonts
    HTML --> WhatsApp
    HTML --> Instagram
```

### 2.5 Architectural Patterns

- **Static Site Architecture:** Single HTML file servido por CDN — zero server-side processing. _Rationale:_ Máxima performance, mínima complejidad, hosting gratis.
- **Progressive Enhancement:** Contenido accesible sin JS; animaciones y interacciones como mejora. _Rationale:_ Funciona en cualquier device, incluso con JS deshabilitado.
- **CSS Custom Properties:** Design tokens en `:root` para paleta, tipografía y motion. _Rationale:_ Cambios de branding centralizados en un solo lugar.
- **Vanilla JS Modules:** Scripts organizados en IIFEs autocontenidas por feature. _Rationale:_ Sin build step, sin dependencies, fácil de mantener.
- **Mobile-First Responsive:** Breakpoints en 480px y 960px con `@media` queries. _Rationale:_ Público objetivo en Paraguay con alto uso móvil.

---

## 3. Tech Stack

| Category | Technology | Version | Purpose | Rationale |
|----------|-----------|---------|---------|-----------|
| Language | HTML5 + CSS3 + ES6+ | Current | Markup, estilos, interacciones | Sin transpilación, soporte nativo |
| Tipografía títulos | Playfair Display | Latest | Headings serif elegante | Sofisticación, itálica para énfasis |
| Tipografía cuerpo | Inter | Latest | Body text sans-serif | Legibilidad excelente |
| Tipografía labels | JetBrains Mono | Latest | Labels monospace | Estética premium para etiquetas |
| CSS Architecture | Custom Properties | Native | Design tokens | Cambios centralizados |
| JS Architecture | Vanilla ES6+ (IIFEs) | Native | Animaciones | Zero dependencies |
| Scroll Animations | IntersectionObserver | Native | Reveal on scroll | Performante, nativo |
| Deploy | Vercel | Free Tier | Hosting + CDN | Ya configurado, edge global |
| Source Control | Git + GitHub | Latest | Versionado | `jaco2015/p18-sitio-kamba-hopo` |
| SEO | Schema.org JSON-LD | Latest | Structured data | Restaurant + TouristAttraction |
| Analytics | Vercel Analytics | Free Tier | Tracking | Sin impacto en performance |
| Image Format | WebP | N/A | Fotos (Epic 2) | Compresión superior |

### Tecnologías explícitamente excluidas

| Tecnología | Razón de exclusión |
|-----------|-------------------|
| React / Vue / Svelte | Over-engineering para single page estática |
| Tailwind / Bootstrap | CSS custom ya implementado |
| Node.js / Express | No hay backend |
| Base de datos | No hay data dinámica |
| npm / build tools | Sin dependencies |
| TypeScript | No justificado para ~80 líneas JS |
| SASS / LESS | CSS custom properties cubren la necesidad |

---

## 4. CSS Architecture

### 4.1 Design Tokens

```css
:root {
  /* BACKGROUNDS */
  --bg-deep:      #040A07;
  --bg-base:      #081209;
  --bg-surface:   #0E1A0F;
  --bg-elevated:  #162218;

  /* ACCENT (Forest Green) */
  --accent:       #4A7C59;
  --accent-soft:  #3D6B4A;
  --accent-light: #6B9E7A;
  --accent-glow:    rgba(74, 124, 89, 0.08);
  --accent-glow-md: rgba(74, 124, 89, 0.12);
  --accent-glow-hi: rgba(74, 124, 89, 0.25);

  /* TEXT */
  --cream:      #E8DCC8;
  --cream-soft: #D4C8B0;
  --text-0:     #F2EDE4;
  --text-1:     #C4BBA8;
  --text-2:     #8A8270;
  --text-3:     #5A5448;

  /* BORDERS */
  --border:       rgba(74, 124, 89, 0.08);
  --border-hover: rgba(74, 124, 89, 0.18);

  /* TYPOGRAPHY */
  --heading-font: 'Playfair Display', 'Georgia', serif;
  --body-font:    'Inter', system-ui, sans-serif;
  --label-font:   'JetBrains Mono', monospace;

  /* MOTION */
  --ease:     cubic-bezier(0.16, 1, 0.3, 1);
  --ease-out: cubic-bezier(0.33, 1, 0.68, 1);
}
```

### 4.2 CSS Component Map

| Sección CSS | Líneas aprox. | Responsabilidad |
|------------|---------------|-----------------|
| Custom Cursor | 75-98 | Cursor circle + dot (desktop only) |
| Scroll Progress | 100-106 | Barra de progreso top |
| Backgrounds | 108-147 | Grain, mesh, grid, leaves (4 capas) |
| Layout | 149-151 | Content z-index, container max-width |
| Nav | 153-196 | Sticky nav, brand, links |
| Hero | 198-284 | Full viewport, animations |
| Buttons | 286-314 | Primary (green), Ghost (outline) |
| Proof Bar | 316-335 | Estadísticas |
| Sections | 337-356 | Padding, eyebrow, title |
| Bento Grid | 358-415 | Cards 2-col, featured, hover |
| Quote | 417-441 | Cita centrada |
| Stack List | 443-465 | Items 2-col con dot |
| CTA Section | 467-490 | Reservas |
| Footer | 492-505 | Links |
| Utilities | 507-520 | Dividers, reveal classes |
| Responsive | 522-545 | 960px, 480px, hover:none |

### 4.3 Responsive Breakpoints

- **Desktop (960px+):** Bento 2-col, stack 2-col, custom cursor, nav links visible
- **Tablet (481-960px):** Bento 1-col, stack 1-col, sin cursor custom, nav links visible
- **Mobile (<480px):** Full width stacked, nav links hidden (sin hamburger — Story 1.2), CTAs stacked, footer stacked

### 4.4 Contraste WCAG

| Token | Color | Sobre #040A07 | Ratio | WCAG AA |
|-------|-------|---------------|-------|---------|
| --cream | #E8DCC8 | Títulos | ~15:1 | PASS |
| --text-0 | #F2EDE4 | Body | ~17:1 | PASS |
| --text-1 | #C4BBA8 | Secundario | ~11:1 | PASS |
| --text-2 | #8A8270 | Muted | ~5.5:1 | PASS (borderline) |
| --text-3 | #5A5448 | Labels | ~3:1 | FAIL (decorativo) |
| --accent-light | #6B9E7A | Énfasis | ~7:1 | PASS |

`--text-3` falla WCAG AA pero se usa solo para labels decorativos (eyebrows, proof labels).

---

## 5. JS Architecture

### 5.1 Module Map

| # | Module | Líneas | Responsabilidad | Desktop | Mobile |
|---|--------|--------|-----------------|---------|--------|
| 1 | Custom Cursor | 807-828 | Cursor circle + dot, hover state | Yes | No |
| 2 | Scroll Progress | 830-838 | Barra verde top | Yes | Yes |
| 3 | Text Split | 840-853 | Split "Kamba Hopo" por letra | Yes | Yes |
| — | Hero Entrance | 855-864 | Activa animaciones hero on load | Yes | Yes |
| 4 | Scroll Reveal | 866-872 | `.visible` on scroll | Yes | Yes |
| 5 | Counter Animation | 874-895 | Números animados (792, 4, 100) | Yes | Yes |
| 6 | Magnetic Buttons | 897-908 | Botones siguen cursor | Yes | No |
| 7 | Background Mesh | 910-919 | Mesh parallax con mouse | Yes | No |
| 8 | Hamburger Menu | — | Story 1.2 (por crear) | No | Yes |
| 9 | Analytics | — | Story 1.6 (por crear) | Yes | Yes |

### 5.2 IIFE Pattern

```javascript
(() => {
  const element = document.getElementById('target');
  if (!element) return;  // Guard clause
  // Logic here
})();
```

Todos los módulos son independientes. No hay shared state ni comunicación inter-módulo.

### 5.3 Browser APIs utilizadas

| API | Módulo | Propósito |
|-----|--------|-----------|
| IntersectionObserver | Reveal, Counters | Viewport detection |
| requestAnimationFrame | Cursor, Counters | 60fps animations |
| mousemove | Cursor, Magnetic, Mesh | Mouse tracking |
| scroll (passive) | Progress | Scroll position |
| classList | Todos | CSS state toggle |

### 5.4 Dependency Graph

```
window.load ─── Hero Entrance ──┬── Text Split
                                ├── Reveal
                                └── Counters

mousemove ──────────────────────┬── Cursor
                                ├── Magnetic
                                └── Mesh BG

scroll ─── Scroll Progress

(todos independientes entre sí)
```

---

## 6. Deploy & Performance

### 6.1 Deployment Pipeline

```
Developer edits HTML → git push master → Vercel auto-deploy (~2s) → Edge CDN Global
```

### 6.2 Vercel Configuration

```json
{
  "outputDirectory": "outputs/kamba-hopo-lp"
}
```

### 6.3 Environments

| Environment | URL | Propósito |
|-------------|-----|-----------|
| Production | `p18-sitio-kamba-hopo.vercel.app` | Sitio live |
| Preview | Auto por PR | Preview de cambios |
| Local | `file:///...index.html` | Desarrollo |

### 6.4 Performance Budget

| Métrica | Target | Estimado | Notas |
|---------|--------|----------|-------|
| HTML size | < 100KB | ~45KB | Sin imágenes |
| FCP | < 1.5s | ~0.8s | CSS inline |
| LCP | < 2.5s | ~1.2s | Hero text |
| TBT | < 200ms | ~50ms | JS ligero |
| CLS | < 0.1 | ~0 | Sin contenido dinámico |
| Lighthouse | > 90 | ~95-99 | Sin imágenes |

**Post-Epic 2 (con imágenes):** Target Lighthouse > 85. Mitigación: WebP < 200KB, `loading="lazy"`.

### 6.5 SEO Technical Spec (Story 1.3-1.5)

```html
<!-- Favicon -->
<link rel="icon" type="image/svg+xml" href="/favicon.svg">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
<meta name="theme-color" content="#040A07">

<!-- Canonical -->
<link rel="canonical" href="https://p18-sitio-kamba-hopo.vercel.app/">

<!-- Open Graph -->
<meta property="og:type" content="website">
<meta property="og:title" content="Kamba Hopo — Bar, Café & Bistro | Vallemi, Paraguay">
<meta property="og:description" content="Donde se cruzan sabores y emociones. Gastronomía, café, karaoke y turismo en cavernas.">
<meta property="og:image" content="https://p18-sitio-kamba-hopo.vercel.app/og-image.png">
<meta property="og:url" content="https://p18-sitio-kamba-hopo.vercel.app/">
<meta property="og:locale" content="es_PY">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Kamba Hopo — Bar, Café & Bistro">
<meta name="twitter:description" content="Donde se cruzan sabores y emociones. Vallemi, Paraguay.">
<meta name="twitter:image" content="https://p18-sitio-kamba-hopo.vercel.app/og-image.png">

<!-- Schema.org -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Restaurant",
  "name": "Kamba Hopo",
  "description": "Bar, Café & Bistro en Vallemi, Paraguay",
  "url": "https://p18-sitio-kamba-hopo.vercel.app",
  "telephone": "+595987463353",
  "servesCuisine": ["Paraguaya", "Bistro", "Café"],
  "priceRange": "$$",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Vallemi",
    "addressCountry": "PY"
  }
}
</script>
```

---

## 7. Coding Standards & Implementation Guide

### 7.1 Critical Rules

- **Single File Rule:** Todo en `index.html`. No separar CSS/JS salvo que supere 2000 líneas.
- **Token First:** Nunca colores hardcodeados — siempre `var(--token)`.
- **IIFE Pattern:** Todo JS nuevo como IIFE con guard clause.
- **Comment Sections:** Usar formato `/* ═══ NAME ═══ */`.
- **No Dependencies:** Prohibido `<script src="">` o `<link>` externos (excepto Google Fonts).
- **Semantic HTML:** Tags semánticos (`<section>`, `<nav>`, `<footer>`).
- **Acentos obligatorios:** Ortografía correcta en español.
- **Responsive obligatorio:** Funcionar en 480px, 960px y desktop.

### 7.2 Naming Conventions

| Element | Convention | Ejemplo |
|---------|-----------|---------|
| CSS classes | kebab-case | `.bento-card` |
| CSS variables | kebab-case semántico | `--bg-deep` |
| CSS sections | `/* ═══ UPPER ═══ */` | `/* ═══ NAV ═══ */` |
| JS variables | camelCase | `const scrollProgress` |
| HTML IDs | camelCase | `id="heroLabel"` |
| CSS state classes | `.visible`, `.hover`, `.active` | `classList.add('visible')` |
| Data attributes | kebab-case | `data-target` |
| Asset files | kebab-case | `og-image.png` |

### 7.3 CSS Insertion Order

```
1. Custom Cursor    │
2. Scroll Progress  │  Existing
3. Backgrounds      │
4. Layout           │
5. Nav              ← Story 1.2: hamburger styles
6. Hero             │
7. Buttons          │
8. Proof Bar        │
9. Sections         │
10. Bento Grid      │
11. Quote           │
12. Stack List      │
13. CTA Section     │
14. Footer          │
15. Utilities       │
16. Responsive      ← Story 1.2: hamburger breakpoints
```

### 7.4 JS Insertion Order

```
1. Custom Cursor       │
2. Scroll Progress     │  Existing
3. Text Split          │
   Hero Entrance       │
4. Scroll Reveal       │
5. Counter Animation   │
6. Magnetic Buttons    │
7. Background Mesh     │
8. Hamburger Menu      ← Story 1.2
9. Analytics Tracking  ← Story 1.6
```

### 7.5 Implementation Guide por Story

| Story | Modifica | Crea | Complejidad |
|-------|----------|------|-------------|
| 1.1 Acentos | `index.html` (texto) | — | Trivial |
| 1.2 Hamburger | `index.html` (CSS+JS+HTML) | — | Media |
| 1.3 Favicon | `index.html` (`<head>`) | `favicon.svg`, `apple-touch-icon.png` | Baja |
| 1.4 Open Graph | `index.html` (`<head>`) | `og-image.png` | Baja |
| 1.5 Schema/SEO | `index.html` (`<head>`) | `sitemap.xml`, `robots.txt` | Baja |
| 1.6 Analytics | `index.html` (JS) | — | Baja |

### 7.6 Story 1.2 Spec — Hamburger Menu

**HTML** (dentro de `<nav>`, después de `.nav-brand`):
```html
<button class="nav-hamburger" id="navHamburger"
        aria-label="Abrir menú" aria-expanded="false">
  <span></span><span></span><span></span>
</button>
<div class="nav-mobile-menu" id="navMobileMenu"
     role="dialog" aria-label="Menú de navegación">
  <a href="#experiencias">Experiencias</a>
  <a href="#carta">Carta</a>
  <a href="#turismo">Turismo</a>
  <a href="#cta">Reservar</a>
</div>
```

**CSS:** Hidden en desktop, visible < 480px. 3 spans animadas a X. Menu fullscreen overlay con `var(--bg-deep)` opacity 0.95. Links centrados, tipografía grande. Transición 0.4s `var(--ease)`.

**JS (módulo 8):** Toggle `.active`. `aria-expanded` toggle. Cerrar al click link (smooth scroll). Cerrar al click fuera. Cerrar con Escape. Prevenir body scroll cuando abierto.

### 7.7 Error Prevention

- **WhatsApp:** Siempre `wa.me/595987463353` — nunca modificar
- **Fonts:** No remover pesos/estilos sin verificar uso
- **Backgrounds:** 4 layers (grain, leaves, mesh, grid) son intencionales — no eliminar
- **Cursor:** `cursor: none` en desktop es intencional (custom cursor)
- **IDs:** No duplicar IDs existentes — verificar antes de agregar

---

## 8. Testing Strategy

### 8.1 Manual Testing Checklist (por story)

**Después de cada story, verificar:**

- [ ] Desktop Chrome (1440px): layout, animaciones, cursor custom
- [ ] Desktop Firefox: layout, compatibilidad
- [ ] Mobile Chrome (360px): responsive, touch, no cursor
- [ ] Mobile Safari (iPhone): responsive, touch, smooth scroll
- [ ] Tablet (768px): layout intermedio
- [ ] WhatsApp link abre correctamente
- [ ] Instagram link abre correctamente
- [ ] Sin errores en Console del browser
- [ ] Scroll suave funciona en todos los nav links

### 8.2 Lighthouse Audit (al cierre de Epic 1)

- [ ] Performance > 90
- [ ] Accessibility > 85
- [ ] Best Practices > 90
- [ ] SEO > 90

### 8.3 Social Sharing Test (Story 1.4)

- [ ] WhatsApp preview muestra título + imagen + descripción
- [ ] Facebook Sharing Debugger valida sin errores
- [ ] Twitter Card Validator muestra summary_large_image

---

## 9. Next Steps

1. **@dev** → Ejecutar Epic 1, stories 1.1-1.6 en orden
2. **@devops** → Deploy a producción después de cada story completada
3. **@qa** → QA gate al cierre del Epic 1 (Lighthouse + manual testing)
4. **Cliente** → Proveer fotos y carta real para Epic 2
