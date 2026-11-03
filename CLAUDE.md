# Plantilla «Pintor y decorador» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **fresco**.
Una sola página para pintores y decoradores autónomos: pisos, gotelé, fachadas, comunidades, papel pintado, lacado,
locales y pintura industrial. Todo en castellano de España, en **primera persona del singular** («pinto», «voy a
verlo»), frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…); `src/styles/global.css` saca de ahí los derivados (`--claro`, `--claro-fuerte`, `--noche`, `--sobre-acento`, `--linea` y la carta de colores `--m1…--m6`) con `color-mix`. El primario lleva texto blanco encima: conviene un azul medio u oscuro. El acento (amarillo) lleva texto oscuro.
- **Tipografías y aspecto general**: `src/styles/global.css` (bandas `.banda--blanca|clara|azul|amarilla|noche`, carta de colores `.carta`/`.muestra`, bandas partidas `.partida` con la pasada amarilla, botones rectos `.btn`/`.btn-sec`, iconos `.cuadro-icono`, cabecera `.cabecera--pintor`, pie `.pie--pintor` y barra fija de móvil `.barra-movil`). Fuentes del sistema: no añadas fuentes externas.
- **Teléfono y WhatsApp**: `site.yaml → contacto.telefono` y `contacto.whatsapp`. Salen solos en la cabecera (botón de WhatsApp), la portada, el presupuesto, el contacto, el pie y la barra fija inferior del móvil «Llamar / WhatsApp» (`src/components/Footer.astro`). Si faltan, esos botones no salen.
- **Imágenes**: en `public/`. Las de relleno están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos nuevas del cliente van en `public/fotos/`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en una muestra de color + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas aguantan listas y campos vacíos.
- `hero` → `hero.astro`: portada partida 50/50 (foto a sangre a la izquierda con la pasada amarilla + titular en blanco). `titulo_destacado` = final del titular en serif cursiva. Debajo de los botones, el teléfono. `items` (solo `titulo`, hasta 6) = promesas de la carta de colores.
- `servicios` → `servicios.astro`: banda azul con rejilla sin tarjetas (`items`: titulo, texto, icono, precio opcional «desde 6 €/m²»). Iconos del oficio: `rodillo`, `brocha`, `pared`, `casa`, `edificio`, `empapelado`, `pistola`, `nave`, `cinta`, `cubo`, `escoba`.
- `sobre` (`tipo: texto`) → `texto.astro`: «Quién soy». Con `imagen`, banda partida con la foto a la derecha; el primer párrafo sale en serif cursiva. `items` (titulo, texto, icono) = seguro, garantía…
- `trabajos` → `trabajos.astro`: mosaico de fotos a sangre (`trabajos`: titulo, texto, lugar, imagen, categoria «Interior|Exterior|Comunidad|Local»). Con dos categorías o más salen filtros. Máximo 24.
- `proceso` → `proceso.astro`: banda amarilla partida, foto a la izquierda (`imagen`) y pasos numerados en línea vertical (`items`: titulo, texto, icono).
- `marcas` → `marcas.astro`: banda noche con las pinturas con las que trabajas (`items`: titulo, texto).
- `zonas` → `zonas.astro`: banda blanca con pueblos y comarcas (`items`: titulo, texto = comarca) y foto a la derecha (`imagen`).
- `opiniones` → `opiniones.astro`: columnas con comillas en muestra amarilla (`testimonios`: texto, autor, servicio). Sin opiniones no se pinta.
- `preguntas` → `preguntas.astro`: acordeón `details/summary` (`preguntas`: pregunta, respuesta) con botón de WhatsApp si hay número. Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: banda partida azul / azul claro con `items` (titulo, texto, icono), teléfono y WhatsApp grandes, `nota`, `boton_formulario` y el formulario corto (nombre, teléfono, qué trabajo —sale de los servicios—, pueblo y qué necesitas).
- `contacto` → `contacto.astro`: teléfono enorme y, debajo, WhatsApp, correo, dirección y horario de `site.yaml → contacto`. Si no hay presupuesto activo, añade el formulario de contacto.
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre como cadena (`"desde 6 €/m²"`, `"Consultar"`).
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para varios valores, una cadena con «;». Máximo 24 elementos por lista.
5. **Trabajo nuevo**: añade un elemento a `secciones.trabajos.trabajos` con `titulo`, `texto`, `lugar`, `imagen` y `categoria` (usa una de las que ya hay para que el filtro lo agrupe).
6. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
7. **Apartado nuevo**: un id propio en `secciones` con `tipo:` = el diseño de otra sección (`servicios`, `trabajos`, `marcas`…) o `texto`. `src/pages/index.astro` lo recoge solo; no lo toques.
8. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio —`seo.tipo: HousePainter`— y de las preguntas, robots, sitemap y llms.txt) y salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el del menú móvil y el de los filtros de trabajos), 16 px de margen lateral del texto en móvil (las fotos y fondos sí tocan el borde), botones de 44 px de alto como mínimo y sin scroll horizontal. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

Fotos de partida en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`, sin derechos de terceros); los SVG de `public/placeholders/` siguen de respaldo.

## Páginas propias (fichas por elemento y páginas por zona)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.servicios.items` → `/servicios/<slug>/` (servicio).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Zonas: cada elemento de `secciones.zonas.items` **con `texto`** (60-150 palabras: qué trabajos se hacen allí, pueblos cercanos)
  tiene su página en `/zonas/<slug>/`. En la sección: `titulo_pagina` («Reformas en {zona}») y `texto_pagina` (entrada, con {zona} y {negocio}).
- Una orden «añade una página para X» = escribir su `detalle` (o el `texto` de la zona) en site.yaml. Nunca crees a mano páginas en
  `src/pages/servicios/` ni en `src/pages/zonas/`: salen solas de `src/pages/[coleccion]/[slug].astro` y `src/pages/zonas/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay; zonas con `areaServed`).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
