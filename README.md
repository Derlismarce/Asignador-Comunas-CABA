# 🗺️ Asignador de Comunas CABA

Aplicación web para normalizar direcciones, geolocalizarlas y asignar automáticamente la comuna, el barrio y la Clave Vereda de la Ciudad Autónoma de Buenos Aires (CABA), pensada para tareas de inspección, fiscalización y análisis territorial. Corre 100% en el navegador, sin necesidad de servidor ni instalación.

---

## 🌐 Aplicación en línea

**https://derlismarce.github.io/Asignador-Comunas-CABA/**

---

## 🚀 Funcionalidades

### 👷 Por Inspector
Importa un Excel con columnas `INSPECTOR`, `DIRECCION` y `Geocodificación`, agrupa los puntos por inspector y permite descargar el recorrido de cada uno en KML (para Google Earth / Google My Maps) y en Excel — individualmente o todos juntos en un .zip.

### 🔀 Asignar Inspectores
A partir de dos archivos (direcciones con comuna, e inspectores con cupo por comuna), asigna cada dirección al inspector más cercano dentro de su comuna, respetando los cupos configurados. El algoritmo se refina en varias rondas para evitar que puntos queden asignados a un inspector lejano. Los puntos se pueden reasignar manualmente haciendo clic en el mapa, y el cambio se refleja automáticamente en las descargas.

### 🌐 Batch (normalización masiva)
Normaliza y geocodifica listas grandes de direcciones (miles de registros) de forma rápida:
- Un motor de normalización **local**, con el callejero oficial de CABA embebido y tolerancia a errores de tipeo (distancia de Levenshtein), resuelve la mayoría de las direcciones sin usar la red.
- Las direcciones resueltas localmente se geocodifican en **lotes de 10 en paralelo** contra el servicio de USIG, en vez de una petición por dirección.
- Lo que el motor local no puede resolver cae a un normalizador de direcciones por texto libre, como respaldo.
- También acepta coordenadas ya resueltas (formato grados/minutos/segundos o decimal) y hace geocodificación inversa para obtener calle y altura.
- Devuelve dirección normalizada, punto geográfico (WKT), comuna, barrio y **Clave Vereda** (buscada por cercanía contra un dataset oficial de ~326.000 tramos de vereda, con índice espacial en el navegador para que la búsqueda sea instantánea); exportable a CSV, Excel y KML.

### 🎨 Otras
- Modo claro / oscuro, con mapa base de OpenStreetMap en claro y CARTO Dark Matter en oscuro.
- Checkbox para mostrar u ocultar los polígonos de comuna sobre el mapa.
- Mini-juego "Space Cleaner" como créditos del proyecto (botón GCBA).

---

## 🛠️ Tecnologías utilizadas

- HTML5 + JavaScript (sin frameworks ni build step)
- [Leaflet.js](https://leafletjs.com/) para el mapa
- [SheetJS (xlsx.js)](https://sheetjs.com/) para leer/escribir Excel
- Mapas base: [OpenStreetMap](https://www.openstreetmap.org/) y [CARTO Basemaps](https://carto.com/basemaps/)
- Geocodificación y callejero oficial: [servicios USIG (GCBA)](https://usig.buenosaires.gob.ar/)
- Límites de comuna y dataset de veredas: información oficial del [Gobierno de la Ciudad de Buenos Aires](https://data.buenosaires.gob.ar/)

---

## 📁 Estructura del proyecto

```
Asignador-Comunas-CABA
│
├── index.html          (aplicación completa)
├── veredas_caba.json   (~326.000 puntos de referencia para Clave Vereda)
└── README.md
```

El callejero, los barrios y los límites de comuna están embebidos dentro de `index.html`. `veredas_caba.json` se descarga aparte (una sola vez, al usar la pestaña Batch) porque es un dataset grande; el resto de la app funciona sin conexión a internet salvo para geocodificar direcciones nuevas contra USIG.

---

## 🎯 Objetivo

Optimizar el procesamiento de grandes volúmenes de direcciones para organismos públicos, mejorando los tiempos de análisis y reduciendo el trabajo manual.

---

## 🔄 Historial de versiones

### Versión 2.1

- Se agrega **Clave Vereda** a la pestaña Batch, buscada por cercanía contra un dataset oficial de ~326.000 tramos de vereda (índice espacial local, sin perder velocidad).

### Versión 2.0

- Rediseño completo: pestañas **Por Inspector**, **Asignar Inspectores** y **Batch**.
- Motor de normalización de direcciones local + geocodificación en lote (mucho más rápido en archivos grandes).
- Reasignación manual de inspectores desde el mapa.
- Algoritmo de asignación por cercanía mejorado (varias rondas de refinamiento).
- Límites de comuna actualizados con dataset oficial, sin huecos entre comunas.
- Modo claro / oscuro.
- Corrección de bugs de parseo de CSV/Excel (comillas con separador embebido, encabezados con espacios).

### Versión 1.0

- Publicación inicial del proyecto.
- Importación de archivos Excel.
- Geolocalización de direcciones.
- Asignación automática de comunas.
- Visualización en mapa.

---

## 📌 Próximas mejoras

- Búsqueda individual de direcciones.
- Estadísticas por comuna.
- Exportación en PDF.

---

## 👨‍💻 Autor

**Derlis Marcelo Fernandez Rivas**

Desarrollador del proyecto.
