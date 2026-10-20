# Speech de exposición — Wuilli

### Modelado UML (Clases, Componentes y Secuencia)

> **Tiempo sugerido:** 3–4 minutos
> **Orden en la presentación:** 3.º (después de arquitectura)

---

## Qué mostrar en pantalla
Diagrama de clases, diagrama de componentes y los tres diagramas de secuencia.

---

## Guion

**Apertura.**
"Gracias, Fabiola. Mi parte es llevar los componentes que ella definió a modelos UML concretos, para que se vea exactamente cómo se estructura y cómo se comporta el sistema."

**Diagrama de componentes.**
"Este primer diagrama muestra los nueve componentes agrupados por capa y cómo se comunican. Se ve el flujo crítico de una transferencia: entra por la API, pasa al servicio de transferencias, que coordina la validación, el proceso atómico y el registro. A la derecha está el adaptador que conecta con los sistemas del banco por VPN."

**Diagrama de clases.**
"Aquí paso de componentes a clases. Las centrales son Cuenta, Transaccion, TransferenciaService, ValidadorFondos, ProcesadorTransaccion y los repositorios. Un punto clave: ProcesadorTransaccion es la única clase que modifica saldos. Eso es coherente con lo que explicó Fabiola: el control del dinero está en un solo lugar."

**Diagramas de secuencia (el corazón del comportamiento).**
"Hice tres diagramas de secuencia, uno por escenario. El primero es la transferencia exitosa: se valida, y el débito y el crédito ocurren dentro de una transacción ACID, marcada explícitamente. El segundo es el rechazo por fondos insuficientes: el sistema se detiene antes de tocar saldos. El tercero es la detección de duplicados: si llega una referencia ya procesada, el sistema devuelve el resultado original sin ejecutar de nuevo. Eso es la idempotencia en acción."

**Coherencia.**
"Todo lo que ven aquí usa los mismos nombres y los mismos IDs que los componentes de Fabiola y los requerimientos de Astrid. No hay nada suelto; cada elemento viene de una decisión previa."

**Transición a Josue.**
"Ya vimos cómo funciona por dentro. Josue muestra ahora cómo lo vive el usuario."

---

## Preguntas probables y cómo responder

- **¿Por qué las validaciones no son una clase que modifica datos?**
  "Separamos responsabilidades: ValidadorFondos solo decide si se puede; ProcesadorTransaccion ejecuta. Así cada clase tiene una sola razón para cambiar."

- **¿Qué muestra el `Note` de transacción ACID en el diagrama de secuencia?**
  "Marca el punto donde débito y crédito se hacen juntos. Si algo falla ahí, se revierte todo; es la garantía de consistencia a nivel de comportamiento."

- **¿Los diagramas son generados o diseñados?**
  "Diseñados por nosotros a partir de los componentes. Los tenemos en Mermaid dentro de la documentación y también exportados como imagen y en draw.io editable."
