# Escáner Papeletas — canal de actualizaciones

Repositorio público que distribuye las actualizaciones de **Escáner Papeletas**, la aplicación
Android de levantamiento en campo de **Áragon Estudios de Opinión**.

Aquí no hay código fuente. Solo se publica lo que un teléfono necesita para mantenerse al día:
el archivo que anuncia la versión vigente y los instaladores de cada versión.

Es público a propósito. Un teléfono en campo debe poder consultar si hay una versión nueva y
descargarla sin credenciales de ningún tipo; separar la distribución del código permite eso sin
exponer nada más.

## Contenido

| Elemento | Función |
|---|---|
| `version.json` | Lo que consulta la aplicación para saber si existe una versión más reciente |
| Releases | El instalador (`.apk`) de cada versión publicada, con sus notas |

## Formato de `version.json`

```json
{
  "version": "1.6.0",
  "versionCode": 15,
  "releaseDate": "2026-08-07",
  "releaseNotes": "Qué cambió, en lenguaje de campo.",
  "apkUrl": "https://github.com/AragonM/escaner-papeletas-data/releases/download/v1.6.0/escaner-papeletas-1.6.0.apk",
  "sha256": "9b4410250f0b2b1e8aa1f8d25705ddb62962d0a17cc3e6e7aa06d696e11fb711"
}
```

**`versionCode` es el campo que decide.** Es un entero que aumenta de uno en uno con cada
publicación; la aplicación lo compara contra el que trae compilado y solo ofrece la actualización
si el de aquí es mayor. `version` es únicamente el nombre legible: comparar textos ("1.10.0" contra
"1.9.0") daría un resultado incorrecto.

**`sha256` es la huella del instalador.** La aplicación la compara con el archivo que descargó y
cancela la instalación si no coinciden — así, un archivo alterado o un instalador subido por error
nunca llega a un teléfono de campo. El campo es opcional para no dejar fuera a versiones anteriores
de la aplicación, pero **toda publicación nueva debe incluirlo**. Se obtiene con:

```
shasum -a 256 escaner-papeletas-<versión>.apk
```

> El `versionCode` de este archivo debe coincidir con el del instalador publicado en el release.
> Si uno se actualiza y el otro no, la aplicación ofrece indefinidamente una versión que ya tiene,
> o deja de ver las nuevas.

## Procedimiento de publicación

1. En el repositorio de código: incrementar `versionCode` y `versionName`, y compilar el instalador
   firmado (`assembleRelease`).
2. Publicar el `.apk` como archivo adjunto de un release en este repositorio.
3. Calcular su `sha256` y actualizar `version.json` con la versión, la huella y las notas.

La firma del instalador debe ser siempre la misma: Android rechaza actualizar una aplicación con un
archivo firmado por una llave distinta.

## Instalación en los teléfonos

Dentro de la aplicación: **Cola → Ajustes → Buscar actualizaciones**. No requiere cable, tienda de
aplicaciones ni desinstalar la versión anterior; los datos y los levantamientos pendientes de enviar
se conservan.

## Historial de versiones

| Versión | `versionCode` | Cambios |
|---|---|---|
| 1.6.0 | 15 | La captura sin señal ya no se registra como papeleta anulada; verificación de la huella y el origen del instalador; instalador 60 % más ligero |
| 1.5.4 | 14 | Lectura de papeletas impresas a una sola cara |
| 1.5.3 | 13 | Corrección del cierre inesperado al cargar proyectos |
| 1.5.2 | 12 | Corrección del bloqueo al escanear |
| 1.5.1 | 11 | Descarga automática de la plantilla al escanear una papeleta recién publicada |
| 1.5.0 | 10 | Voto por coalición, estabilidad y captura sin conexión |
| 1.1.0 | 3 | Mejoras en la pantalla de conexión |
| 1.0.0 | 2 | Primera versión distribuible, con actualización incorporada |
