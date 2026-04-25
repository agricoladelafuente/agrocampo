# 🔒 Seguridad — GestiónAgro

## Autenticación

La aplicación utiliza **autenticación local con hash SHA256**. La contraseña se valida directamente en el navegador sin envío al servidor.

### Características de seguridad:

- ✅ **Hash SHA256** — La contraseña se almacena como hash (no en texto plano)
- ✅ **Validación client-side** — Funciona sin conexión a internet
- ✅ **Sin envío al servidor** — La contraseña nunca se transmite
- ✅ **Sesión en navegador** — Se guarda en `sessionStorage` (se borra al cerrar)

## Cambiar la contraseña

Para cambiar la contraseña:

### 1. Generar el hash SHA256

Ejecuta este comando en tu terminal (Linux/Mac):

```bash
echo -n "tu-nueva-contraseña" | sha256sum
```

Copia el resultado (todo antes del espacio).

**Ejemplo:**
```bash
$ echo -n "MiContraseñaSegura123" | sha256sum
abc1234567890def...  -
```

### 2. Actualizar el archivo

Abre `index.html` y busca esta línea (línea ~165):

```javascript
var PWD_HASH='bda2c12b1f6ce251b0174c3471d386c613c6c5f03e482852bbb9700e79deab87';
```

Reemplaza el hash por el nuevo:

```javascript
var PWD_HASH='abc1234567890def...';
```

### 3. Guardar y subir

```bash
git add index.html
git commit -m "Actualizar contraseña"
git push origin main
```

## Recomendaciones

🔐 **Usa contraseñas fuertes:**
- Mínimo 12 caracteres
- Mezcla: mayúsculas, minúsculas, números, símbolos
- Evita palabras comunes o información personal

⚠️ **Importante:**
- El hash es **unidireccional** — no se puede recuperar la contraseña del hash
- Mantén el hash en un lugar seguro
- Cambia la contraseña regularmente

## Recuperación de sesión

- La sesión se mantiene mientras el navegador esté abierto
- Si cierras el navegador, deberás volver a introducir la contraseña
- Los datos se guardan en Google Sheets (requiere conexión a Internet)

---

¿Preguntas? Consulta el `README.md` para instrucciones de instalación.
