# FamaClub Records

Marcador de dominó y control de consumo de la mesa.
**La mesa · el marcador · la historia.**

## Qué hace

- Partida de 4 jugadores en 2 equipos, con meta configurable (100 / 200 / 300 / otra).
- Tocas el marcador de un equipo → teclado → **➕** y listo.
- Anotaciones en dos columnas, cada una bajo su equipo (como una hoja de anote).
- Editar o eliminar cualquier anotación: el total **siempre** se recalcula solo.
- Deshacer la última anotación.
- Se define por qué se juega (cerveza, refresco, comida) y cuántas debe el perdedor.
- Al ganar, la deuda se registra automáticamente a los dos jugadores perdedores.
- Consumo: personas con nombre y teléfono, productos (Presidente, Modelo, Ron, Picadera…), cantidad y nota, todo con fecha y hora.
- Historial de partidas con marcador, ganador, duración y lo que se jugó.
- Funciona **sin internet** y **no pide ninguna cuenta ni permiso**.

## Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub (público).
2. Sube **el contenido de esta carpeta** a la raíz del repo — `index.html`, `manifest.json`,
   `service-worker.js` y la carpeta `icons/`. No subas la carpeta contenedora.
3. En el repo: **Settings → Pages → Branch: `main` / carpeta `/ (root)` → Save**.
4. Espera 1–2 minutos. Tu app queda en `https://TUUSUARIO.github.io/TUREPO/`.

GitHub Pages sirve por HTTPS automáticamente, que es justo lo que el service worker
necesita para funcionar.

## Instalar en el teléfono (sin barra del navegador)

Abre la URL de arriba en el teléfono:

- **Android (Chrome):** aparecerá el botón *"⤓ Instalar la app"* dentro de la app,
  o usa el menú **⋮ → Instalar aplicación**.
- **iPhone (Safari):** botón **Compartir → Agregar a pantalla de inicio**.

Una vez instalada abre a pantalla completa, con su ícono propio y **sin la barra del
navegador** (eso lo da `"display": "standalone"` del manifest).

## Generar el .apk real

Con la URL de GitHub Pages ya publicada:

1. Entra a **pwabuilder.com** y pega tu URL.
2. Elige el paquete **Android**.
3. Descarga el `.apk` (para instalar a mano) o el `.aab` (para subir a Google Play), ya firmado.

No hay que cambiar nada del código: el `manifest.json` y el `service-worker.js` ya
cumplen todo lo que PWABuilder necesita.

## Estructura

```
index.html          La app completa (HTML + CSS + JS en un solo archivo)
manifest.json       Metadatos de instalación (nombre, íconos, standalone)
service-worker.js   Caché offline
icons/              Íconos en todos los tamaños + versiones maskable
```

## Nota técnica

El marcador **nunca** se guarda como un número suelto: siempre se calcula sumando cada
anotación individual guardada. Por eso editar o borrar una anotación jamás puede
descuadrar el total. Lo mismo aplica a los totales de consumo y deudas.

Los datos se guardan en el propio teléfono (localStorage). No se envía nada a ningún
servidor.
