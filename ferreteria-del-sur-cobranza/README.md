# Cobranza sin trabajo manual en una ferretería de tres sucursales

**Contexto:** comercio minorista de materiales de construcción, tres sucursales,
área de administración. Caso anonimizado.

**Mi rol:** relevamiento, diseño e implementación.
**Herramientas:** plataforma de automatización en nube gestionada, Google Sheets, correo.
**Duración:** 40 horas de construcción.

## 1\. Problema

Dos administrativas dedicaban unas **20 horas por semana**, 80 por mes, a conciliar
pagos de cuenta corriente y enviar recordatorios de vencimiento a mano.

El error más caro no era el tiempo: **15 veces por mes** se le reclamaba el pago a un
cliente que ya había pagado.

Sin cambiar nada, el problema crecía con cada sucursal nueva.

## 2\. Decisión

**Infraestructura: nube gestionada, plan Pro.** Se descartó un VPS con Docker, que salía
más barato en servidor, porque el cliente no tiene a nadie que lo opere.

**Diseño: conciliación por lote cada hora**, en lugar de una ejecución por pago. Así el
volumen entra en el cupo del plan sin cambiar de categoría.

## 3\. Implementación

Cuatro subflujos: lectura de pagos, conciliación contra cuenta corriente, armado de
recordatorios y envío.

Dos alertas: una de errores de ejecución y otra de consumo del cupo del plan.

La operación quedó documentada en un runbook, con el procedimiento de reproceso y a
quién se escala.

El costo mensual está calculado en el modelo de costos, abierto en tres capas.

**Evidencia:** [flujos](evidencia/flujos/) · [diagrama](evidencia/diagrama/) ·
[runbook](evidencia/runbook/) · [modelo de costos](evidencia/modelo-de-costos/)

## 4\. Impacto medido



*| Métrica | Antes | Después | Cómo se midió |*

*|---|---|---|---|*

*| Horas manuales por mes | 80 | 6 | Registro de horas de administración |*

*| Recordatorios a quien ya pagó (por mes) | 15 | 1 | Reclamos y log del flujo |*

*| Días promedio de cobro | 45 | 38 | Reporte contable (estimado) |*

*| Ejecuciones por mes | — | 2.400 | Panel de Insights |*

*| Tasa de error | — | 0,8% | Log del flujo |

\*\*Traducción a negocio.\*\* La automatización libera 74 horas de trabajo*

*administrativo por mes, casi dos semanas de una persona, y evita 14 reclamos de cobro a*

*clientes que ya habían pagado.*



*Con una inversión inicial de 1.200 dólares y un costo de operación de 70 dólares*

*mensuales, \*\*se pagó sola en menos de dos meses\*\*.*



*> Los días promedio de cobro bajaron de 45 a 38, pero ese número está marcado como*

*> \*\*estimado\*\*: en el mismo período el cliente lanzó un descuento por pago anticipado, y*

*> no se puede atribuir toda la mejora a la automatización.*



