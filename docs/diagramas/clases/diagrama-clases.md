# Diagrama de Clases

> **Responsable:** Wuilli  
> **Tarea:** T-08  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-06 (Diseño de componentes — Fabiola)

---

## Instrucciones

1. Revisar `docs/arquitectura/diseno-componentes.md` para conocer los componentes definidos por Fabiola.
2. Modelar las clases que implementan esos componentes.
3. Exportar el diagrama como imagen y agregarla a esta carpeta.

---

## Diagrama

> Insertar imagen aquí: `diagrama-clases.png`

---

## Clases esperadas (base mínima)

| Clase                   | Responsabilidad                                          | Componente |
|-------------------------|----------------------------------------------------------|------------|
| `Cuenta`                | Representa una cuenta bancaria con saldo e ID único      | C-0X       |
| `Transaccion`           | Registra los datos de cada operación realizada           | C-0X       |
| `TransferenciaService`  | Orquesta el proceso de transferencia entre cuentas       | C-0X       |
| `ValidadorFondos`       | Verifica disponibilidad de fondos antes de ejecutar      | C-0X       |
| `HistorialRepository`   | Almacena y consulta el registro de transacciones         | C-0X       |

> Asigna el componente correcto según lo que defina Fabiola en T-06.

---

## Atributos y métodos sugeridos

```
Cuenta
  - id: String
  - titular: String
  - saldo: Decimal
  - activa: Boolean
  + debitar(monto): void
  + acreditar(monto): void
  + getSaldo(): Decimal

Transaccion
  - id: String
  - cuentaOrigen: String
  - cuentaDestino: String
  - monto: Decimal
  - fecha: DateTime
  - estado: EstadoTransaccion  ← (EXITOSA, RECHAZADA, PENDIENTE)

TransferenciaService
  + ejecutarTransferencia(origen, destino, monto): Transaccion

ValidadorFondos
  + validarFondos(cuenta, monto): Boolean
  + validarExistencia(idCuenta): Boolean
  + esDuplicada(transaccion): Boolean

HistorialRepository
  + guardar(transaccion): void
  + consultarPorCuenta(idCuenta): List<Transaccion>
```

---

## Relaciones entre clases

| Relación                                    | Tipo          |
|---------------------------------------------|---------------|
| `TransferenciaService` usa `ValidadorFondos`| Dependencia   |
| `TransferenciaService` usa `Cuenta`         | Asociación    |
| `TransferenciaService` usa `HistorialRepository` | Dependencia |
| `Transaccion` referencia `Cuenta`           | Asociación    |

---

_Completa el diagrama con las clases reales según T-06 y cambia el estado a ✅._
