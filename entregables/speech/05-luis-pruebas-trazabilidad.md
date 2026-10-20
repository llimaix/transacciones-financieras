# Speech de exposición — Luis

### Pruebas y Trazabilidad

> **Tiempo sugerido:** 4–5 minutos
> **Orden en la presentación:** 5.º (cierre del contenido técnico)

---

## Qué mostrar en pantalla
Casos de prueba (con los diagramas de flujo), criterios de aceptación y la matriz de trazabilidad con sus vistas gráficas.

---

## Guion

**Apertura.**
"Gracias, Josue. Yo cierro, y mi parte es la que amarra todo: demostrar que el diseño se puede probar y que cada pieza está conectada con las demás."

**Casos de prueba.**
"Definimos nueve casos de prueba cubriendo los tres tipos de escenario que pide el proyecto: normal, alterno y de error. Por ejemplo, para la transferencia: el caso feliz, el rechazo por fondos insuficientes, la cuenta inexistente, el duplicado y el monto inválido. Cada caso tiene su historia, sus pasos y un diagrama de flujo que muestra el camino de decisión."

**Criterios de aceptación.**
"Cada prueba tiene un criterio de aceptación verificable, escrito en formato Dado-Cuando-Entonces. No son subjetivos: dicen exactamente qué debe pasar. Por ejemplo, 'dado que la cuenta tiene saldo de cien y se piden quinientos, entonces la operación se rechaza y ningún saldo se modifica'. Eso se puede comprobar sin ambigüedad."

**Matriz de trazabilidad (el artefacto estrella).**
"Y esto es lo que integra todo el proyecto: la matriz de trazabilidad. El enunciado pide una cadena obligatoria: requerimiento, caso de uso, diseño, prueba. Aquí está completa. Cada uno de los nueve requerimientos se conecta con su caso de uso, su componente, su clase, su caso de prueba y su criterio de aceptación."

**La vista gráfica (remate).**
"Además de la tabla, lo pusimos como diagrama. Se puede seguir cualquier línea de izquierda a derecha y ver la cadena entera sin saltos. Esto demuestra algo clave que pide el proyecto: coherencia entre artefactos. No hay ningún elemento huérfano; todo lo que diseñamos responde a un requerimiento y todo requerimiento se prueba."

**Cierre del equipo.**
"En resumen: partimos de un problema real, lo convertimos en requerimientos verificables, elegimos una arquitectura justificada, la modelamos, la diseñamos para el usuario y la dejamos probada y trazada de punta a punta. El sistema protege el dinero por diseño, no por casualidad. Gracias."

---

## Preguntas probables y cómo responder

- **¿Cómo garantizan que no falta ningún requerimiento por probar?**
  "Por la matriz: verificamos que los nueve RF tengan al menos un caso de prueba y un criterio. No hay requerimiento sin prueba ni prueba sin requerimiento."

- **¿Qué es la idempotencia y dónde se prueba?**
  "Es que repetir una solicitud no genera un segundo movimiento. Se prueba en el caso CP-04: se reenvía una referencia ya usada y el sistema devuelve el resultado original sin volver a transferir."

- **¿Por qué la trazabilidad es tan importante para nosotros como cliente?**
  "Porque les da garantía y control. La matriz demuestra que cada necesidad que ustedes plantearon está diseñada y probada, sin cabos sueltos. Y si mañana piden un cambio, pueden ver de inmediato qué partes del sistema se ven afectadas. Es transparencia y mantenibilidad a futuro."
