# Set Up Dashboard - MVP de Aperturas de Service Centers

Dashboard automatizado para dar visibilidad semanal al equipo de Set Up sobre el estado de apertura de Service Centers distribuidos en México, reduciendo el tiempo de preparación de reportes de 2+ horas a menos de 5 minutos.

## Contexto del Proyecto

El equipo de Set Up gestiona la apertura Service Centers en distintos estados de México. La información estaba dispersa entre Monday.com, Google Sheets y registros manuales, sin visibilidad consolidada. Este proyecto resuelve ese problema con un pipeline automatizado de datos, un tablero visual y un módulo de IA para detección de riesgos.

## Entregables

### 1. Consolidación de Datos (Python + Pandas)
- Carga y limpieza del dataset de Service Centers
- Cálculo de métricas consolidadas: avance total por categoría, días de retraso acumulado, clasificación de riesgo (semáforo)
- Métricas financieras adicionales: desviación de CapEx
- Exportación a formato estructurado para el tablero

### 2. Tablero Visual (Looker Studio)
- *Tarjetas de resumen:* Total de SCs, % de avance promedio, SCs en riesgo crítico
- *Gráfica de barras apiladas:* avance por categoría segmentado por estado
- *Tabla detallada:* con formato condicional (verde/amarillo/rojo) según días de retraso
- *Filtros interactivos:* por estado, tipo de SC y rango de fechas

 *[Ver tablero en vivo](https://datastudio.google.com/reporting/c85f14d1-cab5-484b-81fa-2da678ba3e5b)*

### 3. Módulo de IA para Detección de Riesgos (Claude API)
- Recibe el DataFrame consolidado en formato JSON
- Genera automáticamente un resumen ejecutivo (máx. 80 palabras)
- Identifica los 3 principales riesgos operativos de la semana
- Propone acciones concretas por cada riesgo

## Tecnologías Utilizadas

- *Python 3* con pandas para ETL
- *Google Colab* como entorno de ejecución
- *Looker Studio* para visualización
- *Anthropic Claude API* para análisis con IA
- *Google Sheets* como fuente de datos del tablero

## Estructura del Repositorio

- set_up_dashboard.ipynb — Notebook con el pipeline completo (carga, limpieza, transformación, exportación y módulo de IA)
- service_centers_consolidado.xlsx — Dataset procesado y consolidado
- resumen_ejecutivo_[Fecha].md — Ejemplo de salida del módulo de IA

## Cómo Reproducir

1. Abrir el notebook en Google Colab
2. Subir el archivo de datos de Service Centers
3. Configurar la API key de Anthropic en los Secretos de Colab (nombre: antropic_api_key)
4. Ejecutar todas las celdas en orden (Entorno de ejecución → Ejecutar todas)
5. El tablero se conecta a la hoja de Google Sheets exportada

## Notas de Implementación

- Para la exportación de datos se optó por Excel + carga a Google Sheets debido a restricciones de seguridad organizacionales (política iam.disableServiceAccountKeyCreation activa por defecto). En un entorno productivo se implementaría con OAuth 2.0 o Workload Identity Federation.
- El dataset incluye 10 estados (vs. los 4 mencionados originalmente en el brief), reflejando una distribución geográfica más amplia.

## Autor

[Monica Alejandra Martinez Mendoza] — Caso práctico para [Mercado Libre]
