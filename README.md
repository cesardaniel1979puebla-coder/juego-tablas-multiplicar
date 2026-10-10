# Saltos multiplicadores

Juego educativo de las tablas del 2 al 9, de ×1 a ×10. Funciona sin dependencias, recursos externos ni servicios de pago.

## Abrir el juego

Descarga `index.html` y ábrelo en un navegador. En Android puedes abrir el archivo con Chrome desde el gestor de archivos. Para una dirección web local, ejecuta desde esta carpeta:

```sh
python3 -m http.server 8000 --bind 0.0.0.0
```

Abre `http://localhost:8000` en el mismo equipo. En un celular conectado a la misma red, usa `http://IP-DEL-EQUIPO:8000` y permite ese puerto en el firewall si fuera necesario. Un entorno en la nube necesita exponer el puerto 8000 mediante su vista previa de puertos.

## Cómo jugar

Toca una de las tres respuestas para saltar. Cada acierto avanza a la siguiente multiplicación. Un error muestra la respuesta correcta y permite reiniciar la tabla actual desde ×1. Los botones superiores permiten elegir cualquier tabla; una marca indica las completadas.

El navegador guarda las tablas completadas y la multiplicación actual mediante `localStorage`. Al cambiar de tabla se empieza en ×1. Los datos pertenecen al navegador y a la dirección utilizada; borrar sus datos elimina el progreso. Si el navegador bloquea el almacenamiento, aparece un aviso y el juego sigue funcionando sin guardar. Para guardar de manera estable, utiliza siempre la misma dirección HTTP.

El juego admite controles táctiles, teclado y la preferencia de movimiento reducido.

## PWA instalable y publicación gratuita con HTTPS

La PWA incluye `manifest.webmanifest`, `sw.js` e íconos PNG en `icons/`. No requiere compilación ni instalación de dependencias. El service worker descarga el juego en la primera visita; espera a ver **Listo para jugar sin internet** antes de desconectarte. El progreso sigue usando la misma clave de `localStorage` que el juego original. El progreso de un archivo local o de otra dirección no se transfiere automáticamente a la nueva dirección HTTPS.

### Publicar con GitHub Pages (desde el navegador)

Para usar Pages gratis con una cuenta GitHub Free, el repositorio debe ser público. Comprueba la visibilidad en Settings → General. Si es privado, no cambies la visibilidad sin antes revisar que no contiene información privada; también puedes crear un repositorio público nuevo con estos archivos y adaptar la dirección.

1. Descomprime `saltos-multiplicadores-pwa.zip` en tu equipo.
2. Abre `https://github.com/cesardaniel1979puebla-coder/juego-tablas-multiplicar` e inicia sesión con la cuenta que puede editarlo. Selecciona la rama `main`.
3. En **Add file → Upload files**, arrastra `index.html`, `manifest.webmanifest`, `sw.js`, `README.md` y la carpeta `icons` desde el paquete. Conserva la carpeta `icons` con sus tres archivos. Pulsa **Commit changes** para guardarlos en `main`. No subas el ZIP como sustituto de estos archivos.
4. La carpeta `.github` puede estar oculta en tu equipo. Para añadir el flujo sin depender de verla, usa **Add file → Create new file**. En el nombre escribe `.github/workflows/pages.yml`. Pega el contenido de ese archivo incluido en el paquete y guarda con **Commit changes** en `main`.
5. Abre **Settings → Pages → Build and deployment → Source** y selecciona **GitHub Actions**.
6. Abre **Actions → Publicar juego en GitHub Pages → Run workflow**, selecciona `main` y pulsa **Run workflow**. Si Actions está deshabilitado, permite las acciones en **Settings → Actions → General**. Espera a que la ejecución termine en verde; si falla, abre el paso en rojo para ver la causa.
7. En **Settings → Pages** encontrarás el enlace publicado. Con el nombre actual del repositorio será `https://cesardaniel1979puebla-coder.github.io/juego-tablas-multiplicar/`. Esta dirección solo estará disponible después de una publicación correcta; no es una vista previa temporal. Conserva los nombres del propietario y del repositorio para mantenerla estable. Si aparece la opción **Enforce HTTPS**, actívala.

La configuración del flujo concede al token automático de GitHub solo lectura del repositorio y los permisos necesarios para Pages; no necesitas añadir secretos ni una tarjeta de pago.

### Instalar en Android

1. Abre el enlace HTTPS publicado en Chrome con internet.
2. Espera el mensaje **Listo para jugar sin internet**.
3. Toca **Instalar juego** si aparece, o abre el menú **⋮ → Instalar aplicación / Añadir a pantalla de inicio**. El texto puede variar según la versión de Chrome.
4. Abre el ícono instalado. Activa el modo avión y vuelve a abrirlo para comprobar el modo sin conexión.

El ZIP o un archivo `file://` no instala la PWA: primero publica los archivos por HTTPS. Los datos se guardan en ese navegador; borrar los datos del sitio elimina el progreso y la caché. El navegador también puede eliminar almacenamiento por falta de espacio.

### Actualizar el juego

Sube los cambios a `main` e incrementa `CACHE` en `sw.js` (por ejemplo, `saltos-app-v2`) si cambias archivos públicos. Pages los publicará automáticamente. Visita el juego con internet y cierra todas sus ventanas para que el nuevo service worker pueda activarse; al volver a abrirlo se usará la nueva versión. La actualización no borra el progreso.

### Verificación realizada

Se comprobaron las 80 multiplicaciones, opciones únicas, controles táctiles en tamaño móvil, reinicio y progreso guardado. La verificación PWA comprueba el manifiesto, los tamaños de los íconos, la activación del service worker y la reapertura sin red con progreso conservado en Chromium. La publicación HTTPS debe verificarse después de activar Pages; no se ha publicado desde este entorno porque su credencial de GitHub es inválida.
