# Pizza Planet — Dirección visual "Cyber Diner"

Fuente: estudio de marca en Figma Make ("Estudio de marca para exoplanetas", versión 2 "Redesign Pizza Planet with cyberpunk direction").
Úsalo como **referencia de estilo** (colores, tipografía, textura). La **estructura** de pantallas la manda `design/boceto.png` (wireframe de 5 pantallas).
Objetivo: que se parezca a esta dirección pero **mejor**: más coherente, más legible para visualización de datos, menos "póster" y más "instrumento".

## Concepto
Diner espacial retro + señalética cyberpunk. Estación de exploración interestelar: neón, paneles técnicos, retículas, scanlines, cortes angulares.
Principio: **base científica rigurosa + capa visual retro-cyber**. La información debe leerse clara; la personalidad vive en tipografía, color, marcos y detalles.

## Paleta
| Nombre | Hex | Rol |
|---|---|---|
| Night City | `#08080C` | Fondo principal (dominante) |
| Titanio | `#F4F1E8` | Texto principal sobre oscuro; fondos claros de secciones |
| Plasma magenta | `#FF2DAA` | Acento principal, CTA, estado activo/seleccionado |
| Cian terminal | `#28E7F5` | Datos, enlaces, filtros, órbitas, info |
| Ácido alien | `#D7FF2F` | Destacados puntuales: habitabilidad, etiquetas, CTA secundario |
| Ultravioleta | `#5021A8` | Profundidad, sombras desplazadas, bordes, gradientes |

Contraste medido (WCAG):
- Sobre Night City: titanio 17.7, ácido 17.4, cian 13.2, magenta 5.9, ultravioleta 2.0
- Sobre Titanio: ultravioleta 8.8, magenta 3.0, cian 1.3, ácido 1.0

Reglas:
- Fondo oscuro como base; los neones son **acentos**, nunca dos neones grandes compitiendo en la misma vista.
- Ultravioleta **solo decorativo** sobre oscuro (no texto).
- Sobre fondo claro, cian y ácido no sirven para texto; usar Night City o ultravioleta.
- En el grafo 3D y gráficos: codificar categorías (p. ej. método de descubrimiento) con cian / magenta / ácido / titanio y variantes atenuadas; no depender solo del color (forma o etiqueta también).

## Tipografía (Google Fonts)
- **Display / identidad: Orbitron** — logo, títulos de pantalla, cifras gigantes (año en la línea del tiempo). Itálica/inclinada con sombra desplazada en el hero.
- **Interfaz y texto: Space Grotesk** — Regular / Medium / Bold.
- **Datos técnicos: IBM Plex Mono** — distancias, radios, masas, coordenadas, fechas, etiquetas pequeñas en mayúsculas con tracking amplio (p. ej. `SISTEMA DE MARCA / CY-77`).

## Lenguaje gráfico
- Planetas y órbitas dibujados en neón (anillo ácido, planeta magenta, punto cian).
- Retícula fina de fondo, scanlines sutiles, ruido/interferencia leve.
- Paneles técnicos con borde fino, esquinas cortadas en ángulo, sombras sólidas desplazadas (ultravioleta o magenta).
- Bandas diagonales magenta y rótulos tipo ticker (`// PLANET // PIZZA //`).
- Botones sólidos rectangulares (ácido o magenta) con flecha ↗ y texto mono en mayúsculas.
- Microetiquetas técnicas: `UBICACIÓN: SECTOR PP-77`, `TRANSMISIÓN: EN VIVO`, códigos de barras decorativos.

## Qué mejorar respecto a la referencia
- Moderar los efectos (scanlines, glitch, sombras) en las vistas de datos: que no ensucien el grafo ni las tablas.
- Jerarquía clara en la ficha científica: valor grande en Plex Mono, unidad pequeña, etiqueta mono atenuada.
- Valores vacíos visibles como "sin dato", nunca como 0.
- Respetar `prefers-reduced-motion`.
- No usar el logo, cohete ni personajes de Toy Story: identidad propia.
