# Flujos UX

> **Responsable:** Josue
> **Tarea:** T-11
> **Estado:** ✅ Completado
> **Depende de:** T-03 (Casos de uso)

---

## 1. Propósito

Describir los flujos de interacción del usuario con el sistema para los casos de uso principales, desde el inicio de la operación hasta su resultado. Cada flujo corresponde a un caso de uso definido en el modelo (CU-01 a CU-04).

---

## 2. Flujo 1 — Inicio de transferencia (perspectiva del usuario · CU-02)

```mermaid
flowchart TD
    A([Inicio]) --> B[Iniciar sesión]
    B --> C[Panel principal]
    C --> D[Seleccionar 'Nueva transferencia']
    D --> E[Formulario: cuenta destino, monto, referencia]
    E --> F[Pantalla de confirmación de datos]
    F --> G{¿Confirma?}
    G -- No --> E
    G -- Sí --> H[Enviar solicitud al sistema]
    H --> I{Resultado}
    I -- Exitosa --> J[Mostrar comprobante]
    I -- Error --> K[Mostrar motivo y opciones]
    J --> L([Fin])
    K --> L
```

---

## 3. Flujo 2 — Procesamiento en el sistema (perspectiva del sistema · CU-02 / CU-03)

```mermaid
flowchart TD
    A([Recibir solicitud de transferencia]) --> B{¿Cuentas existen y habilitadas?}
    B -- No --> R1[Rechazar: cuenta inexistente/inhabilitada]
    B -- Sí --> C{¿Monto válido?}
    C -- No --> R2[Rechazar: monto inválido]
    C -- Sí --> D{¿Fondos suficientes?}
    D -- No --> R3[Rechazar: fondos insuficientes]
    D -- Sí --> E{¿Solicitud duplicada?}
    E -- Sí --> R4[Devolver resultado original · no re-ejecuta]
    E -- No --> F[Débito origen + Crédito destino · transacción ACID]
    F --> G[Registrar transacción EXITOSA]
    G --> H[Notificar al usuario]
    R1 --> X[Registrar RECHAZADA + notificar]
    R2 --> X
    R3 --> X
    H --> Z([Fin])
    R4 --> Z
    X --> Z
```

> Los escenarios de rechazo (R1–R4) corresponden a CU-03 y nunca modifican saldos.

---

## 4. Flujo 3 — Consulta de historial (CU-04)

```mermaid
flowchart TD
    A([Usuario selecciona 'Ver historial']) --> B[Indicar filtros: cuenta, período, estado]
    B --> C[Sistema verifica permisos]
    C --> D{¿Tiene permisos?}
    D -- No --> E[Mostrar acceso denegado]
    D -- Sí --> F{¿Hay resultados?}
    F -- No --> G[Mostrar 'Sin operaciones']
    F -- Sí --> H[Mostrar lista de transacciones]
    H --> I[Seleccionar una transacción]
    I --> J[Mostrar detalle y estado]
    E --> K([Fin])
    G --> K
    J --> K
```

---

## 5. Flujo 4 — Creación de cuenta (CU-01)

```mermaid
flowchart TD
    A([Administrador solicita crear cuenta]) --> B[Ingresar datos de la cuenta]
    B --> C{¿Datos obligatorios completos?}
    C -- No --> B
    C -- Sí --> D{¿Identificador ya existe?}
    D -- Sí --> E[Rechazar: identificador duplicado]
    D -- No --> F[Asignar ID único y registrar cuenta]
    F --> G[Confirmar creación]
    E --> H([Fin])
    G --> H
```

---

## 6. Correspondencia flujo → caso de uso

| Flujo | Caso de uso | Pantallas (wireframes) |
|-------|-------------|------------------------|
| Flujo 1 Inicio de transferencia | CU-02 | WF-01, WF-02, WF-03, WF-04, WF-05, WF-06 |
| Flujo 2 Procesamiento | CU-02 / CU-03 | (lógica interna, sin pantalla propia) |
| Flujo 3 Consulta de historial | CU-04 | WF-02, WF-07, WF-08 |
| Flujo 4 Creación de cuenta | CU-01 | (pantalla administrativa) |

> **Versión editable (draw.io):** `flujos-ux.drawio` (los cuatro flujos en páginas separadas).
