# Requerimientos No Funcionales

> **Responsable:** Astrid
> **Tarea:** T-02
> **Estado:** ✅ Completado
> **Depende de:** T-01

---

## 1. Propósito

Los requerimientos no funcionales (RNF) establecen **qué tan confiable, seguro, íntegro y eficiente** debe ser el sistema, más allá de las funciones que ejecuta. En un sistema financiero son determinantes: no basta con que una transferencia parezca funcionar, hay que demostrar que el dinero se conserva, que los errores se controlan y que las operaciones se pueden auditar.

> **Importante:** los criterios de aceptación aquí descritos son una **propuesta inicial**, no características ya demostradas. Los objetivos de rendimiento y disponibilidad (RNF-05, RNF-06) deberán validarse con la institución antes de aprobar el diseño definitivo.

---

## 2. Catálogo de requerimientos no funcionales

| Código | Atributo de calidad | Criterio propuesto de aceptación | Prioridad |
|--------|---------------------|----------------------------------|-----------|
| **RNF-01** | Consistencia financiera | En ninguna prueba se permitirá un débito sin su crédito correspondiente, ni un crédito sin su débito. El total de dinero del sistema no cambia por efecto de una transferencia. | Crítica |
| **RNF-02** | Confiabilidad | Ante fallos simulados durante una transferencia, los saldos permanecen consistentes y el resultado de la operación siempre puede determinarse (completada o rechazada, nunca ambiguo). | Crítica |
| **RNF-03** | Seguridad | Solo usuarios autenticados y autorizados pueden ejecutar las acciones correspondientes a sus permisos. | Alta |
| **RNF-04** | Integridad y trazabilidad | Cada operación tiene una referencia única y un registro consultable con su estado y datos relevantes. | Alta |
| **RNF-05** | Rendimiento | Definir con el cliente un tiempo máximo de respuesta y una carga de operaciones esperada; validar ambos mediante pruebas. *(Objetivo a acordar)* | Media |
| **RNF-06** | Disponibilidad | Acordar un objetivo de disponibilidad y un procedimiento de recuperación ante interrupciones. *(Objetivo a acordar)* | Media |
| **RNF-07** | Mantenibilidad | Las reglas de validación deben poder modificarse sin obligar a rediseñar todo el sistema. | Alta |
| **RNF-08** | Privacidad | El historial solo muestra información financiera a usuarios con permisos adecuados. | Alta |

---

## 3. Desarrollo de los atributos críticos

Los tres primeros RNF son los que sostienen la confianza en un sistema financiero y merecen desarrollo detallado.

### RNF-01 · Consistencia financiera (atomicidad)
El débito y el crédito forman una **transacción atómica**: ambos se confirman o ninguno se aplica (regla de negocio **RB-07**). Si falla cualquier paso tras el débito, el sistema revierte el cambio (*rollback*) y deja los saldos como estaban. El invariante es: *la suma total de saldos no se altera por una transferencia; solo se redistribuye*.

### RNF-02 · Confiabilidad (manejo de errores y resultado determinable)
Toda operación termina en un estado explícito y verificable (`COMPLETADA` o `RECHAZADA`), nunca en un estado ambiguo. Ante una interrupción, debe existir un procedimiento para determinar el resultado real antes de permitir un reintento, evitando dobles débitos. Esto se apoya en el registro trazable (**RB-06**) y la referencia única de solicitud (**RB-05**).

### RNF-03 · Seguridad (autenticación y autorización)
El acceso a funciones restringidas exige identificación previa. Las acciones se limitan según el rol del usuario: administrar cuentas, solicitar/procesar transferencias o consultar historial son permisos diferenciados. Los permisos definitivos se confirman con la institución.

---

## 4. Trazabilidad RNF → RF / Reglas de negocio

| RNF | Se apoya en RF | Reglas de negocio |
|-----|----------------|-------------------|
| RNF-01 Consistencia | RF-06 | RB-04, RB-07 |
| RNF-02 Confiabilidad | RF-05, RF-06, RF-09 | RB-05, RB-06, RB-07 |
| RNF-03 Seguridad | RF-02, RF-08 | — |
| RNF-04 Integridad y trazabilidad | RF-03, RF-07 | RB-01, RB-06 |
| RNF-05 Rendimiento | RF-06 | — |
| RNF-06 Disponibilidad | RF-09 | RB-07 |
| RNF-07 Mantenibilidad | RF-04 | — |
| RNF-08 Privacidad | RF-08 | RB-06 |

> RNF-07 (Mantenibilidad) es el atributo que justifica, en la fase de diseño arquitectónico, separar las reglas de validación en un módulo propio para poder modificarlas sin rediseñar el sistema completo.

---

## 5. Impacto para la administración / cliente

Estos requerimientos permiten **evaluar la propuesta con evidencias**:

- **Consistencia y confiabilidad** → el dinero se conserva incluso ante fallos.
- **Seguridad y privacidad** → solo quien debe, ve y opera lo que le corresponde.
- **Integridad y trazabilidad** → toda operación es auditable.
- **Mantenibilidad** → las reglas de negocio evolucionan sin reconstruir el sistema.

---

> Los objetivos de rendimiento (RNF-05) y disponibilidad (RNF-06) quedan pendientes de cuantificar con el cliente y se documentarán junto con los supuestos del sistema.
