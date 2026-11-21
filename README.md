# Control de puntualidad — FMDJ

Tablero mensual de atrasos de la Fundación Mariana de Jesús.

- **index.html**: la página que se abre por el enlace de GitHub Pages.
- **config.json**: configuración base. Aquí va la URL de Apps Script.
- **Code.gs**: el código que se pega en Apps Script. No se sube a GitHub.

La hoja de cálculo de Google es la base de datos. Ahí quedan los cortes, los ajustes, las justificaciones y la bitácora.

## Instalación (una sola vez)

### A. Hoja de cálculo y Apps Script

1. En Google Drive, con la cuenta institucional de Talento Humano, crea una hoja nueva: **Puntualidad FMDJ**.
2. Abre **Extensiones › Apps Script**. Borra lo que aparece y pega todo el contenido de `Code.gs`. Pulsa **Guardar**.
3. Vuelve a la hoja y recárgala. Aparece el menú **Puntualidad**.
4. Elige **Puntualidad › 1. Preparar hoja (primera vez)**. Google pide permisos: acéptalos.
5. Elige **Puntualidad › 2. Crear o cambiar usuario** y crea tu usuario:
   - Perfil: `admin`
   - Departamentos: `*`
   - ID de empleado: tu ID del biométrico (`2025`). Así el sistema no te deja justificar tus propios atrasos.
   - Clave: 10 caracteres o más, que no uses en otro sistema.
6. En Apps Script pulsa **Implementar › Nueva implementación**. En el engranaje elige **Aplicación web**.
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier persona**
7. Pulsa **Implementar** y copia la URL que termina en `/exec`.

### B. GitHub Pages

1. En `config.json`, reemplaza `PEGA_AQUI_LA_URL_QUE_TERMINA_EN_/exec` por la URL que copiaste. Mantén las comillas.
2. Sube `index.html` y `config.json` al repositorio. **No subas** `Code.gs` ni ningún Excel.
3. En el repositorio: **Settings › Pages › Branch: main / (root) › Save**.
4. El enlace queda como `https://talentohumano-cyber.github.io/NOMBRE-DEL-REPO/`.

### C. Usuarios

Créalos desde el menú **Puntualidad › 2. Crear o cambiar usuario**.

| Perfil | Qué puede hacer |
|---|---|
| `admin` | Cargar y guardar cortes, cambiar ajustes y parámetros, justificar, ver la bitácora |
| `director` | Ver y justificar solo los departamentos que le asignes |
| `lector` | Solo consultar los departamentos que le asignes |

Escribe los departamentos tal como salen en el reporte del biométrico: `FMDJ MATRIZ`, `CESI`, `SIL`, `CMAU-CREAR`, `Fundación Mariana de Jesús`.

Pon siempre el **ID de empleado** de cada director. Así no puede justificar sus propios atrasos.

## Uso mensual

1. Abre el enlace e ingresa con tu usuario.
2. Pulsa **Cargar Excel** y elige el reporte del biométrico.
3. Revisa la pestaña **Calidad de datos**.
4. Pulsa **Guardar corte en la nube**. Desde ese momento los directores lo ven y pueden justificar.
5. Cada corte queda en su propia pestaña de la hoja (`Corte 2026-11-19`). Los cortes anteriores se eligen en la lista de cortes del tablero.

## Si cambias el código de Code.gs

Apps Script sigue usando la versión anterior hasta que publicas una nueva:
**Implementar › Administrar implementaciones › lápiz › Versión: Nueva versión › Implementar**.
La URL `/exec` no cambia.

## Seguridad

- Comparte la hoja de cálculo **solo** con Talento Humano. Quien puede editar la hoja puede leer todo y saltarse los permisos del tablero.
- Las claves se guardan como huella cifrada (SHA-256 con sal), nunca en texto.
- La remuneración solo llega al perfil `admin`.
- Si una clave se filtra: **Puntualidad › Cerrar todas las sesiones abiertas** y crea una clave nueva para ese usuario.
- Para dar de baja a alguien: **Puntualidad › Desactivar usuario**.
