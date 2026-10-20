# Alternativas Arquitectónicas Descartadas

> **Responsable:** Fabiola
> **Tarea:** T-05
> **Estado:** ✅ Completado
> **Depende de:** —

---

## 1. Propósito

El proyecto exige comparar la arquitectura elegida (Capas con núcleo de dominio transaccional sobre AWS) contra al menos dos estilos alternativos, justificando por qué fueron descartados para este problema y este alcance. El criterio de comparación principal es siempre el mismo: **cómo cada estilo garantiza la consistencia financiera (no perder ni crear dinero) bajo despliegue en AWS con integración on-premise vía VPN + API/SOAP**.

---

## 2. Alternativa 1 — Arquitectura de Microservicios

**Descripción breve:**
El sistema se dividiría en servicios independientes y desplegables por separado (por ejemplo: servicio de cuentas, servicio de transferencias, servicio de historial), cada uno con su propia base de datos, comunicándose por red.

**Ventajas para este problema:**
- Escalado independiente de cada servicio.
- Despliegues parciales sin afectar todo el sistema.
- Buen encaje natural con servicios gestionados de AWS.

**Desventajas / razones de descarte:**
- **Rompe la atomicidad del débito/crédito:** si "cuentas" y "transferencias" viven en bases de datos separadas, una transferencia deja de ser una transacción ACID única y exige **consistencia distribuida** (patrón Saga, compensaciones o two-phase commit).
- Eso introduce estados intermedios en los que el dinero puede quedar temporalmente "en el aire", justo el riesgo que el sistema debe eliminar (RNF-01, RB-07).
- La complejidad operativa (orquestación, mensajería, monitoreo distribuido) es desproporcionada para el alcance de la fase 1.
- **Razón específica de descarte:** garantizar que nunca exista un débito sin su crédito es mucho más simple y robusto con una única transacción ACID que coordinando compensaciones entre servicios.

---

## 3. Alternativa 2 — Arquitectura Hexagonal pura (Puertos y Adaptadores)

**Descripción breve:**
El dominio queda totalmente aislado en el centro y toda interacción externa (API, base de datos, integraciones) entra y sale por "puertos" implementados por "adaptadores". Es un estilo excelente para aislar la lógica de negocio de la tecnología.

**Ventajas para este problema:**
- Máximo aislamiento del dominio financiero respecto de la tecnología (gran mantenibilidad y testabilidad).
- Facilita sustituir adaptadores (por ejemplo, cambiar el mecanismo de integración on-premise) sin tocar el núcleo.

**Desventajas / razones de descarte:**
- Para el alcance de la fase 1, la ceremonia de definir puertos y adaptadores para cada interacción **añade complejidad conceptual** que no se traduce en beneficio proporcional.
- El equipo y la institución defienden con más facilidad un modelo en capas clásico, que es ampliamente conocido y suficiente para los requerimientos actuales.
- **Razón específica de descarte:** no se descarta por ser mala (de hecho es una evolución natural), sino por **sobredimensionada para esta fase**. La arquitectura elegida ya incorpora su mejor idea —aislar el dominio— mediante la **capa anticorrupción** para las integraciones on-premise, sin pagar el costo de hexagonalizar todo el sistema.

---

## 4. Conclusión comparativa

| Criterio | Capas + dominio transaccional (elegida) | Microservicios | Hexagonal pura |
|----------|------------------------------------------|----------------|----------------|
| Garantía de consistencia financiera | **Fuerte** (ACID única) | Débil (consistencia distribuida) | Fuerte |
| Complejidad operativa en AWS | Baja–media | Alta | Media–alta |
| Facilidad de defensa / comprensión | Alta | Media | Media |
| Encaje con el alcance de fase 1 | **Óptimo** | Sobredimensionado | Sobredimensionado |

La arquitectura en **Capas con núcleo de dominio transaccional** supera a ambas alternativas para este caso específico: garantiza la consistencia financiera con una transacción ACID única (la vía más robusta para proteger el dinero), mantiene baja la complejidad operativa en AWS y es fácil de justificar ante la institución. Además, incorpora la mejor virtud del estilo hexagonal —el aislamiento del dominio— de forma acotada, a través de la capa anticorrupción que gestiona la integración on-premise por VPN y API/SOAP.
