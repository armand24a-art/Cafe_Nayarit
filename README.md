# APS-Café Nayarit - Sitio de divulgación científica

Página web para publicar en GitHub Pages el contenido de la investigación
sobre el **modelo de distribución potencial de café (MaxEnt)** y el
**Área Prioritaria de Producción Sostenible de Café (APS-Café)** en Nayarit, México.

## Publicaciones de referencia

| Documento | Enlace |
|---|---|
| Artículo (modelo): *Potential Coffee Distribution in a Central-Western Region of Mexico* (Ecologies, 2023) | https://doi.org/10.3390/ecologies4020018 |
| Capítulo de libro: *Área prioritaria de producción sostenible de café (APS-Café), en Nayarit* (2026) | https://doi.org/10.52501/cc.448.07 |
| Libro completo: *Café de Nayarit: sostenibilidad, biodiversidad y patrimonio socioeconómico* | https://comunicacion-cientifica.com/libros/cafe-de-nayarit/ |

## Contenido del sitio

- Encabezado con el "gancho" (problema y paradoja de la caficultura nayarita).
- Resumen ejecutivo de 5 líneas.
- Sección de relevancia del problema y contexto.
- Metodología visual (MaxEnt, AUC 0.98, TSS 0.96).
- Hallazgos clave con números traducidos a impacto.
- **Mapa interactivo Leaflet** con el área de estudio (archivo GeoJSON) y leyenda de idoneidad, con 3 mapas base (OpenStreetMap, Esri Imágenes, Esri Topográfico).
- Sección de limitaciones como oportunidades (prueba de fuego).
- Sección de aplicaciones y futuro.
- Botones con vista previa para los documentos publicados.
- Diseño adaptable (responsive) a PC, tablet y celular.

## Archivos

```
Site_Cafe/
├── index.html                     (página completa)
├── favicon.svg
├── data/
│   └── nayarit_idoneidad.geojson  (área de estudio e idoneidad)
└── README.md
```

## Cómo publicar en GitHub Pages

1. Crea un repositorio en https://github.com (por ejemplo `site-cafe`).
2. Sube todos los archivos de esta carpeta al repositorio:
   ```bash
   git init
   git add .
   git commit -m "Sitio web investigación café Nayarit"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/site-cafe.git
   git push -u origin main
   ```
3. En GitHub, entra a **Settings > Pages**.
4. En **Source** selecciona `Deploy from a branch` y la rama `main` con la carpeta raíz (`/`).
5. Guarda y espera 1-2 minutos; el sitio quedará en:
   `https://TU_USUARIO.github.io/site-cafe/`

> El sitio funciona 100 % con archivos estáticos (HTML, CSS, JS y GeoJSON);
> Leaflet se carga desde CDN, por lo que solo se requiere conexión a internet.

## Nota sobre el mapa

Los polígonos del GeoJSON son una **representación esquemática** del corredor
de aptitud identificado en el estudio. Para obtener la cartografía oficial,
consulta las figuras y tablas del artículo fuente
(DOI 10.3390/ecologies4020018) y del capítulo (DOI 10.52501/cc.448.07).