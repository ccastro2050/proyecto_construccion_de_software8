# Especificación — Versión 8: la facturación en el navegador (el cierre)

> **Versión 8** ([mapa](../0_mapa_versiones.md)) · Acumulativa: v1–v7
> intactas. La operación de negocio más rica del sistema — los SPs y
> triggers de la v2 — por fin con pantalla. Con esto la ruta del curso
> queda COMPLETA: API específica tri-motor + front completo.

## 1. Propósito
Crear, consultar y anular facturas desde el navegador, con la regla de
oro intacta: **el front no calcula NADA** — subtotales, total y stock
los pone la BD (triggers) a través de la API.

## 2. Alcance
**Incluye:** `/facturas` (lista con estado y total) · `/facturas/{n}`
(detalle maestro-renglones con nombres resueltos) · `/facturas/nueva`
(selects de cliente/vendedor + hasta 5 renglones producto+cantidad) ·
anular con confirmación (stock restaurado) · estados vestidos con la
marca (activa Verde Páramo, anulada Rojo Anulada).
**NO incluye:** editar/borrar facturas (anular ES la operación de
negocio, regla de la v2) · dashboards.

## 3. Requisitos funcionales
- **RF1** Listar: número, fecha, cliente y vendedor POR NOMBRE (los
  resolvió el SP), total y estado como badge de la marca.
- **RF2** Detalle: encabezado + renglones con subtotales de la BD.
- **RF3** Crear: selects cargados de la API; renglones diligenciados
  viajan como `productos:[{codigo, cantidad}]` al SP; el 422 y los
  errores del trigger (stock insuficiente) se muestran vestidos.
- **RF4** Anular: solo visible en facturas activas; 409 de la doble
  anulación y 404 mostrados como mensajes.

## 4. Criterios de aceptación
1. **Regresión:** smokes v6 y v7 sin cambios; diagnóstico `"version":"v8"`.
2. `/facturas` muestra las 6 semilla con nombres y badges.
3. Crear una factura (cliente 1, vendedor 1, PR001×2) desde el
   formulario: aparece con total CALCULADO y el stock de PR001 bajó
   (verificable por la API); el detalle muestra los renglones.
4. Anularla: mensaje de stock restaurado y badge en rojo; anularla otra
   vez → el mensaje del 409, vestido.
5. Crear con renglones vacíos → el 422 de la petición, vestido; con
   cantidad 9999 → el mensaje del trigger (stock insuficiente).

## 5. TERMINADA
Criterios en verde → tag `v8` → **la ruta del curso está COMPLETA**.
