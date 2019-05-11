
## Service Worker
ES lo que permite que las PWA funcionen. Son scripts que corren en el nuestro navegador detras de escena, que por defecto no tiene acceso a ninguna parte del brouser (no puede tocar el DOM directamente), para expone una pequeña api con la que nos podemos comunicar por ejemplo, en el caso de recibir notificaciones.
También esto significa que los serviceWorkers se les puede dar mucho mas control de lo que pasa detrás de escena. Se puede tener control absoluto de lo que sucede a nivel red, esto quiere decir que podemos controlar como se maneja todas y cada una de las request que hace nuestro navegador, por ejemplo, manejar el cache de cada una, y decidir diferentes estrategias de red como lo pueden ser establecer que ciertas cosas deban ser cacheadas por adelantado y tener una suerte de proceso de instalación dentro de nuestra app. Esto nos permite mejorar la UX, ya que si se carga todo detrás de escena los tiempos de recarga de nuestra app van a ser mejores.

- También se pueden utilizar cosas como push notifications, donde se puede dejar el navegador detrás de escena esperando que le envíen notificaciones como lo pueden ser los resultados de un partido de fútbol en tiempo real.

- Los Service Workers idealmente solo funcionan en modo de producción y no en desarrollo porque estos empiezan a modificar las estrategias de red que utilizabamos y empieza a guardar en cache ciertas cosas, eso es exactamente lo que no se quiere cuando estamos desarrollando, puesto que se están corrigiendo bugs y puede que esos bugs se almacenen en cache y terminemos corrigiendo errores guardados en cache y no propios del programa.

- Al trabajar con Service Workers es bueno dirigirse a la pestaña de application de chrome devtools, ir a clear storage y poner clear side data. Esto va a desinstalar todo lo que es cache y sobre todo va a limpiar los service Workers. (Esto es una fuente de bugs constante a la hora del desarrollo)

- El Service Workers de create-react-app se llama “SW Precache“, y este lo que hace es pre-cargar y dejar disponibles offline todos los archivos necesarios para correr nuestra aplicación, que son main.css, main.js, index y otras cosa mas como el service worker. La tuerca que algunos archivos tienen al inicio de su nombre indica que estos fueron cargados por el Service Worker.
  * SW Precache solo carga los assets de la aplicación
  * Una recomendación a la hora de hacer debugging es refrescar el sitio pues un service worker por lo general se inicializa después de la primera carga.

ADVERTENCIA:
Nunca conviene escribir nuestro propio ServiceWorker, especialmente con herramientas de bajo nivel. Esto no tiene que ver con un tema de confianza, sino con cómo funciona un SW y sobre todo lo qué un SW tiene control
Una vez que el ServiceWorker se instala en el cliente, el sitio queda fuertemente cacheado cómo está y es muy difícil corregir bugs en este contexto.

RECOMENDACIÓN:
Siempre conviene confiar o utilizar alguna herramienta que esté muy testeada y probada, y que tenga buenas herramientas de testing. Y … NO intentar crear nuestros propios Service Workers


## Workbox
Workbox es una librería hecha por Google para crear ServiceWorkers, y tiene una API fácil de usar. Esta nos va a permitir tener un control muy especifico de como funciona nuestra aplicación a nivel de red. Se va a poder elegir exactamente que sucede con cada asset, que se precarga, y que no se pre-carga, como se guarda en cache, entre otras cosas.
Tambien funciona google analytics offline. Google analytics requiere de una conexión de red para funcionar, pero con Workbox
esto se permite cachear offline. Entonces si nuestros usuarios están en una situación con mala conectividad, analytics va a guardar los eventos en una base de datos interna y en cuanto recobremos conexión los va a enviar nuevamente a los servidores de analytics para que podamos ver que estuvieron haciendo

Hay un pequeño detalle al momento de implementar Workbox en nuestro proyecto y es que estamos yendo en contra de los principios de Create React App y esto solo significa una cosa “eject”, esto nos llenaría de archivos que no nos sirven. Para evitar hacer eject vamos a instalar react-app-rewired y el plugin para webpack de workbox.

#### react-app-rewired
Esta nos va a permitir modificar el comportamiento de create-react-app sin tener que ejectar. Esto nos permite sumar plugins como el plugin para hacer el rewired de workbox. Esto nos va a permitir reemplazar el service worker que nos da Create react app por workbox, que nos va a dar todo el control a nosotros para empezar a modificar la estructura de red

> npm add workbox-webpack-plugin react-app-rewire-workbox react-app-rewired

- Se debe tomar en cuenta:
* Cuando se hace un rewired de create react app se debe crear un archivo que se llame config-overrides que nos va a permitir modificar la configuración interna de lo que seria el proceso de build. Este archivo tiene la configuración mínima y necesaria para que funcione el service worker custom nuestro
