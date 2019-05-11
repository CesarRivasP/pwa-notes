## Tools

### Google Lighthouse
Es una herramienta que viene con chrome la cual nos permite realizar diagnosticos de una web app, centrandose en el performance y accesibilidad. Nos permite testear si nuestra app se considera una pwa o no, y sobre todo, que pasos se deben tomar para que lo sea

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

Por lo general, se intenta tener un Time to Interactive de menos de 5 segundos en Lighthouse con un telefono medium con una conexión mala

### Activar la funcionalidad de Add to Home Screen

### Notas:
#### Usar Gatsby o NextJS
- Por lo general Gatsby se recomienda para sitios estáticos y Next para apps dinámicas o más complejas, pero últimamente están teniendo paridad de features entre ambos, así que la elección se vuelve un poco más difícil.
Generalmente se usa Next.JS porque tiene mejor soporte, creo que es un poco más fácil de aprender y tampoco impone demasiadas restricciones de arquitectura, así que da más control en proyectos grandes. Lo hemos usado en proyectos desde blogs hasta apps gigantes y se comporta muy bien en todos los casos.

#### Versiones de Android
Según el sitio de estadísticas de la web: https://www.statista.com/

Al primer semestre de 2018, la distribución de versions de Android más usadas en base a los 2000 millones de usuarios a nivel global, según datos de Google en la I/O 2018, es la siguiente:

https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%20de%202018-07-20%2001-26-23-f6656d06-eb32-4ecd-b26e-a54e137ca4db.jpg

- Stack eficiente:
ReactJS + NextJS + PWA …
