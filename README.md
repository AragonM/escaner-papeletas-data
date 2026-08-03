# Escáner Papeletas — actualizaciones

Repo **público** que sirve las actualizaciones de la app Android **Escáner Papeletas** de
Áragon Estudios de Opinión. Aquí no hay código: el código vive en un repo privado aparte.

Existe por una razón concreta: un teléfono en campo tiene que poder consultar la versión y bajar el
APK **sin ninguna credencial**. Separarlo del código permite exactamente eso — el teléfono solo
conoce esta URL pública, jamás un token.

## Qué hay aquí

| Archivo | Para qué |
|---|---|
| `version.json` | Lo que consulta la app para saber si hay algo más nuevo |
| Releases | Cada APK publicado, como asset del release de su versión |

## `version.json`

```json
{
  "version": "1.1.0",
  "versionCode": 3,
  "releaseDate": "2026-08-03",
  "releaseNotes": "Qué cambió, en lenguaje de campo",
  "apkUrl": "https://github.com/AragonM/escaner-papeletas-data/releases/download/v1.1.0/escaner-papeletas-1.1.0.apk"
}
```

**`versionCode` es el campo que decide.** Es un entero que sube de 1 en 1 con cada publicación; la
app lo compara contra el que trae compilado y solo ofrece la actualización si el de aquí es mayor.
`version` es solo el nombre que lee la persona — comparar textos ("1.10.0" contra "1.9.0") daría el
resultado equivocado.

> El `versionCode` de este archivo debe coincidir con el del APK del release. Si se sube uno y no el
> otro, la app se ofrece una actualización a sí misma en bucle, o deja de ver las nuevas.

## Cómo actualizar la flota

1. En el repo privado: subir `versionCode` y `versionName`, y compilar el release firmado.
2. Publicar el APK como asset de un release aquí.
3. Actualizar `version.json` con la versión nueva.
4. En cada teléfono: **Cola → Ajustes → Buscar actualizaciones**.

El paso a paso completo está en el README del repo privado.

## Versiones

| Versión | `versionCode` | Qué trae |
|---|---|---|
| 1.1.0 | 3 | Textos de la pantalla de conexión más claros; recuadro del QR centrado desde el inicio |
| 1.0.0 | 2 | Primera versión firmada y distribuible, con actualizador incorporado |
