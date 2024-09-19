# Preguntas Prueba Técnica

## 1) Habrás observado que las llamadas al servicio para obtener el listado de Municipios son bastante lentas. ¿Cómo haríamos para mejorar el tiempo de respuesta de este servicio?

Se podría implementar un sistema de caché para almacenar los resultados de las consultas a este servicio externo, de modo que las llamadas siguientes puedan devolver datos rápidamente sin necesidad de volver a consultar el servicio la llamada al servicio de la Aemet. Sería viable ya que en principio los nombres de los municipios y sus identificadores, a priori parece que no tengan que cambiar mucho. Si por el caso cambian frecuentemente, las políticas de expiración del caché tendrían que ser relativamente frecuentes.

Otra manera de hacerlo (habría que comprobar si mejora el resultado), sería creando un Job para obtener los municipios y almacenarlos en base de datos. Habría que mantener los resultados actualizados estableciendo un periodo de ejecución. Si se guardan en base de datos, también se podría configurar un sistema de caché.

---

## 2) Notarás además que el servicio para recuperar la predicción para un municipio devuelve una URL a la que hacer la consulta. ¿Por qué motivo piensas que AEMET ha implementado este servicio así?

Al proporcionar una URL, AEMET puede distribuir la carga entre diferentes instancias o servicios, lo que puede ayudar a manejar picos en la demanda sin afectar el rendimiento general. Además, este enfoque separa la lógica de la recuperación de datos de la presentación.

---

## 3) A nuestros usuarios les ha gustado la aplicación, pero les parece muy engorroso tener que indicar cada vez que acceden a la aplicación el municipio donde se encuentran para consultar la previsión del tiempo. Les gustaría que se recordará el último municipio seleccionado y que automáticamente les cargue la predicción del día siguiente. ¿Cómo lo podríamos hacer?

Una manera rápida y fácil de implementar sería guardarlo en la parte cliente (por ejemplo local storage).  
Otra manera sería almacenarlo en base de datos.

---

## 4) Tras la amenaza de AEMET con cortarnos el servicio, debemos apresurarnos a buscar alguna solución que afecte lo mínimo posible a nuestros usuarios. ¿Qué podríamos hacer? ¿Cómo implementarías la solución?
Una posibilidad sería obtener los datos del servicio de la Aemet y almacenarlos en base de datos. De esta manera se solicitarán 1 única vez al servicio independientemente de la cantidad de solicitudes que recibamos nosotros.
El proceso de obtención de datos deberá ser diario, ya que las predicciones son diarias.
