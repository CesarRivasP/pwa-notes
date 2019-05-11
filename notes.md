## Tools

### Google Lighthouse
Es una herramienta que viene con chrome la cual nos permite realizar diagnosticos de una web app, centrandose en el performance y accesibilidad. Nos permite testear si nuestra app se considera una pwa o no, y sobre todo, que pasos se deben tomar para que lo sea.

Lighthouse requiere de las siguientes funcionalidades:
- Un serviceWorker (solo funciona en modo de producción)

### First meaningful paint o Primer Pintado Significativo
Es una métrica suministrada por el navegador, que indica cuanto tarda en segundos o fracciones, la representación (renderización) del contenido más significativo en el sitio.
Nota: está métrica actualmente solo está disponible en Google Chrome.

#### ¿Cómo bajar los tiempos del First Meaningful Paint o TTFMP de nuestra PWA?
- Server Side Rendering
  * create-react-app no lo posee, por lo que se pueden usar frameworks como Gatsby y Next.
  * Con el Server Side Rendering, en lugar de pasar por el proceso de renderizacion común en el que se hace la carga del lado del cliente, el servidor mismo carga y guarda en cache todo lo que necesita consumir en cuanto a datos, y nos retorna el html listo para consumir. Esto significa que no hay que hacer ningún tipo de request desde el cliente y la aplicación se retorna en un formato listo para leer. Esto baja muchísimo el First Meaningful Paint. Se puede ahorrar un 1 o 2 si se tiene un servidor bien configurado
- Menos HTML y CSS
  * Mientras menos html y css se tenga en la aplicación, mas rápido va a cargar-
- Servidores mas rápidos

### Time to Interactive
Nos indica en que momento esta interactiva la aplicación. Cuando nos referimos a Time to Interactive se esta buscando que:
- Se haya cargado React
- Se haya inicializado la aplicación
- Se puedan corren comandos en la aplicación

>El Time to Interactive tiene que ver mucho con el tamaño del framework que se este utilizando.

Por lo general, se intenta tener un Time to Interactive de menos de 5 segundos en Lighthouse con un teléfono medium con una conexión mala

### Implementar la funcionalidad de Add to Home Screen
Es una de las mejores funcionalidades si se quiere fidelizar aun mas a nuestros usuarios. Chrome, en Android por defecto, nos propone una vez que se cumplen todos los requisitos de Lighthouse la posibilidad de agregar la aplicacion a la HomeScreen.

#### configurando el manifest.json
- short_name es el nombre que se utiliza en el home screen
- start_url: esto nos dice en que pagina comienza nuestra app. Por temas de compatibilidad, conviene que siempre sea '/' en lugar de 'index.html'. Esto va a evitar algunos bugs particularmente en IOS
- display: "standalone" quiere decir que la app puede correr por si misma.
- theme_color: o color de combinación, tiene que ver con como se va a ver la aplicación, es decir, que colores se van a utilizar para que combine mas con nuestra app. Por ejemplo, la barra de tareas, la barra de la ventana, entre otros. En el theme-color ubicado en el index.html se le puede indicar el color a la barra de navegacion de chrome
- src: ruta del icono
- sizes: tamaño de la imagen. 512x512 es el tamaño ideal para los iconos, puesto que este permite ir desde un tamaño pequeño a uno muy grande. Se pueden expecificar varias resoluciones
- type: formato de la imagen
- Related-aplication: esto por defecto indica si se quiere que en el app to HomeScreen chrome recomiende una aplicación del store en lugar de la Progressive Web App. Por defecto, no es necesario.
- Scope: se pueden tener múltiples PWA por dominio, y esto esta definido por el scope. Por defecto la aplicación de prueba (recetas) funciona en el root del dominio, asi que no hace falta cambiar nada, y se le coloca una barra para indicar que cubra todo el dominio por defecto.

### ngrok
Nos permite testear las PWA sin necesidad de llevar la aplicación a producción.
NGROK nos permite hacer un tunel y tener un servidor https que dirige perfectamente a nuestra maquina, y de esta forma se puede testear instantaneamente una PWA con una conexión https.

Para que ngrok funcione correctamente se debe tener corriendo el servidor local en una terminal, y el ngrok en otra terminal, ambas apuntando al mismo puerto … ya que ngrok … hace las veces de proxy o similar.

### Service Worker
ES lo que permite que las PWA funcionen. Es un script que nuestro navegador corre detras de escena, que por defecto no tiene acceso a ninguna parte del brouser (no puede tocar el DOM directamente), para expone una pequeña api con la que nos podemos comunicar por ejemplo, en el caso de recibir notificaciones.
Tambien esto significa que los serviceWorkers se les puede dar mucho mas control de lo que pasa detrás de escena. Se puede tener control absoluto de lo que sucede a nivel red, esto quiere decir que podemos controlar como se maneja todas y cada una de las request que hace nuestro navegador, por ejemplo, manejar el cache de cada una, y decidir diferentes estrategias de red como lo pueden ser establecer que ciertas cosas deban ser cacheadas por adelantado y tener una suerte de proceso de instalación dentro de nuestra app. Esto nos permite mejorar la UX, ya que si se carga todo detras de escena los tiempos de recarga de nuestra app van a ser mejores.
Tambien se pueden utilizar cosas como push notifications, donde se puede dejar el navegador detrás de escena esperando que le envíen notificaciones como lo pueden ser los resultados de un partido de futbol en tiempo real.

### Notas:
#### Usar Gatsby o NextJS
- Por lo general Gatsby se recomienda para sitios estáticos y Next para apps dinámicas o más complejas, pero últimamente están teniendo paridad de features entre ambos, así que la elección se vuelve un poco más difícil.
Generalmente se usa Next.JS porque tiene mejor soporte, creo que es un poco más fácil de aprender y tampoco impone demasiadas restricciones de arquitectura, así que da más control en proyectos grandes. Lo hemos usado en proyectos desde blogs hasta apps gigantes y se comporta muy bien en todos los casos.

#### Versiones de Android
Según el sitio de estadísticas de la web: https://www.statista.com/

Al primer semestre de 2018, la distribución de versions de Android más usadas en base a los 2000 millones de usuarios a nivel global, según datos de Google en la I/O 2018, es la siguiente:

https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%20de%202018-07-20%2001-26-23-f6656d06-eb32-4ecd-b26e-a54e137ca4db.jpg

- Stack eficiente:
ReactJS + NextJS + PWA


#### ServiceWorkers
El que los ServiceWorkers sólo funcionen en modo de producción tiene que ver con que requieren de forma obligatoria estar alojados en sitios que usan sertificados SSL, es decir con protocolo https

Es por razones de confiabilidad y seguridad, ya que las PWAs pueden solicitar permisos que podrían poner en riesgo la privacidad de los usuarios, y Google previene para no ser responsable de ataques Man-in-the-middle, etc.
