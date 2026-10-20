# Speech de exposición — Astrid

### Requerimientos y Casos de Uso

> **Tiempo sugerido:** 3–4 minutos
> **Orden en la presentación:** 1.º (abre el contenido técnico)

---

## Qué mostrar en pantalla
Documento de requerimientos funcionales, no funcionales y el diagrama de casos de uso.

---

## Guion

**Apertura (contexto del problema).**
"Buenos días. Antes de hablar de soluciones, quiero mostrarles que entendimos bien su problema. Su institución necesita modernizar las transferencias entre cuentas porque hoy enfrenta inconsistencias en saldos, operaciones duplicadas o incompletas y poca trazabilidad. Mi parte del trabajo fue traducir esa necesidad en requerimientos claros y verificables, para que cada cosa que prometemos se pueda comprobar."

**Requerimientos funcionales.**
"La lista base del enunciado no era exhaustiva, así que la analizamos y la ampliamos a nueve requerimientos funcionales, de RF-01 a RF-09. Los agrupamos en cuatro áreas: gestión de cuentas, transferencias, validaciones e historial. Lo importante no es la cantidad, sino que cada requerimiento está redactado para poder comprobarse con una prueba más adelante."

**Reglas de negocio (el punto fuerte).**
"Detrás de los requerimientos definimos siete reglas de negocio, de RB-01 a RB-07. Las dos más importantes son la RB-07, operación atómica —el débito y el crédito se confirman juntos o no se hace ninguno—, y la RB-05, procesamiento único, que evita que una misma transferencia se ejecute dos veces. Estas reglas son las que protegen el dinero."

**Requerimientos no funcionales.**
"Definimos ocho requerimientos no funcionales. El crítico es RNF-01, consistencia financiera: el sistema nunca puede crear ni destruir dinero. Los de rendimiento y disponibilidad los dejamos como objetivos a acordar con el cliente, en vez de inventar cifras que no podemos sostener."

**Casos de uso.**
"Todo esto se traduce en cuatro casos de uso: crear cuenta, realizar transferencia, rechazar transferencia inválida o duplicada, y consultar historial. Un detalle de modelado: las validaciones internas no las pusimos como casos de uso sueltos, sino como pasos incluidos dentro de la transferencia, que es lo correcto en UML."

**Transición a Fabiola.**
"Con los requerimientos definidos, Fabiola explica cómo decidimos la arquitectura que los sostiene."

---

## Preguntas probables y cómo responder

- **¿Por qué agregaron requerimientos que no estaban en el enunciado?**
  "Porque el enunciado lo pedía explícitamente: la lista no era exhaustiva. Agregamos los que responden a los errores del sistema actual, como evitar duplicados y gestionar errores."

- **¿Cómo garantizan que un requerimiento es verificable?**
  "Cada uno tiene un caso de prueba y un criterio de aceptación asociados. Eso lo mostrará Luis en la matriz de trazabilidad."

- **¿Por qué no definieron tiempos de respuesta exactos?**
  "Preferimos acordarlos con ustedes a partir de su volumen real de operaciones. Dejarlos como un objetivo a validar nos permite comprometernos con una cifra que luego podamos cumplir, en lugar de prometer un número a ciegas. Es una decisión pensada para darles certeza."
