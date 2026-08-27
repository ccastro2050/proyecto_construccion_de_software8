# Especificación — Versión 7: el front COMPLETO (las 12 entidades + roles)

> **Versión 7** ([mapa](../0_mapa_versiones.md)) · Acumulativa: v1–v6
> intactas. La v6 construyó UNA rebanada del front (producto); la v7
> demuestra que el molde del front es industrial — y estrena el control
> de acceso por ROLES (los datos RBAC de la v3, por fin trabajando).

## 1. Propósito
Todas las entidades operables desde el navegador SIN copiar 12 veces el
molde: un **registro de metadatos** (`entidades.py`) describe cada
entidad y unas **rutas genéricas** (`/e/<entidad>`) la sirven. El menú
se arma según el rol.

## 2. Alcance
**Incluye:** 9 entidades CRUD + 2 puentes (asignar/quitar la pareja
exacta, sin editar) · FKs como `<select>` cargados desde la API ·
secciones solo-admin (usuario, rol, ruta, puentes) ocultas y bloqueadas
sin el rol Administrador · `session["es_admin"]` decidido por la API.
**NO incluye:** la facturación en pantalla (v8) · editar puentes.

## 3. Requisitos funcionales
- **RF1** `/e/<entidad>`: listar/crear/editar(PATCH)/eliminar según el
  registro; errores de la API vestidos (como en v6).
- **RF2** FKs como select: cliente elige persona/empresa; vendedor,
  persona; los puentes, sus dos lados.
- **RF3** Puentes: asignar y QUITAR por la pareja exacta; sin editar.
- **RF4** Roles: el menú muestra solo lo permitido; entrar por URL a lo
  solo-admin sin serlo → rebote con mensaje.
- **RF5** Usuario: la lista jamás muestra contraseñas; editar re-hashea.

## 4. Criterios de aceptación
1. **Regresión:** smoke v6 (login + producto) sin cambios; diagnóstico
   `"version":"v7"`.
2. Un usuario SIN rol admin no ve las secciones admin (y por URL
   rebota); con el rol 1 asignado y reentrando, las ve.
3. La cadena comercial desde el navegador: empresa E200 → persona P020
   → cliente (con los selects) → vendedor — todo por formularios.
4. Puente: asignar un rol a un usuario y quitar ESA pareja.
5. Los 51 endpoints de la API responden igual (nada se tocó).

## 5. TERMINADA
Criterios en verde → tag `v7` → solo entonces se especifica la v8.
