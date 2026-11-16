# Dashboard OEE y Paradas de Línea – Envasado

Español | [English](README.en.md)

Dashboard en **Power BI** que mide el OEE de una planta embotelladora con sus tres componentes (disponibilidad, rendimiento y calidad), identifica las paradas de mayor impacto hasta el nivel de subcausa y equipo, y cuantifica el efecto de las acciones de mejora.

![Desempeño operativo]
## Problema de negocio

Las paradas de línea se registraban con detalle, pero sin relacionarlas con la producción. No era posible responder rápido cuánto OEE se pierde y por qué, qué causas y equipos explican el tiempo detenido, qué líneas y turnos rinden peor y si las mejoras funcionan.

**Pregunta central:** ¿cómo convertir los registros de producción y paradas en indicadores que prioricen las acciones de mantenimiento y mejora continua?

## Resultados clave

| Indicador | Valor |
|---|---|
| OEE anual | **78.6 %** (meta 85 %, brecha −6.4 pp) |
| Disponibilidad / Rendimiento / Calidad | 89.8 % / 88.8 % / 98.5 % |
| Horas de parada | 2,673 h (≈ 1.56 M cajas no producidas) |
| OEE antes vs. después de las mejoras | 74.1 % → **82.9 % (+8.8 pp)** |
| Horas de parada antes vs. después | **−37 %** |
| Cambio de formato (SMED) | 29.4 → **19.2 min (−35 %)** |

## Principales hallazgos

- **Disponibilidad y rendimiento explican el 94 % de la pérdida de OEE**; la calidad tiene un impacto menor.
- **Mantenimiento (31.7 %) y Preparación de máquina (26.2 %)** concentran el 58 % del tiempo de parada y tienen las paradas más largas (~25 min).
- **11 de 18 causas explican el 80 %** del tiempo detenido; Mantenimiento mecánico es la principal (15 %).
- Las tres líneas tienen un OEE similar, pero **L1 concentra el 57 % de las cajas perdidas** por su mayor velocidad.
- El **turno C** tiene el OEE más bajo (77.1 %) por menor rendimiento, no por más paradas.

## Recomendaciones

1. Plan de mantenimiento preventivo para sensores, rodamientos de llenadora, transmisión y tablero eléctrico, con seguimiento mensual de MTTR y MTBF.
2. Extender SMED a calibraciones, arranques y cambios de producto, replicando lo logrado en cambio de formato.
3. Priorizar L1: cada hora recuperada vale más del doble que en L2.
4. Revisar velocidad y prácticas del turno C, estandarizando las del turno A.

## Dashboard

| Análisis de paradas | Impacto de la mejora |
|---|---|
|**[Proyecto_OEE_page-0001)](img/Proyecto_OEE_page-0001.jpg)** **[Proyecto_OEE_page-0002](img/Proyecto_OEE_page-0002.jpg)** |**[Proyecto_OEE_page-0003](img/Proyecto_OEE_page-0003.jpg)**|

## Solución técnica

- **Modelo en estrella:** 2 tablas de hechos (producción y paradas) y dimensiones de calendario, línea, turno y parada (categoría → causa → subcausa → equipo).
- **55 medidas DAX** organizadas en carpetas: OEE y componentes, MTTR, MTBF, Pareto con RANKX y % acumulado, cascada de pérdidas, cajas perdidas y comparación Antes/Después.
- **Power Query** para tipificar datos y separar fecha y hora de cada parada.
- **Datos:** 3,285 registros de producción y 7,821 paradas de 3 líneas y 3 turnos (año 2025).

![Modelo de datos]

```DAX
OEE = [Disponibilidad] * [Rendimiento] * [Calidad]
MTTR = DIVIDE([Tiempo Parada], [Número de Paradas], 0)
OEE Antes = CALCULATE([OEE], CalendarioDAX[Periodo] = "Antes")
```

## Herramientas

Power BI · Power Query · DAX · Modelamiento dimensional · Visualización de datos

## Estructura del repositorio

```
├── README.md            Este documento
├── README.en.md         Versión en inglés
├── docs/Informe_OEE.pdf Informe completo del análisis
├── img/                 Capturas del dashboard y del modelo
└── (archivo .pbix y datos, si se publican)
```

**[Ver informe completo (PDF)](docs/Proyecto_OEE.pdf)**

## Notas

Empresa ficticia (Embotelladora SAC) y datos sintéticos construidos para el proyecto; no corresponden a resultados de ninguna empresa real.

## Autor

**Sergio Aguilar Dinis** – Data Analyst | Business Intelligence
[LinkedIn](https://www.linkedin.com/in/sergio-aguilar-dinis-4766b858) · [Portafolio](https://fancy-coyote-67e.notion.site/PORTFOLIO-ES-b44f7f51a593839abe7b0196b748def2)
