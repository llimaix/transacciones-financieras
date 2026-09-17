# Matriz de Trazabilidad

> **Responsable:** Luis  
> **Tarea:** T-15  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-01, T-03, T-06, T-08, T-13, T-14

---

## Instrucciones

Este documento conecta cada requerimiento con su caso de uso, componente/clase de diseño y caso de prueba.  
Es el **artefacto integrador** del proyecto. Requiere que todos los integrantes hayan completado sus tareas.

**Luis debe coordinar con cada integrante los IDs finales antes de completar esta matriz.**

---

## Matriz

| Requerimiento | Descripción                             | Caso de uso | Componente | Clase de diseño        | Caso de prueba | Criterio aceptación |
|---------------|-----------------------------------------|-------------|------------|------------------------|----------------|---------------------|
| RF-01.1       | Crear cuentas                           | CU-01       | C-0X       | `Cuenta`               | CP-05          | CA-06               |
| RF-01.2       | ID único por cuenta                     | CU-01       | C-0X       | `Cuenta`               | CP-06          | CA-06               |
| RF-02.1       | Transferir fondos entre cuentas         | CU-02       | C-0X       | `TransferenciaService` | CP-01          | CA-01               |
| RF-02.2       | Registrar cada transacción              | CU-02       | C-0X       | `HistorialRepository`  | CP-01          | CA-01               |
| RF-03.1       | Validar existencia de cuentas           | CU-02       | C-0X       | `ValidadorFondos`      | CP-03          | CA-03               |
| RF-03.2       | Validar disponibilidad de fondos        | CU-02       | C-0X       | `ValidadorFondos`      | CP-02          | CA-02               |
| RF-03.3       | Evitar duplicidad de operaciones        | CU-02       | C-0X       | `ValidadorFondos`      | CP-04          | CA-04               |
| RF-04.1       | Consultar historial de transacciones    | CU-03       | C-0X       | `HistorialRepository`  | CP-07          | CA-05               |

> **Nota:** Reemplaza todos los `C-0X` con los IDs reales que Fabiola defina en `diseno-componentes.md`.  
> Agrega las filas que falten según los RF adicionales que identifique Astrid.

---

## Estado de insumos para esta matriz

| Artefacto                        | Responsable | Estado      |
|----------------------------------|-------------|-------------|
| Requerimientos funcionales (IDs) | Astrid      | ⬜ Pendiente |
| Casos de uso (IDs)               | Astrid      | ⬜ Pendiente |
| Componentes (IDs)                | Fabiola     | ⬜ Pendiente |
| Clases de diseño                 | Wuilli      | ⬜ Pendiente |
| Casos de prueba (IDs)            | Luis        | ⬜ Pendiente |
| Criterios de aceptación (IDs)    | Luis        | ⬜ Pendiente |

---

_Actualiza la matriz con los IDs reales cuando todos hayan completado sus tareas. Cambia el estado a ✅ al finalizar._
