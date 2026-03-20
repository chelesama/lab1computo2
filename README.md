# 🖤 Registro Emocional 

##  Descripción del proyecto

Esta aplicación fue desarrollada con Vue.js y tiene como objetivo permitir al usuario registrar cómo se siente durante el día, junto con la intensidad de esa emoción.

La idea nace de una problemática real: muchas veces las personas no identifican ni expresan lo que sienten, lo que puede provocar acumulación emocional. Esta app busca ser una forma sencilla y visual de llevar ese registro.

Además de guardar emociones, la aplicación también interpreta la intensidad y muestra mensajes de apoyo, haciendo la experiencia más humana y no solo funcional.

---

##  Tecnologías utilizadas

- Vue.js 3 (Composition API)
- HTML
- CSS
- JavaScript
- LocalStorage (para persistencia de datos)

---

##  Variables reactivas utilizadas

- `emocion`: almacena lo que el usuario escribe sobre cómo se siente.
- `intensidad`: representa el nivel de la emoción (de 1 a 10).
- `registros`: lista donde se guardan todos los registros emocionales.
- `error`: muestra mensajes de validación.
- `filtro`: permite filtrar los registros por nivel (Alta, Media, Baja).

---

## Evento utilizado

Se utilizó el evento `@click` en el botón "Guardar", el cual ejecuta la función que valida y registra la emoción del usuario.

También se utiliza en los botones de eliminación para borrar registros específicos.

---

##  Uso de `v-for`

La directiva `v-for` se utilizó para recorrer la lista de registros y mostrarlos dinámicamente en pantalla.

Esto permite que cada emoción ingresada se renderice automáticamente sin necesidad de actualizar la página.

---

##  Uso de `v-if`

Se utilizó `v-if` en diferentes situaciones:

- Para mostrar mensajes de error cuando el usuario no ingresa información.
- Para mostrar un mensaje cuando no existen registros.
- Para mostrar mensajes dinámicos de apoyo emocional.

Esto mejora la interacción y hace la aplicación más clara para el usuario.

---

## Validación de datos

La validación se realiza verificando que el campo de emoción no esté vacío antes de guardar un registro.

Si el usuario intenta guardar sin escribir nada, se muestra un mensaje de error y no se permite continuar.

La validación es importante porque evita datos inválidos y mejora la calidad de la información almacenada.

---

## Funcionalidades principales

- Registro de emociones con intensidad
- Interpretación de la intensidad (Alta, Media, Baja)
- Mensajes de apoyo dinámicos
- Eliminación de registros
- Filtro por tipo de intensidad
- Persistencia de datos con LocalStorage

---

##  Conclusión

Esta aplicación no solo cumple con los requisitos técnicos solicitados, sino que también busca aportar una pequeña herramienta de apoyo emocional.

Se intentó hacer una interfaz simple pero significativa, donde el usuario no solo ingrese datos, sino que también reciba una pequeña respuesta que haga la experiencia más cercana y humana.
