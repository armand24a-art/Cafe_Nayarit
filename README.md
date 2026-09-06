# El corredor del café — Nayarit

Sitio web de divulgación científica para el modelo de distribución potencial de
café (*Coffea arabica*) en Nayarit y la propuesta de Área Prioritaria de
Producción Sostenible de Café (APS-Café).

Basado en:

- Ávalos-Jiménez, A.; Marceleño-Flores, S.M.L.; Nájera-González, O.; Flores-Vilchez, F. (2023).
  *Potential Coffee Distribution in a Central-Western Region of Mexico*. Ecologies, 4(2), 269–287.
  https://doi.org/10.3390/ecologies4020018
- Ávalos-Jiménez, A.; Flores-Vilchez, F.; Arcadia-Peralta, E.A. (2026).
  *Área prioritaria de producción sostenible de café (APS-Café), en Nayarit*.
  En: *Café de Nayarit: sostenibilidad, biodiversidad y patrimonio socioeconómico*. Comunicación Científica.
  https://doi.org/10.52501/cc.448.07
- Nájera González, A.; Nájera González, O.; Marceleño Flores, S.M.L. (coords.) (2026).
  *Café de Nayarit: sostenibilidad, biodiversidad y patrimonio socioeconómico*. Comunicación Científica.
  https://doi.org/10.52501/cc.448

## Qué incluye

```
cafe-nayarit-site/
├── index.html              → toda la página (estructura + estilos + interactividad)
├── data/
│   └── area_estudio.geojson → capa real de idoneidad para café (5 niveles), derivada del
│                              shapefile del modelo, disuelta por nivel y simplificada
└── README.md
```

El mapa usa **Leaflet** con dos capas base (OpenStreetMap y satélite Esri) y
carga el polígono real del área de estudio desde `data/area_estudio.geojson`.

### Sobre el archivo geojson

El archivo `Cafe.geojson` que compartiste contenía 7,169 polígonos en proyección
UTM zona 13N (EPSG:32613), con la clasificación de idoneidad del modelo MaxEnt
en 5 niveles (Nula, Muy Baja, Baja, Media, Alta) para cada uno de los 18
municipios de Nayarit. Para usarlo en la web, sin perder el desglose municipal
real, se hicieron tres transformaciones:

1. **Reproyección** de EPSG:32613 a EPSG:4326 (lat/lon), que es lo que requiere Leaflet.
2. **Disolución por municipio + nivel de idoneidad**: los 7,169 polígonos se agruparon
   en 65 (18 municipios × los niveles presentes en cada uno), sumando la superficie real
   (`Supha`) de cada combinación. Esto conserva el dato real por municipio — el mismo
   nivel de detalle que usa la Tabla 5 del capítulo del libro — sin cargar miles de
   parcelas diminutas innecesarias para una vista estatal.
3. **Simplificación geométrica** (tolerancia ~35 m, topología preservada) y redondeo de
   coordenadas a 5 decimales, para que el archivo pese ~320 KB en vez de 6 MB.

El resultado son datos reales, no aproximados: las hectáreas que ves en el mapa, en
las tablas bajo el mapa y en los popups de cada polígono son sumas exactas de las
hectáreas (`Supha`) del archivo original, agrupadas por municipio y nivel.

Con esta capa, el propio sitio calcula en el navegador (con JavaScript, no con
números fijos en el HTML) la superficie total por nivel y el ranking de municipios
con idoneidad "Alta" — por eso aparecen ahí municipios como Ruíz, Santiago Ixcuintla
o Del Nayar, que el artículo original no menciona explícitamente pero que sí
tienen parcelas de alta idoneidad según el propio modelo.

Si quieres el detalle completo sin disolver (los 7,169 polígonos originales, solo
reproyectados) para un análisis más fino en un SIG de escritorio, dímelo y te
preparo esa versión aparte — para la web no se recomienda por su peso.

## Cómo probarlo en tu computadora antes de publicar

Los navegadores bloquean `fetch()` de archivos abiertos directamente con `file://`,
así que para ver el mapa correctamente durante las pruebas locales corre un
servidor simple desde la carpeta del proyecto:

```bash
cd cafe-nayarit-site
python3 -m http.server 8000
```

Y abre `http://localhost:8000` en tu navegador.

## Cómo publicarlo en GitHub Pages

1. Crea un repositorio nuevo en GitHub (por ejemplo `cafe-nayarit`).
2. Sube estos tres elementos (`index.html`, la carpeta `data/`, y este `README.md`)
   a la raíz del repositorio.
3. Ve a **Settings → Pages** en el repositorio.
4. En **Source**, elige la rama `main` y la carpeta `/ (root)`, y guarda.
5. Espera 1–2 minutos: GitHub te dará una URL del tipo
   `https://tu-usuario.github.io/cafe-nayarit/`.

Si prefieres hacerlo por línea de comandos:

```bash
git init
git add .
git commit -m "Publicar sitio del corredor del café en Nayarit"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/cafe-nayarit.git
git push -u origin main
```

Luego activa Pages como en el paso 3–4.

## Personalización rápida

- **Enlaces a documentos**: en `index.html`, busca la sección `id="documentos"` y
  cambia las URLs de los botones si cambian los DOI o si subes tú mismo los PDF
  (por ejemplo a la carpeta del repositorio) en vez de enlazar a comunicacion-cientifica.com.
- **Colores**: todos los colores están definidos como variables al inicio del
  `<style>` (`--parchment`, `--ink`, `--cherry`, `--sage`, `--gold`), así que puedes
  cambiar la paleta completa editando esas ocho líneas.
- **Textos**: todo el copy está en español directamente en el HTML, buscable por
  sección (`<section id="...">`).
