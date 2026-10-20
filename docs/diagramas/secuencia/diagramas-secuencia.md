# Diagramas de Secuencia

> **Responsable:** Wuilli
> **Tarea:** T-09
> **Estado:** ✅ Completado
> **Depende de:** T-03 (Casos de uso)

---

## 1. Propósito

Mostrar la interacción temporal entre el actor y los componentes/clases del sistema para los flujos principales de la transferencia. Los participantes corresponden a las clases del diagrama de clases y a los componentes C-01..C-09.

---

## 2. Diagrama 1 — Transferencia exitosa

```mermaid
sequenceDiagram
    actor Operador
    participant API as C-01 API
    participant TS as C-02 TransferenciaService
    participant V as C-05 ValidadorFondos
    participant P as C-06 ProcesadorTransaccion
    participant CR as C-07 CuentaRepository
    participant HR as C-08 HistorialRepository

    Operador->>API: transferir(origen, destino, monto, ref)
    API->>TS: ejecutarTransferencia(solicitud)
    TS->>V: validarExistencia(origen, destino)
    V->>CR: obtener(origen), obtener(destino)
    CR-->>V: cuentas
    V-->>TS: válidas
    TS->>V: validarFondos(origen, monto)
    V-->>TS: fondos suficientes
    TS->>V: esDuplicada(ref)
    V->>HR: existeReferencia(ref)
    HR-->>V: no existe
    V-->>TS: no es duplicada
    TS->>P: procesar(origen, destino, monto)
    Note over P,CR: Transacción ACID (débito + crédito)
    P->>CR: debitar(origen, monto)
    P->>CR: acreditar(destino, monto)
    CR-->>P: saldos actualizados
    P-->>TS: Transaccion EXITOSA
    TS->>HR: guardar(Transaccion EXITOSA)
    TS-->>API: resultado exitoso
    API-->>Operador: comprobante
```

---

## 3. Diagrama 2 — Transferencia rechazada (fondos insuficientes)

```mermaid
sequenceDiagram
    actor Operador
    participant API as C-01 API
    participant TS as C-02 TransferenciaService
    participant V as C-05 ValidadorFondos
    participant CR as C-07 CuentaRepository
    participant HR as C-08 HistorialRepository

    Operador->>API: transferir(origen, destino, monto, ref)
    API->>TS: ejecutarTransferencia(solicitud)
    TS->>V: validarExistencia(origen, destino)
    V->>CR: obtener(origen), obtener(destino)
    CR-->>V: cuentas
    V-->>TS: válidas
    TS->>V: validarFondos(origen, monto)
    V->>CR: obtener(origen).getSaldo()
    CR-->>V: saldo < monto
    V-->>TS: fondos insuficientes
    Note over TS: No se modifica ningún saldo
    TS->>HR: guardar(Transaccion RECHAZADA - "Fondos insuficientes")
    TS-->>API: error: fondos insuficientes
    API-->>Operador: motivo del rechazo
```

---

## 4. Diagrama 3 — Transferencia duplicada detectada

```mermaid
sequenceDiagram
    actor Operador
    participant API as C-01 API
    participant TS as C-02 TransferenciaService
    participant V as C-05 ValidadorFondos
    participant HR as C-08 HistorialRepository

    Operador->>API: transferir(origen, destino, monto, ref)
    API->>TS: ejecutarTransferencia(solicitud)
    TS->>V: esDuplicada(ref)
    V->>HR: existeReferencia(ref)
    HR-->>V: ya existe
    V-->>TS: es duplicada
    Note over TS: Idempotencia (RB-05): no se ejecuta de nuevo
    TS->>HR: buscar(ref)
    HR-->>TS: resultado original
    TS-->>API: devuelve resultado original (sin re-ejecutar)
    API-->>Operador: "Operación duplicada detectada"
```

> **Versión editable (draw.io):** `diagramas-secuencia.drawio` (contiene los tres diagramas en páginas separadas).

---

## 5. Observaciones

- En el flujo exitoso, el débito y el crédito ocurren **dentro de una transacción ACID** gestionada por `ProcesadorTransaccion` (C-06); si cualquiera falla, se revierte todo (RNF-01, RB-07).
- En los flujos de rechazo, **ningún saldo se modifica**: el sistema valida antes de procesar.
- La detección de duplicados aplica **idempotencia por referencia única** (RB-05): una solicitud repetida devuelve el resultado original sin generar un segundo movimiento.
