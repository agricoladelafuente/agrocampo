# 🌿 GestiónAgro

Control operativo de horas, pagos, seguridad social y gasoil para dos empresas agrícolas.

## 🚀 Instalación

### 1. Google Sheet

Crea un Sheet con **5 pestañas** (nombres exactos):

| Pestaña | Cabeceras fila 1 |
|---|---|
| `Horas` | id · fecha · emp · trab · horas |
| `Pagos` | id · fecha · emp · trab · importe · metodo |
| `SS` | id · mes · emp · trab · dias |
| `Gasoil` | id · tipo · fecha · emp · litros · precio |
| `Trabajadores` | id · name |

### 2. Apps Script

1. En el Sheet → **Extensiones → Apps Script**
2. Pega el código de `apps-script.js`
3. **Implementar → Nueva implementación → Aplicación web**
   - Ejecutar como: Yo
   - Acceso: **Cualquier persona**
4. Copia la URL

### 3. GitHub Pages

1. Crea repo `gestionagro` en GitHub
2. Sube `index.html` y `README.md`
3. **Settings → Pages → main → root**

### 4. Conectar

Abre la app → pega la URL del Apps Script → Conectar

## 📱 Móvil

Abre en Chrome/Safari → Menú → **Añadir a pantalla de inicio**
