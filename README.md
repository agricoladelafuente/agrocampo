# 🌿 GestiónAgro — Control Operativo

Aplicación web para el control de horas de trabajo, pagos, seguridad social y gasoil de dos empresas agrícolas compartidas.



**Demo:** `https://pedrocastillaortega.github.io/gestionagro/`

---

## 🚀 Instalación paso a paso

### Paso 1: Crear el Google Sheet

1. Ve a [Google Sheets](https://sheets.google.com) y crea una hoja nueva
2. Llámala **"GestiónAgro - Datos"**
3. Crea **5 pestañas** (hojas) con estos nombres exactos:

| Pestaña | Cabeceras (fila 1) |
|---|---|
| `Horas` | id \| fecha \| emp \| trab \| horas |
| `Pagos` | id \| fecha \| emp \| trab \| importe \| metodo |
| `SS` | id \| mes \| emp \| trab \| dias |
| `Gasoil` | id \| tipo \| fecha \| emp \| litros \| precio |
| `Trabajadores` | id \| name |

> ⚠️ Cada cabecera va en una celda separada. Pon "id" en A1, "fecha" en B1, etc.

### Paso 2: Configurar el Apps Script

1. En el Google Sheet, ve a **Extensiones > Apps Script**
2. Borra todo el código que haya
3. Pega el contenido completo del archivo `apps-script.js`
4. Guarda el proyecto (Ctrl+S) — ponle nombre "GestiónAgro Backend"

### Paso 3: Desplegar el Apps Script

1. En Apps Script, pulsa **Implementar > Nueva implementación**
2. Selecciona tipo: **Aplicación web**
3. Configura:
   - **Descripción:** GestiónAgro API
   - **Ejecutar como:** Yo
   - **Quién tiene acceso:** Cualquier persona
4. Pulsa **Implementar**
5. **Copia la URL** que te da (algo como `https://script.google.com/macros/s/ABC.../exec`)

> La primera vez te pedirá permisos para acceder a tu Google Sheet. Acéptalos.

### Paso 4: Subir a GitHub Pages

1. Ve a [GitHub](https://github.com) y crea un repositorio nuevo llamado `gestionagro`
2. Sube los archivos `index.html` y `README.md`
3. En el repositorio, ve a **Settings > Pages**
4. En "Source" selecciona **Deploy from a branch**
5. Selecciona la rama `main` y carpeta `/ (root)`
6. Guarda. En unos minutos estará en `https://pedrocastillaortega.github.io/gestionagro/`

### Paso 5: Conectar la aplicación

1. Abre la app en el navegador
2. Te aparecerá un banner pidiendo la URL
3. Pega la URL del Apps Script del paso 3
4. Pulsa **Conectar**

¡Listo! Los datos se guardan directamente en tu Google Sheet.

---

## 📱 Instalar en el móvil

1. Abre la URL en Chrome (Android) o Safari (iPhone)
2. Pulsa el menú (⋮ o compartir)
3. Selecciona **"Añadir a pantalla de inicio"**

---

## 📊 Funcionalidades

### Registro
- **⏱ Horas de trabajo** — por empresa, trabajador y fecha
- **💶 Pagos** — efectivo o transferencia/nómina
- **🏛 Seguridad Social** — jornadas oficiales cotizadas
- **⛽ Gasoil** — consumos diarios + compras con precio

### 4 Informes (de fecha a fecha)
1. **Horas** — desglose por empresa y trabajador con coste
2. **Pagos vs Coste** — saldo de cada empresa
3. **Seg. Social** — días reales vs cotizados + compensación entre empresas
4. **Gasoil** — inventario, desviaciones y valoración económica

### Configuración
- Precio/hora (por defecto 10,10 €)
- Coste SS/jornada (por defecto 18,17 €)
- Horas/jornada (por defecto 6,5)

---

## 🔧 Notas técnicas

- Frontend: HTML/CSS/JS puro (single page app)
- Backend: Google Apps Script + Google Sheets
- Comunicación: JSONP (evita problemas de CORS)
- La configuración (tarifas) se guarda en localStorage del navegador
- Los datos se guardan en Google Sheets (accesibles desde cualquier dispositivo)
- Compatible con móvil (responsive + bottom nav + FAB)
