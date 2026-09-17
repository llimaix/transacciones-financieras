# Casos de Prueba

> **Responsable:** Luis  
> **Tarea:** T-13  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-03 (Casos de uso — Astrid)

---

## Instrucciones

Por cada caso de uso se necesitan **al menos 3 escenarios**: normal, alterno y error.  
Usa los IDs de casos de uso definidos por Astrid en `docs/diagramas/casos-de-uso/casos-de-uso.md`.

---

## CU-02 — Realizar transferencia

### CP-01 · Transferencia exitosa (escenario normal)
| Campo              | Detalle                                                   |
|--------------------|-----------------------------------------------------------|
| **ID**             | CP-01                                                     |
| **Caso de uso**    | CU-02                                                     |
| **Precondición**   | Cuenta origen y destino existen. Saldo origen ≥ monto.    |
| **Entrada**        | Origen: C-001, Destino: C-002, Monto: Q500.00             |
| **Pasos**          | 1. Ingresar datos → 2. Confirmar → 3. Sistema procesa     |
| **Resultado esperado** | Saldo origen se reduce Q500. Saldo destino aumenta Q500. Transacción registrada como EXITOSA. |
| **Estado**         | ⬜ Pendiente                                              |

---

### CP-02 · Fondos insuficientes (escenario alterno)
| Campo              | Detalle                                                   |
|--------------------|-----------------------------------------------------------|
| **ID**             | CP-02                                                     |
| **Caso de uso**    | CU-02                                                     |
| **Precondición**   | Cuenta origen existe con saldo de Q100.00.                |
| **Entrada**        | Origen: C-001, Destino: C-002, Monto: Q500.00             |
| **Pasos**          | 1. Ingresar datos → 2. Confirmar → 3. Sistema valida fondos |
| **Resultado esperado** | Sistema rechaza la operación. Saldos sin cambios. Transacción registrada como RECHAZADA con motivo "Fondos insuficientes". |
| **Estado**         | ⬜ Pendiente                                              |

---

### CP-03 · Cuenta destino inexistente (escenario de error)
| Campo              | Detalle                                                   |
|--------------------|-----------------------------------------------------------|
| **ID**             | CP-03                                                     |
| **Caso de uso**    | CU-02                                                     |
| **Precondición**   | Cuenta origen existe. Cuenta destino no existe en el sistema. |
| **Entrada**        | Origen: C-001, Destino: C-999 (no existe), Monto: Q200.00 |
| **Pasos**          | 1. Ingresar datos → 2. Confirmar → 3. Sistema valida existencia |
| **Resultado esperado** | Sistema notifica "Cuenta destino no encontrada". Sin cambios en saldos. |
| **Estado**         | ⬜ Pendiente                                              |

---

### CP-04 · Transferencia duplicada (escenario de error)
| Campo              | Detalle                                                   |
|--------------------|-----------------------------------------------------------|
| **ID**             | CP-04                                                     |
| **Caso de uso**    | CU-02                                                     |
| **Precondición**   | Ya existe una transacción idéntica reciente (mismo origen, destino y monto en ventana de tiempo). |
| **Entrada**        | Mismos parámetros de una transacción ejecutada hace 30 segundos. |
| **Pasos**          | 1. Ingresar datos → 2. Confirmar → 3. Sistema detecta duplicado |
| **Resultado esperado** | Sistema rechaza la operación con mensaje "Operación duplicada detectada". |
| **Estado**         | ⬜ Pendiente                                              |

---

## CU-01 — Crear cuenta

### CP-05 · Creación exitosa (escenario normal)
> _(Completar con el mismo formato)_

### CP-06 · ID de cuenta duplicado (escenario de error)
> _(Completar con el mismo formato)_

---

## CU-03 — Consultar historial

### CP-07 · Consulta con resultados (escenario normal)
> _(Completar con el mismo formato)_

### CP-08 · Consulta sin transacciones (escenario alterno)
> _(Completar con el mismo formato)_

---

_Completa todos los casos de prueba pendientes y cambia el estado a ✅._
