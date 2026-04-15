# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Estado actual del repositorio
- El repositorio contiene una app web estática en un único archivo: `index.html`.
- No hay `package.json`, `pyproject.toml`, `go.mod`, `Makefile` ni otros manifiestos de build/lint/tests.
- No existen archivos de reglas adicionales (`WARP.md`, `CLAUDE.md`, `.cursorrules`, `.cursor/rules/`, `.github/copilot-instructions.md`).

## Comandos y flujo de trabajo (reales para este repo)
- Clonar:
  - `git clone https://github.com/agricoladelafuente/agrocampo.git`
- Ver cambios:
  - `git status`
  - `git --no-pager diff`
- Ejecutar localmente:
  - Abrir `index.html` en navegador.
- Build/Lint/Tests:
  - No hay pipeline configurado de build.
  - No hay lint automatizado configurado.
  - No hay suite de tests automatizada.
  - No aplica “ejecutar un test individual” porque no existe framework de testing en el repo.

## Funcionalidad core verificada (navegador)
- Carga inicial de la app (`HTTP 200` y render de `#appContent`).
- Navegación entre secciones principales (`horas`, `pagos`, `ss`, `gasoil`, `trab`, `config`, `informes`).
- Apertura y cierre de modal de registro de horas.
- Persistencia de configuración en `localStorage` (`ga_cfg`).
- Generación de informe en la vista de `informes` (tipo 5).

## Arquitectura de alto nivel
- **Frontend monolítico**: toda la UI, estilos y lógica están embebidos en `index.html`.
  - Estructura: HTML de secciones/modales + CSS inline + JavaScript inline.
  - Navegación por secciones (`horas`, `pagos`, `ss`, `gasoil`, `trab`, `config`, `informes`) controlada por `go(...)`.
- **Estado en memoria**:
  - Objeto global `D` con colecciones generales y por empresa (`*_E1`, `*_E2`).
  - Configuración local en `localStorage` bajo `ga_cfg` (`precioHora`, `costeSS`, `horasJornada`).
- **Backend externo (Google Apps Script)**:
  - Endpoint en `URL_API` (script web de Google Apps Script).
  - Comunicación por JSONP (`jsonp(...)`) con acciones como `getAllByEmp`, `add`, `delete`, `ping`.
  - `loadAll()` hidrata el estado completo desde Sheets.
- **Capa de dominio**:
  - CRUD por módulo (`addH`, `addP`, `addSS`, `addGC`, `addGP`, `addW`, `del`).
  - Renderizadores por sección (`renH`, `renP`, `renS`, `renG`, `renW`).
  - Cálculo de gasoil por PMP con `calcPMP(...)`.
  - Informes en `genR()` con 5 tipos y salida imprimible (`printR()`).

## Dependencias operativas externas (README)
- La fuente de datos está en Google Sheets y requiere pestañas con nombres y cabeceras exactas:
  - `Horas`: `id`, `fecha`, `emp`, `trab`, `horas`
  - `Pagos`: `id`, `fecha`, `emp`, `trab`, `importe`, `metodo`
  - `SS`: `id`, `mes`, `emp`, `trab`, `dias`
  - `Gasoil`: `id`, `tipo`, `fecha`, `emp`, `litros`, `precio`
  - `Trabajadores`: `id`, `name`
- El README indica pegar código de `apps-script.js` en Apps Script, pero ese archivo no está en este repositorio. Si se necesita tocar backend, primero recuperar/crear ese script.
- Despliegue documentado en README mediante GitHub Pages (rama `main`, raíz del repo).
