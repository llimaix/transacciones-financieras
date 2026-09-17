# Casos de Uso

> **Responsable:** Astrid  
> **Tarea:** T-03  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-01 (Requerimientos funcionales)

---

## Actores del sistema

| Actor     | Descripción                                              |
|-----------|----------------------------------------------------------|
| Cliente   | Usuario que solicita y realiza transferencias            |
| Auditor   | Usuario que consulta el historial de transacciones       |
| Sistema   | Actor secundario que ejecuta validaciones automáticas    |

---

## Diagrama de casos de uso

> Insertar imagen del diagrama aquí (draw.io, Lucidchart, PlantUML, etc.)  
> Archivo sugerido: `diagrama-casos-de-uso.png` en esta misma carpeta.

---

## Listado de casos de uso

| ID    | Caso de uso                        | Actor principal | RF relacionado |
|-------|------------------------------------|-----------------|----------------|
| CU-01 | Crear cuenta                       | Cliente         | RF-01          |
| CU-02 | Realizar transferencia             | Cliente         | RF-02          |
| CU-03 | Consultar historial                | Cliente/Auditor | RF-04          |
| CU-04 | Validar fondos disponibles         | Sistema         | RF-03          |
| CU-05 | Detectar transferencia duplicada   | Sistema         | RF-03          |
| CU-06 | _(agregar más según análisis)_     |                 |                |

---

## Descripción expandida — CU-02: Realizar transferencia

**Actores:** Cliente, Sistema  
**Precondiciones:** El cliente debe tener una cuenta activa con fondos suficientes.  
**Postcondiciones:** Los saldos de ambas cuentas se actualizan y la transacción queda registrada.

### Flujo normal
1. El cliente ingresa los datos de la transferencia (cuenta origen, destino, monto).
2. El sistema valida que ambas cuentas existen.
3. El sistema valida que hay fondos suficientes en la cuenta origen.
4. El sistema verifica que no es una operación duplicada.
5. El sistema ejecuta la transferencia (debita origen, acredita destino).
6. El sistema registra la transacción con estado "exitosa".
7. El sistema notifica al cliente el resultado.

### Flujo alterno — fondos insuficientes
- En el paso 3, si los fondos son insuficientes:
  - El sistema registra el intento con estado "rechazada".
  - El sistema notifica al cliente el motivo del rechazo.
  - El flujo termina sin modificar saldos.

### Flujo de error — cuenta destino inexistente
- En el paso 2, si la cuenta destino no existe:
  - El sistema notifica al cliente que la cuenta no fue encontrada.
  - El flujo termina sin modificar nada.

---

## Descripción expandida — CU-01: Crear cuenta

> _(Completar con el mismo formato: flujo normal, alterno y de error)_

---

## Descripción expandida — CU-03: Consultar historial

> _(Completar con el mismo formato: flujo normal, alterno y de error)_

---

## Descripción expandida — CU-04 y CU-05

> _(Completar según análisis del equipo)_

---

_Cambia el estado a ✅ cuando termines._
