# Speech de exposición — Josue

### UX / Wireframes y Supuestos

> **Tiempo sugerido:** 3–4 minutos
> **Orden en la presentación:** 4.º (después de UML)

---

## Qué mostrar en pantalla
El prototipo HTML abierto en el navegador (navegable en vivo) y la lista de supuestos.

---

## Guion

**Apertura.**
"Gracias, Wuilli. Si Wuilli mostró cómo funciona por dentro, yo muestro cómo lo experimenta el usuario. Y empiezo con algo importante: los supuestos."

**Supuestos (por qué importan).**
"Documentamos los supuestos de forma obligatoria porque evitan prometer cosas que el cliente no ha confirmado. Por ejemplo: asumimos usuarios autenticados por rol, moneda en quetzales, montos con precisión decimal exacta, y que el volumen de transacciones se confirmará con el banco. Hacerlos explícitos protege al equipo y al cliente."

**Flujos UX.**
"Diseñamos los flujos de las operaciones principales. El más importante es el de una transferencia: iniciar sesión, llenar el formulario, confirmar los datos, y ver el resultado, sea comprobante de éxito o mensaje de error. También están el flujo de consulta de historial y el de creación de cuenta."

**Wireframes / prototipo (el momento de impacto).**
"En vez de dibujos estáticos, armamos un prototipo navegable. Aquí lo tienen —abrir el HTML— son las ocho pantallas: login, panel con el saldo, formulario de transferencia, confirmación, resultado exitoso con comprobante, resultado de error, historial y detalle."

**El detalle que conecta con el diseño.**
"Un punto fino: en el formulario, la referencia única de la transferencia la genera el sistema, no el usuario. Eso es a propósito: si el usuario pudiera editarla, se rompería la prevención de duplicados que explicó Astrid en las reglas de negocio. Y en la pantalla de error siempre decimos 'no se modificó ningún saldo', que es la consistencia hecha visible para el usuario."

**Transición a Luis.**
"Ya vimos requerimientos, arquitectura, modelo y experiencia. Luis cierra demostrando que todo esto se puede probar y que está conectado de punta a punta."

---

## Preguntas probables y cómo responder

- **¿Es un prototipo funcional?**
  "Es un prototipo visual de alta fidelidad para validar la experiencia, no la aplicación real. El proyecto evalúa diseño, no implementación de código."

- **¿Por qué el usuario no ingresa la referencia?**
  "Porque es la clave de la idempotencia. Si la pudiera manipular, podría provocar o evadir la detección de duplicados. Por eso la genera el sistema."

- **¿Por qué 'solicitud de turno' se volvió 'inicio de transferencia'?**
  "Reinterpretamos ese término del enunciado al contexto financiero y lo dejamos documentado como supuesto, para no desviarnos de lo que el cliente pidió."
