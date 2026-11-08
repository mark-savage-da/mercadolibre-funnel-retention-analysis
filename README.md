# MercadoLibre Funnel & Retention Analysis

## Project Overview

Este caso de portafolio de Miguel Torres parte de un proyecto aprobado en TripleTen. Analicé dónde se pierden más usuarios en el recorrido de compra y en qué momento conviene probar una acción para que vuelvan después de registrarse. El **14,32 %** de quienes seleccionaron un producto lo agregó al carrito. Ese fue el punto con mayor pérdida entre las transiciones analizadas.

## Business Context

Para priorizar mejoras en la experiencia de compra, el equipo de producto necesita saber si los usuarios abandonan antes de agregar un producto al carrito o cuando ya están intentando pagar. La actividad después del registro permite identificar un momento para probar acciones que incentiven el regreso a la plataforma.

## Datasets Used

- **Eventos de compra (`mercadolibre_funnel`).** Registran las acciones de usuarios y sesiones, junto con su fecha y país. El embudo cubre del 1 de enero al 31 de agosto de 2025.
- **Actividad después del registro (`mercadolibre_retention`).** Permite identificar si un usuario estuvo activo a los 7, 14, 21 y 28 días de registrarse. El resumen ejecutivo de retención se centra en los registros del 1 de enero al 1 de junio de 2025.

## Project Objectives

- Identificar la transición con mayor pérdida de usuarios en el recorrido de compra.
- Medir cómo cambia la actividad tras el registro y comparar los resultados por país.
- Proponer acciones que puedan evaluarse con métricas de conversión y retención.

## Analytical Workflow

### 1. Data Loading and Initial Exploration

Usé SQL para inspeccionar las primeras filas de las tablas e identificar los eventos del recorrido de compra.

### 2. Data Quality Review

Revisé la estructura de las tablas para identificar los campos de usuario, sesión, fecha y actividad que sustentan el análisis.

### 3. Data Cleaning

Para el embudo, la fecha relevante es la del evento de compra. Para la retención, el seguimiento empieza en la fecha de registro de cada usuario.

### 4. User-Level Aggregation

El embudo resume el avance entre pasos, desde la primera visita hasta la compra. Para analizar la retención, agrupé a los usuarios por mes de registro. Cada grupo mensual es una cohorte.

### 5. Descriptive Analysis

Comparé la proporción que avanzó de un paso al siguiente y la proporción de usuarios activos en cada momento de seguimiento. El libro de análisis reúne los resultados generales y el desglose por país.

### 6. Data Visualization

Cada barra muestra qué porcentaje avanzó al siguiente paso. La barra destacada muestra la transición con menor conversión.

<p align="center">
  <img src="images/1_mercadolibre-funnel-conversion.png" alt="Conversión entre etapas del embudo. De selección a carrito avanzó el 14,32 %, la tasa más baja de las cinco transiciones mostradas." width="760">
</p>

*Fuente · Excel aprobado, hoja `Resumen`, rango `A9:C14`. Los valores se pueden consultar en el [libro de análisis](mercadolibre-funnel-retention-analysis.xlsx).*

La segunda gráfica muestra qué porcentaje de las personas que se registraron en marzo de 2025 estuvo activo a los 7, 14, 21 y 28 días.

<p align="center">
  <img src="images/2_mercadolibre-march-2025-cohort-retention.png" alt="Actividad de los usuarios registrados en marzo de 2025. El 87,7 % estuvo activo el día 7, el 56,8 % el día 14, el 26,6 % el día 21 y el 3,0 % el día 28." width="760">
</p>

*Fuente · Excel aprobado, hoja `Retencion x Cohort`, rango `A4:E4`. Los valores se pueden consultar en el [libro de análisis](mercadolibre-funnel-retention-analysis.xlsx).*

### 7. Outlier Detection

El libro también incluye a los usuarios registrados en agosto. En ese grupo, el **70,8 %** estuvo activo a los 7 días y el **0,2 %** a los 28 días. Agosto se presenta por separado porque queda fuera del periodo de registro usado en el resumen ejecutivo de retención.

### 8. Customer Segmentation

A los 28 días del registro, el porcentaje de usuarios activos fue del **3,2 % en Perú**, el **3,1 % en México** y el **1,6 % en Colombia**. El desglose muestra cómo varía la actividad entre mercados.

### 9. Executive Insights

La ficha del producto es el primer punto para probar una mejora de conversión. Para retención, la segunda semana después del registro ofrece un momento para probar una comunicación que invite al usuario a volver.

## Key Tasks Performed

Exploré las tablas con SQL, documenté en Excel el embudo y la retención por país y por mes de registro, y preparé dos gráficas para comunicar los hallazgos.

## Key Findings

- **Conversión.** El **85,68 %** de quienes seleccionaron un producto no lo agregó al carrito. Fue la mayor pérdida del embudo y sitúa la primera prueba de conversión en la ficha del producto.
- **Retención.** Entre los usuarios incluidos en el resumen ejecutivo, el **86,6 %** estuvo activo a los 7 días del registro y el **55,4 %** a los 14 días. La caída de **31,2 puntos porcentuales** entre ambos cortes señala cuándo probar una acción de reactivación. En D28, la actividad fue del **2,6 %**.

## Business Recommendations

- **Facilitar el paso al carrito.** Probar si mostrar el costo y el plazo de entrega en la ficha aumenta la proporción de usuarios que agregan un producto al carrito. Medir también cuántos terminan comprando.
- **Invitar al usuario a volver durante su segunda semana.** Enviar un recordatorio entre los días 7 y 14 después del registro a un grupo de usuarios. Comparar cuántos vuelven a usar la plataforma frente a un grupo similar que no recibe el mensaje.

## Tools and Skills

**SQL** para explorar las tablas y estructurar el análisis de conversión y retención. **Excel** para documentar resultados, comparar mercados y preparar el resumen ejecutivo.

## Professional Value

El análisis conecta dos decisiones de producto con sus métricas. Una mejora en la ficha se evalúa por el paso al carrito y la compra final. Una acción de reactivación se evalúa por el regreso de usuarios registrados.

## Personal Voice & Learning

Al revisar el embudo, encontré que el mayor punto de pérdida ya aparecía al pasar de la ficha al carrito. Ese hallazgo me permitió formular una prueba concreta sobre la información que ve el comprador antes de decidir.

## Repository Structure

```text
mercadolibre-funnel-retention-analysis/
├── images/
│   ├── 1_mercadolibre-funnel-conversion.png
│   └── 2_mercadolibre-march-2025-cohort-retention.png
├── README.md
└── mercadolibre-funnel-retention-analysis.xlsx
```

### File Guide

- [Libro de análisis](mercadolibre-funnel-retention-analysis.xlsx) · Resumen ejecutivo y tablas de conversión y retención.
- [Gráficas](images/) · Archivos PNG del embudo y de la actividad de los usuarios registrados en marzo.

## Reproducibility Note

El [libro de análisis](mercadolibre-funnel-retention-analysis.xlsx) contiene los valores usados en las gráficas. La hoja `Resumen` presenta la conversión entre etapas y `Embudo General` muestra el avance acumulado. Para la segunda gráfica se usa la fila de marzo de 2025 en `Retencion x Cohort`. El repositorio publica las tablas de resultados y las visualizaciones.
