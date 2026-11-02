# Plantilla NoExpertise · Pintor y decorador

Web de una sola página para pintores y decoradores autónomos: pisos, quitar gotelé, fachadas, comunidades, papel
pintado, lacado de puertas, locales y pintura industrial. Habla en primera persona, con el teléfono y el WhatsApp
siempre a mano (barra fija en el móvil). Bandas a todo el ancho en blanco, azul limpio, amarillo rodillo, azul
claro y noche; carta de colores bajo la portada, mosaico de trabajos de borde a borde y fotos a sangre.

- Sectores: pintor, pintura, decorador, empapelado, lacado, pintura-industrial. Estilo: fresco. Plan mínimo: gratis.
- Secciones: hero, servicios, sobre (`tipo: texto`), trabajos, proceso, marcas, zonas, opiniones, preguntas, presupuesto, contacto (y `texto` para apartados nuevos).
- Ejemplo: «Pinturas Arribas», pintor autónomo ficticio de Zamora (teléfonos y marcas de pintura ficticios).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`HousePainter`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

## Campos propios

| Sección | Campo | Qué es |
|---|---|---|
| `hero` | `titulo_destacado` | Final del titular, en serif cursiva |
| `hero` | `items[].titulo` | Promesas de la carta de colores bajo la portada (hasta 6) |
| `servicios` | `items[].precio` | Precio orientativo opcional («desde 6 €/m²», «Consultar») |
| `sobre` | `items[]` | Seguro, garantía… (titulo, texto, icono) |
| `trabajos` | `trabajos[]` | titulo, texto, lugar, imagen, categoria («Interior», «Exterior», «Comunidad», «Local»: filtros) |
| `marcas` | `items[]` | Pinturas con las que trabajas (titulo = marca, texto = para qué) |
| `zonas` | `items[].texto` | Comarca del pueblo (opcional) |
| `opiniones` | `testimonios[].servicio` | Trabajo y lugar de quien opina |
| `presupuesto` | `boton_formulario`, `nota` | Texto del botón y nota bajo el teléfono |

El formulario de presupuesto es corto: nombre, teléfono, qué trabajo (de los servicios), pueblo o barrio y qué
necesitas; abre el correo del negocio (`mailto`). Con teléfono o WhatsApp en `contacto`, el móvil muestra una barra
fija inferior «Llamar / WhatsApp».

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.servicios.items` con `detalle` tiene su página en `/servicios/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Cada zona de `secciones.zonas.items` con `texto` tiene su página en `/zonas/<slug>/` (`src/pages/zonas/[slug].astro`); en la sección, `titulo_pagina` y `texto_pagina` con {zona} y {negocio}.
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
