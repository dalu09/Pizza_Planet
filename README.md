# Pizza Planet — Visual Analytics de exoplanetas

Explorador visual basado en los CSV descargados del [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/). La página carga los archivos locales, ubica los planetas en un mapa 3D a partir de sus coordenadas y distancia, permite buscar por planeta o sistema y filtrar por método de descubrimiento. Al seleccionar un punto se muestran sus parámetros y el número/tipo de soluciones asociadas.

## Datos incluidos

Los dos archivos son exportaciones de las tablas `pscomppars` y `ps` del archivo de NASA. Cada CSV incluye al inicio comentarios con la fecha de exportación y la descripción (`# COLUMN`) de sus campos; la fila de encabezados viene después de esos comentarios.

| Archivo | Filas de datos | Columnas | Qué contiene |
| --- | ---: | ---: | --- |
| `data/PSCompPars_2026.11.12_16.30.57.csv` (`PSCompPars`) | 6,470 | 84 | Parámetros predeterminados para planetas confirmados: una fila por planeta. Es la fuente principal del mapa y de las búsquedas. |
| `data/PS_2026.11.12_16.32.23.csv` (`PS`) | 40,414 | 92 | Distintas soluciones/publicaciones y registros de parámetros por planeta. `default_flag = 1` marca la solución predeterminada; las filas restantes no son planetas adicionales. |

En esta instantánea, `PSCompPars` contiene 6,470 nombres de planeta en 4,862 sistemas anfitriones. `PS` contiene 40,414 registros para esos mismos 6,470 nombres, incluyendo soluciones de distintos tipos y candidaturas. Por eso no se deben sumar las filas de ambas tablas como si fueran planetas. La aplicación relaciona sus registros mediante `pl_name`; usa `PSCompPars` para el catálogo visible y `PS` para enriquecer cada planeta con su tipo de solución y cantidad de registros relacionados.

## Cómo leer las columnas

Las descripciones completas y oficiales de cada columna están dentro de los comentarios de cada CSV. Los campos más relevantes para la aplicación y el análisis son:

| Campo | Significado |
| --- | --- |
| `pl_name`, `hostname` | Nombre del planeta y del sistema anfitrión; `pl_name` es la clave usada para relacionar las tablas. |
| `discoverymethod`, `disc_year`, `disc_facility` | Método, año e instalación de descubrimiento. |
| `pl_rade`, `pl_bmasse`, `pl_orbper` | Radio en radios terrestres, masa en masas terrestres y período orbital en días. Pueden estar vacíos si no hay una medición. |
| `pl_orbsmax`, `pl_orbeccen`, `pl_insol`, `pl_eqt` | Semieje mayor, excentricidad, insolación y temperatura de equilibrio. |
| `sy_snum`, `sy_pnum`, `st_spectype`, `st_teff`, `st_rad`, `st_mass` | Número de estrellas/planetas del sistema y propiedades de la estrella anfitriona. |
| `ra`, `dec`, `sy_dist` | Ascensión recta y declinación en grados, y distancia del sistema en parsecs. La vista convierte la distancia a años luz para representar posiciones 3D. |
| `sy_vmag`, `sy_kmag`, `sy_gaiamag` | Magnitudes aparentes en bandas V, K y Gaia. |

Varios parámetros tienen columnas complementarias con sufijos `err1`/`err2` (incertidumbres superior e inferior) y `lim` (indicador de límite). Un valor vacío significa que esa medición no está disponible; no equivale a cero. `PS` añade `default_flag`, `soltype`, las referencias `pl_refname`/`st_refname`/`sy_refname` y fechas de actualización/publicación/liberación (`rowupdate`, `pl_pubdate`, `releasedate`).

## Ejecutar

La página usa `fetch()` para leer archivos locales, por lo que debe servirse por HTTP (abrir `index.html` directamente como `file://` normalmente bloquea la carga de los CSV). Desde la raíz del proyecto:

```bash
python3 -m http.server 8000
```

Luego abre <http://localhost:8000>. Three.js, Tailwind y Font Awesome se cargan desde CDN, así que también se requiere conexión a internet para esas librerías.