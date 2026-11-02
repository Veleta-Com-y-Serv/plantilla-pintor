# Pintor y decorador: brief de diseño

Plantilla `pintor` creada el 02/11/2026 a partir de `limpieza-hogar` con `php artisan plantillas:nueva` y
rediseñada entera (fila 1 de la tanda 4, «autónomos»). De la base solo queda la estructura técnica (site.ts,
seo.ts, Base.astro, Imagen.astro, formulario `mailto`). Este fichero se queda en el repo: es lo que lee quien
(persona o agente) la rediseñe después.

## Brief

- **Para quién**: pintores y decoradores autónomos o con un equipo muy pequeño: pintura de pisos, quitar gotelé,
  fachadas, comunidades, papel pintado, lacado de puertas, locales y pintura industrial (`sectores` de
  template.yaml). Quien entra quiere ver trabajos hechos, saber si va a su pueblo, cuánto cuesta más o menos y
  llamar o escribir por WhatsApp.
- **Voz**: primera persona del singular («Soy Marcos, pintor en Zamora desde 2009»). Nada de «nuestra empresa».
- **Qué tiene que conseguir la web**: que llamen o escriban por WhatsApp (barra fija inferior en móvil, botón en
  la cabecera, teléfono a la vista en la portada, en presupuesto y en contacto) o que pidan presupuesto con un
  formulario corto (nombre, teléfono, qué trabajo, pueblo y qué necesita; solo texto).
- **Tono y estilo** (`fresco`): limpio y recién pintado. Sí: la carta de colores de la tienda de pinturas,
  blanco con un azul limpio y el amarillo del rodillo, esquinas rectas. No: brochazos dibujados, salpicaduras,
  esquinas redondas ni la caja centrada estrecha con tarjetas blancas.
- **Paleta de ejemplo**: primario `#1f5fd6` (azul limpio; lleva texto blanco), acento `#ffcc1a` (amarillo rodillo;
  lleva texto oscuro), fondo `#ffffff`, texto `#13213a` (azul noche). Derivados con `color-mix` en `global.css`:
  `--claro` (primario al 7 % sobre el fondo), `--claro-fuerte` (16 %), `--noche`, `--sobre-acento`, `--linea` y
  la carta `--m1…--m6` (primario, primario al 50 % y al 20 %, acento, acento al 45 %, noche). Si el cliente cambia
  los cuatro colores, la carta y las bandas siguen funcionando.
- **Tipografía**: titulares en sans muy pesada de sistema (`Arial Black`, `Segoe UI Black`…, 900) con interletrado
  negativo, enormes (portada hasta 5,6 rem; secciones hasta 4,2 rem); el final del titular de la portada
  (`titulo_destacado`) y los números de los servicios, en serif cursiva (Georgia). Texto en Segoe UI / system-ui.
  Antetítulos en mayúsculas espaciadas con una muestra de color cuadrada delante.
- **Firma visual**:
  1. **Carta de colores**: las promesas de la portada en muestras cuadradas de borde a borde, numeradas («Nº 01»),
     en seis tonos sacados de los colores del cliente; el mismo motivo hace de filo de la cabecera y del pie.
  2. **Pasada de rodillo**: cada foto a sangre lleva un filo amarillo (vertical entre foto y texto en la portada;
     abajo en las bandas partidas; azul sobre la banda amarilla).
  3. Esquinas rectas en todo: botones con un filo inferior más oscuro, iconos en cuadrado, signo «+» en muestra.
  4. Mosaico de trabajos de borde a borde sin márgenes, con el primero a doble tamaño y filtros por categoría.
- **Ritmo de bandas** (todas a todo el ancho): portada partida (foto a sangre a la izquierda, texto en blanco) →
  carta de colores → servicios azul → quién soy azul claro con foto a sangre a la derecha → trabajos blanco con
  mosaico a sangre → cómo trabajo amarillo con foto a la izquierda → marcas noche → zonas blanco con foto a la
  derecha → opiniones azul claro → preguntas blanco → presupuesto partido (azul / azul claro) → contacto blanco
  con el teléfono enorme → pie noche con filo de muestras. En móvil, barra fija «Llamar / WhatsApp».
- **Apartados** (en orden): `hero` (items = promesas), `servicios` (items: titulo, texto, icono, precio «desde»
  opcional), `sobre` (`tipo: texto`, con imagen e items), `trabajos` (`trabajos`: titulo, texto, lugar, imagen,
  categoria «Interior|Exterior|Comunidad|Local»), `proceso` (items, imagen), `marcas` (items: titulo, texto),
  `zonas` (items: titulo, texto = comarca; imagen), `opiniones` (`testimonios` con `servicio`), `preguntas`,
  `presupuesto` (items, `boton_formulario`, `nota`), `contacto`. `texto` para apartados nuevos.
- **Fotos** (`fotos.json`, 11): pared recién pintada con rodillo (portada, 1:1); herramientas (quién soy, 3:4);
  siete trabajos 4:3 (salón, fachada de pueblo, escalera, dormitorio infantil, cafetería, puertas lacadas,
  garaje); habitación protegida con plástico y cinta (cómo trabajo, 3:4); ciudad junto al río (zonas, 4:3). Sin
  texto legible, sin logotipos, sin personas reconocibles.
- **Responsive**: móvil primero; a 375 px una columna con 16 px de margen del texto, fotos de borde a borde, la
  carta en 2 columnas y barra fija abajo; a 768 px la portada y las bandas partidas pasan a 50/50; a 1100 px
  servicios a 3 columnas (4 a 1280), mosaico a 4 columnas con el primero doble, opiniones a 3 y contacto a 4.
- **Qué no hacer**: volver a la portada de la base (texto sobre azul cielo y foto con esquina redonda), poner
  burbujas o esquinas redondas, usar el amarillo como color de texto sobre blanco, meter precios o cifras fijos
  en los componentes o hablar en plural de empresa.
