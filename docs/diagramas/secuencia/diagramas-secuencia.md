# Diagramas de Secuencia

> **Responsable:** Wuilli  
> **Tarea:** T-09  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-03 (Casos de uso — Astrid)

---

## Instrucciones

Crear un diagrama de secuencia por flujo. Cada diagrama debe mostrar la interacción temporal entre actores y componentes del sistema. Exportar cada diagrama como imagen en esta carpeta.

---

## Diagrama 1 — Transferencia exitosa

> Insertar imagen: `secuencia-transferencia-exitosa.png`

**Participantes:** Cliente, TransferenciaService, ValidadorFondos, Cuenta (origen), Cuenta (destino), HistorialRepository

**Secuencia resumida:**
```
Cliente → TransferenciaService : ejecutarTransferencia(origen, destino, monto)
TransferenciaService → ValidadorFondos : validarExistencia(origen)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : validarExistencia(destino)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : validarFondos(origen, monto)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : esDuplicada(transaccion)
ValidadorFondos → TransferenciaService : false
TransferenciaService → Cuenta(origen) : debitar(monto)
TransferenciaService → Cuenta(destino) : acreditar(monto)
TransferenciaService → HistorialRepository : guardar(transaccion EXITOSA)
TransferenciaService → Cliente : transaccion exitosa
```

---

## Diagrama 2 — Transferencia fallida (fondos insuficientes)

> Insertar imagen: `secuencia-fondos-insuficientes.png`

**Secuencia resumida:**
```
Cliente → TransferenciaService : ejecutarTransferencia(origen, destino, monto)
TransferenciaService → ValidadorFondos : validarExistencia(origen)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : validarFondos(origen, monto)
ValidadorFondos → TransferenciaService : false  ← fondos insuficientes
TransferenciaService → HistorialRepository : guardar(transaccion RECHAZADA)
TransferenciaService → Cliente : error - fondos insuficientes
```

---

## Diagrama 3 — Transferencia duplicada detectada

> Insertar imagen: `secuencia-duplicada.png`

**Secuencia resumida:**
```
Cliente → TransferenciaService : ejecutarTransferencia(origen, destino, monto)
TransferenciaService → ValidadorFondos : validarExistencia(origen)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : validarFondos(origen, monto)
ValidadorFondos → TransferenciaService : true
TransferenciaService → ValidadorFondos : esDuplicada(transaccion)
ValidadorFondos → TransferenciaService : true  ← duplicada detectada
TransferenciaService → HistorialRepository : guardar(transaccion RECHAZADA - duplicada)
TransferenciaService → Cliente : error - operación duplicada
```

---

_Genera los diagramas visuales, agrega las imágenes y cambia el estado a ✅._
