# Kamba Hopo — Product Requirements Document (PRD)

## 1. Problem Definition, Goals and Context

### 1.0 Problem Statement

Kamba Hopo es un negocio multifuncional (bar, café, bistro, karaoke, turismo) en Vallemi, Paraguay, que actualmente no tiene presencia digital profesional. Su único canal es Instagram (792+ seguidores) y WhatsApp. Sin un sitio web, pierde visibilidad ante turistas que buscan opciones en Google, no puede mostrar su carta ni atracciones turísticas de forma organizada, y depende exclusivamente del boca a boca y redes sociales para generar reservas. Ya existe un prototipo HTML deployado en Vercel, pero tiene gaps técnicos (sin navegación mobile, sin SEO, sin acentos) que impiden usarlo como sitio oficial.

### 1.1 Goals

- Tener presencia digital profesional para Kamba Hopo en Vallemi, Paraguay
- Comunicar las 4 experiencias del lugar: Restaurante & Bistro, Café con Estilo (Marley Coffee Paraguay), Karaoke y Turismo/Aventura
- Generar reservas y consultas por WhatsApp (+595 987 463 353)
- Posicionar a Kamba Hopo como destino gastronómico y de aventura en Vallemi
- Mostrar la carta de forma atractiva (platos, cafetería, bebidas)
- Promover el turismo local: Caverna Kamba Hopo, Río Paraguay, Cerro Vallemi, historia afro-paraguaya

### 1.2 Background Context

Kamba Hopo es un bar, café y bistro ubicado en Vallemi, Paraguay. Combina gastronomía paraguaya tradicional, café de especialidad en alianza con @marleycoffee.paraguay, karaoke y turismo de aventura. Su nombre proviene de la caverna Kamba Hopo, formación geológica histórica vinculada a la historia afro-paraguaya de la zona.

El negocio tiene presencia activa en Instagram (792+ seguidores, 36 publicaciones) y opera reservas vía WhatsApp. Ya existe un sitio estático generado y deployado en Vercel, que necesita ser llevado a producción final con contenido verificado.

### 1.3 Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2026-02-28 | 1.0 | Versión inicial basada en PDF, HTML existente y perfil IG | Morgan |
| 2026-02-28 | 1.1 | Agregado problem statement, scope boundaries, KPIs | Morgan |

### 1.4 Success KPIs

| KPI | Baseline | Target | Timeframe |
|-----|----------|--------|-----------|
| Visitas mensuales al sitio | 0 | 500+ | 3 meses post-launch |
| Clicks en botón WhatsApp / mes | 0 | 50+ | 3 meses post-launch |
| Lighthouse Performance score | N/A | > 90 | Al cierre Epic 1 |
| Lighthouse SEO score | N/A | > 90 | Al cierre Epic 1 |

### 1.5 Scope Boundaries

**IN Scope (MVP — Epic 1):**
- Corrección de contenido existente (acentos, ortografía)
- Hamburger menu mobile
- Favicon y branding en browser
- Open Graph / meta tags para compartir en redes
- Schema.org y SEO técnico básico
- Analytics básico

**IN Scope (Epic 2):**
- Fotografías reales del local, comida y turismo
- Carta con items y precios reales
- OG Image real

**OUT of Scope:**
- Dominio custom (gestión administrativa, no desarrollo)
- Sistema de reservas online (se mantiene WhatsApp)
- E-commerce / pagos online
- Multi-idioma (guaraní, inglés)
- Blog o sección de noticias
- App mobile nativa
- CMS o panel de administración
- Integración con Google Maps embed
- Sistema de reviews/testimonios
- Menú interactivo con filtros/búsqueda

**Future Enhancements (post-MVP):**
- Galería de fotos con lightbox
- Google Maps embed con ubicación
- Integración con Google Business Profile
- Sección de eventos/agenda de karaoke
- Testimonios de clientes
- Multi-idioma (guaraní para público local)

---

## 2. Requirements

### 2.1 Functional Requirements

- **FR1:** El sitio debe ser una single-page con hero section que incluya logo (KH), tagline "Donde se cruzan sabores y emociones", subtítulo descriptivo y label "Bar · Café · Bistro · Karaoke · Turismo"
- **FR2:** CTA principal "Reservar por WhatsApp" debe abrir `wa.me/595987463353` en nueva pestaña
- **FR3:** Botón secundario "Explorar" debe hacer scroll suave a sección experiencias
- **FR4:** Barra de prueba social con: 792+ Seguidores, 4 Experiencias Únicas, 100% Sabor Paraguayo, Marley Coffee Partner — con animación de contador
- **FR5:** Sección Experiencias con cards bento: Restaurante & Bistro (featured, span 2 rows), Café con Estilo (@marleycoffee.paraguay), Karaoke — cada una con tags descriptivos
- **FR6:** Sección Carta con cards bento: Platos Principales (featured), Cafetería (Marley Coffee, repostería artesanal), Bebidas (cócteles, cervezas, tereré)
- **FR7:** Sección Turismo "Aventura en Vallemi" con lista: Caverna Kamba Hopo (tours guiados, 3.5km del puerto), Río Paraguay (paseos en lancha), Cerro Vallemi (trekking/miradores), Turismo Histórico (historia afro-paraguaya)
- **FR8:** Sección CTA final "Reserva tu experiencia" con botón WhatsApp y texto que menciona: mesa, karaoke, tours en cavernas
- **FR9:** Navegación sticky con links: Experiencias, Carta, Turismo, Reservar
- **FR10:** Footer con copyright, link a Instagram (@kambahopo) y WhatsApp
- **FR11:** Cita/quote decorativa "Donde se cruzan sabores y emociones" entre secciones Experiencias y Carta
- **FR12:** Navegación mobile (< 480px) con hamburger menu funcional

### 2.2 Non-Functional Requirements

- **NFR1:** Carga < 3 segundos en conexión móvil 3G (Paraguay)
- **NFR2:** 100% responsive: mobile-first (320px+), tablet (768px+), desktop (960px+)
- **NFR3:** HTML/CSS/JS estático puro — sin framework, sin backend, sin build step
- **NFR4:** Paleta Forest Green: `--accent: #4A7C59`, `--bg-deep: #040A07`, `--cream: #E8DCC8`
- **NFR5:** Tipografías: Playfair Display (títulos), Inter (cuerpo), JetBrains Mono (labels)
- **NFR6:** Animaciones: scroll reveal con blur, contadores animados, cursor custom (desktop), botones magnéticos, barra de progreso de scroll
- **NFR7:** Grain texture, mesh gradient y leaf pattern como capas de fondo decorativas
- **NFR8:** Contenido principal visible sin JavaScript (progressive enhancement)
- **NFR9:** Deploy en Vercel como sitio estático desde `outputs/kamba-hopo-lp/`
- **NFR10:** Idioma: español paraguayo (`lang="es-PY"`)

---

## 3. User Interface Design Goals

### 3.1 Overall UX Vision

Experiencia inmersiva dark-premium que evoca la atmósfera nocturna y natural de Kamba Hopo. El usuario entra en un "mundo visual" con texturas de grano de película, gradientes orgánicos y animaciones sutiles que transmiten sofisticación y calidez paraguaya. El flujo guía naturalmente desde la curiosidad (hero) → descubrimiento (experiencias/carta) → acción (reserva WhatsApp).

### 3.2 Key Interaction Paradigms

- **Scroll storytelling:** Secciones se revelan con fade + blur al hacer scroll (IntersectionObserver)
- **Cursor custom:** Círculo animado que reacciona al hover sobre elementos interactivos (solo desktop)
- **Botones magnéticos:** Siguen sutilmente el cursor para sensación premium
- **Contadores animados:** Números crecen al entrar en viewport (proof bar)
- **Barra de progreso:** Línea verde en top que indica posición de scroll
- **Text split animation:** Nombre "Kamba Hopo" aparece letra por letra en hero
- **Mesh parallax:** Fondo sigue ligeramente el movimiento del mouse

### 3.3 Core Screens and Views

Single page con 6 secciones verticales:

1. **Hero** — Impacto visual, tagline, CTAs
2. **Proof Bar** — Métricas de confianza (792+, 4, 100%, Marley)
3. **Experiencias** — Bento grid con las 4 propuestas de valor
4. **Carta** — Bento grid con platos, café, bebidas
5. **Turismo** — Stack list con 4 atracciones de Vallemi
6. **CTA / Reservas** — Cierre con WhatsApp prominente

### 3.4 Accessibility

WCAG AA parcial:

- Contraste de texto verificado sobre fondos oscuros (cream #E8DCC8 sobre #040A07 = ratio ~15:1)
- Texto secundario (--text-2: #8A8270 sobre #040A07) requiere revisión de contraste
- Cursor custom deshabilitado en touch devices y mobile
- Contenido accesible sin JS (estructura HTML semántica)

### 3.5 Branding

- **Logo:** Círculo con iniciales "KH" en verde sobre fondo oscuro
- **Paleta principal:** Forest Green noir — negro profundo (#040A07) con acentos verde bosque (#4A7C59) y cream cálido (#E8DCC8)
- **Tipografía títulos:** Playfair Display (serif elegante, itálica para énfasis)
- **Tipografía cuerpo:** Inter (sans-serif clean)
- **Tipografía labels:** JetBrains Mono (monospace técnico, caps, letter-spacing amplio)
- **Efectos visuales:** Grain texture, mesh gradients verdes sutiles, leaf pattern tropical, grid sutil
- **Alianza visual:** Marley Coffee Paraguay mencionado en tags y descripciones

### 3.6 Target Device and Platforms

Web Responsive con 3 breakpoints:

- **Mobile** (< 480px): Nav oculta, layout single column, sin cursor custom, CTAs apilados
- **Tablet** (< 960px): Grid adaptado, sin cursor custom
- **Desktop** (960px+): Experiencia completa con cursor custom, grids 2 columnas, efectos hover

---

## 4. Technical Assumptions

### 4.1 Repository Structure

Monorepo simple — un solo repositorio con outputs estáticos:

```
p18-sitio-kamba-hopo/
├── outputs/kamba-hopo-lp/index.html    ← Producción (single file)
├── outputs/premium-design/             ← Variantes alternativas
├── vercel.json                         ← Config deploy
└── .aios-core/                         ← Framework AIOS
```

### 4.2 Service Architecture

Sitio estático puro — zero dependencies:

- Single HTML file con CSS y JS inline (~920 líneas)
- Sin build step, sin bundler, sin npm packages
- Sin backend, sin API, sin base de datos
- Google Fonts como único recurso externo (Playfair Display, Inter, JetBrains Mono)
- WhatsApp como canal de contacto (wa.me link directo, sin formularios)

### 4.3 Testing Requirements

- **Visual:** Verificación manual en Chrome, Safari, Firefox — mobile y desktop
- **Performance:** Lighthouse score > 90 en todas las categorías
- **Links:** Verificar que WhatsApp abre correctamente (`wa.me/595987463353`)
- **Responsive:** Testear en 320px, 480px, 768px, 960px, 1440px
- **Animaciones:** Verificar scroll reveal, contadores, cursor custom en desktop
- Sin tests automatizados — scope no lo justifica para HTML estático

### 4.4 Additional Technical Assumptions

- **Deploy:** Vercel (configurado, `vercel.json` → `outputs/kamba-hopo-lp`)
- **Source control:** GitHub (`jaco2015/p18-sitio-kamba-hopo`, rama `master`)
- **Hosting:** Vercel free tier (suficiente para este volumen de tráfico)
- **Dominio:** Actualmente `p18-sitio-kamba-hopo.vercel.app` — pendiente dominio custom
- **CDN:** Vercel Edge Network incluido
- **Imágenes:** Ninguna actualmente — sitio es 100% texto/CSS. Futuras fotos deben ser WebP < 200KB
- **SEO:** Actualmente solo tiene `<title>` y `<meta description>`. Falta Open Graph, schema.org, favicon, sitemap
- **Analytics:** No implementado
- **Idioma:** Español paraguayo (`es-PY`), contenido sin acentos en el HTML actual
- **Performance actual:** Excelente — un solo archivo HTML sin imágenes ni dependencies externas (excepto fonts)

---

## 5. Epic List

### Epic 1: Sitio MVP Production-Ready

Corregir todos los gaps técnicos del HTML existente para que el sitio sea profesional y funcional: acentos/tildes, hamburger menu mobile, favicon, Open Graph meta tags, schema.org para restaurante, sitemap.xml y analytics. Resultado: sitio publicable y listo para compartir.

### Epic 2: Contenido Real y Optimización Visual

Integrar fotos reales del local, comida y atracciones turísticas. Actualizar carta con items y precios reales. Optimizar imágenes (WebP). Resultado: sitio que convierte visitantes en clientes porque muestra el producto real.

---

## 6. Epic Details

### Epic 1: Sitio MVP Production-Ready

**Objetivo:** Corregir todos los gaps técnicos del HTML existente para que el sitio sea profesional, accesible desde mobile y optimizado para SEO. Al finalizar, el sitio estará listo para ser compartido como presencia digital oficial de Kamba Hopo.

#### Story 1.1: Corrección de contenido — Acentos y tildes

*As a visitante hispanohablante, I want leer contenido con ortografía correcta, so that el sitio transmita profesionalismo y cuidado.*

**Acceptance Criteria:**

1. Todo el texto del HTML tiene acentos y tildes correctos ("corazón", "tradición", "música", "único", etc.)
2. El `lang="es-PY"` se mantiene
3. No se altera la estructura HTML ni los estilos
4. Verificado manualmente que no queda ningún texto sin acentuar

#### Story 1.2: Hamburger menu mobile

*As a visitante mobile, I want acceder a la navegación del sitio, so that pueda saltar a cualquier sección sin hacer scroll largo.*

**Acceptance Criteria:**

1. En viewport < 480px aparece un icono hamburger en el nav
2. Al tocar se despliega menú con: Experiencias, Carta, Turismo, Reservar
3. Al seleccionar una opción el menú se cierra y hace scroll suave a la sección
4. Animación de apertura/cierre suave, coherente con el estilo premium del sitio
5. Implementado en vanilla JS (sin librería)

#### Story 1.3: Favicon y meta tags básicos

*As a visitante, I want ver un favicon de Kamba Hopo en la pestaña del browser, so that identifique el sitio fácilmente entre mis pestañas.*

**Acceptance Criteria:**

1. Favicon SVG con las iniciales "KH" en verde sobre fondo oscuro (consistente con logo)
2. Fallback favicon.ico para browsers legacy
3. Apple touch icon (180x180) para iOS home screen
4. Meta tag `theme-color` configurado con `#040A07`

#### Story 1.4: Open Graph y meta tags para redes sociales

*As a dueño del negocio, I want que al compartir el link en WhatsApp o Instagram muestre preview atractivo, so that genere más clicks cuando comparta el sitio.*

**Acceptance Criteria:**

1. Open Graph tags: og:title, og:description, og:image, og:url, og:type
2. Twitter Card tags: twitter:card, twitter:title, twitter:description, twitter:image
3. og:image de al menos 1200x630px con branding Kamba Hopo (generado como SVG o placeholder hasta tener fotos reales)
4. Preview verificado en WhatsApp y Facebook sharing debugger

#### Story 1.5: Schema.org y SEO técnico

*As a dueño del negocio, I want que Kamba Hopo aparezca correctamente en Google, so that clientes potenciales me encuentren buscando "restaurante en Vallemi".*

**Acceptance Criteria:**

1. Schema.org JSON-LD tipo `Restaurant` con: name, address (Vallemi, Paraguay), telephone, url, servesCuisine, priceRange
2. Schema.org `TouristAttraction` para la Caverna Kamba Hopo
3. Sitemap.xml generado en raíz del sitio
4. robots.txt básico permitiendo indexación completa
5. Canonical URL definida

#### Story 1.6: Analytics y monitoreo

*As a dueño del negocio, I want saber cuántas personas visitan mi sitio, so that pueda medir el impacto de mi presencia digital.*

**Acceptance Criteria:**

1. Vercel Analytics activado (o Google Analytics 4 como alternativa)
2. Tracking de clicks en botón WhatsApp (evento custom)
3. No afecta performance (carga async)
4. Cumple con normativas de privacidad básicas

---

### Epic 2: Contenido Real y Optimización Visual

**Objetivo:** Reemplazar todo el contenido placeholder con assets reales del negocio. Al finalizar, el sitio mostrará fotos reales, precios actualizados y contenido verificado por el cliente, maximizando la conversión de visitantes a reservas.

#### Story 2.1: Fotografías reales del local y experiencias

*As a visitante, I want ver fotos reales de Kamba Hopo, so that tenga expectativas claras de lo que voy a encontrar.*

**Acceptance Criteria:**

1. Foto hero del local o ambiente (background o sección)
2. Al menos 1 foto por experiencia: restaurante, café, karaoke
3. Todas las imágenes en formato WebP, max 200KB cada una
4. Lazy loading implementado con `loading="lazy"`
5. Alt text descriptivo en cada imagen

#### Story 2.2: Fotografías de turismo y atracciones

*As a turista, I want ver fotos de las atracciones de Vallemi, so that me motive a planificar una visita.*

**Acceptance Criteria:**

1. Al menos 1 foto por atracción: Caverna Kamba Hopo, Río Paraguay, Cerro Vallemi
2. Imágenes WebP < 200KB con lazy loading
3. Sección turismo rediseñada para acomodar imágenes (cards en vez de stack list si aplica)

#### Story 2.3: Carta con items y precios reales

*As a visitante, I want ver la carta real con precios, so that pueda decidir si el lugar se ajusta a mi presupuesto.*

**Acceptance Criteria:**

1. Items de carta son los reales del negocio (provistos por el cliente)
2. Precios en guaraníes (₲) visibles
3. Subsecciones actualizadas: Platos Principales, Cafetería, Bebidas
4. Layout acomodado para mostrar items con precio (posible lista o grid)

#### Story 2.4: OG Image real y revisión final de contenido

*As a dueño del negocio, I want que el preview de redes sociales muestre una foto real de mi local, so that el link compartido sea atractivo y genuino.*

**Acceptance Criteria:**

1. og:image actualizada con foto real del local (1200x630px)
2. Revisión final de todos los textos con el cliente
3. Verificado que no queda contenido placeholder
4. Deploy final a producción

---

## 7. Checklist Results

**Executed:** 2026-02-28 | **Version:** 1.1 (post-fixes)

| Category | Status | Notes |
|----------|--------|-------|
| 1. Problem Definition & Context | **PASS** | Problem statement, goals, KPIs y scope boundaries agregados |
| 2. MVP Scope Definition | **PASS** | IN/OUT scope explícito, future enhancements documentados |
| 3. User Experience Requirements | **PASS** | Paradigmas de interacción detallados, accessibility documentada |
| 4. Functional Requirements | **PASS** | 12 FR + 10 NFR testeables y detallados |
| 5. Non-Functional Requirements | **PASS** | Performance, responsive, stack definidos (security N/A para static) |
| 6. Epic & Story Structure | **PASS** | 2 epics, 10 stories, ACs claros, secuencia lógica |
| 7. Technical Guidance | **PASS** | Stack 100% definido, zero ambiguity |
| 8. Cross-Functional Requirements | **PARTIAL** | Data/integrations N/A para static site. WhatsApp documentado. |
| 9. Clarity & Communication | **PASS** | Lenguaje claro, versionado, bien estructurado |

**Overall:** 8/9 PASS — **READY FOR ARCHITECT**

---

## 8. Next Steps

### 8.1 UX Expert Prompt

> @ux-design-expert — Revisar el sitio deployado en `p18-sitio-kamba-hopo.vercel.app` y el HTML en `outputs/kamba-hopo-lp/index.html`. Validar la experiencia mobile (falta hamburger menu), contraste de colores WCAG AA (especialmente --text-2 sobre fondos oscuros), y proponer mejoras visuales para integrar fotografías reales en el Epic 2. Usar este PRD como referencia.

### 8.2 Architect Prompt

> @architect — Revisar el HTML estático en `outputs/kamba-hopo-lp/index.html` (~920 líneas, single file). Evaluar si la arquitectura single-file se mantiene viable para el Epic 2 (integración de imágenes) o si conviene separar en archivos CSS/JS. Definir estrategia de optimización de imágenes WebP y lazy loading. Usar este PRD como referencia.
