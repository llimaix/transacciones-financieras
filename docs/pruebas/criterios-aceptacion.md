# Criterios de Aceptación

> **Responsable:** Luis
> **Tarea:** T-14
> **Estado:** ✅ Completado
> **Depende de:** T-13 (Casos de prueba)

---

## 1. Propósito

Definir criterios **verificables** (no subjetivos) en formato **Dado / Cuando / Entonces** (Gherkin). Cada criterio se liga a un requerimiento funcional (RF) y a un caso de prueba (CP), de modo que su cumplimiento pueda comprobarse objetivamente.

---

## CA-01 · Transferencia exitosa
**RF:** RF-03, RF-06, RF-07 · **CP:** CP-01

```gherkin
Dado que la cuenta CTA-10001 tiene saldo de Q1,000.00
  Y la cuenta CTA-10025 existe y está habilitada
Cuando el usuario solicita transferir Q500.00 de CTA-10001 a CTA-10025
Entonces el saldo de CTA-10001 debe quedar en Q500.00
  Y el saldo de CTA-10025 debe aumentar en Q500.00
  Y debe registrarse una transacción con estado "EXITOSA"
  Y el usuario debe recibir un comprobante con referencia única
```

---

## CA-02 · Rechazo por fondos insuficientes
**RF:** RF-04 · **CP:** CP-02

```gherkin
Dado que la cuenta CTA-10001 tiene saldo de Q100.00
Cuando el usuario solicita transferir Q500.00 desde CTA-10001
Entonces la transferencia debe ser rechazada
  Y el saldo de CTA-10001 no debe modificarse
  Y debe registrarse una transacción con estado "RECHAZADA"
  Y el mensaje debe indicar "Fondos insuficientes"
```

---

## CA-03 · Rechazo por cuenta inexistente
**RF:** RF-04 · **CP:** CP-03

```gherkin
Dado que la cuenta CTA-99999 no existe en el sistema
Cuando el usuario intenta transferir a CTA-99999
Entonces la transferencia debe rechazarse antes de modificar cualquier saldo
  Y el sistema debe responder "Cuenta destino no encontrada"
  Y ningún saldo debe modificarse
```

---

## CA-04 · Prevención de duplicados
**RF:** RF-05 · **CP:** CP-04

```gherkin
Dado que se ejecutó una transferencia con la referencia REF-000457
Cuando se recibe nuevamente una solicitud con la misma referencia REF-000457
Entonces el sistema no debe ejecutar una segunda transferencia
  Y debe devolver el resultado original de la operación
  Y el mensaje debe indicar "Operación duplicada detectada"
  Y los saldos no deben modificarse
```

---

## CA-05 · Rechazo por monto inválido
**RF:** RF-04 · **CP:** CP-05

```gherkin
Dado que las cuentas CTA-10001 y CTA-10025 existen y están habilitadas
Cuando el usuario solicita transferir un monto de Q0.00 o negativo
Entonces la transferencia debe rechazarse antes de procesar
  Y el mensaje debe indicar "Monto inválido"
  Y ningún saldo debe modificarse
```

---

## CA-06 · Creación de cuenta con identificador único
**RF:** RF-01 · **CP:** CP-06

```gherkin
Dado que el administrador proporciona datos válidos para una nueva cuenta
  Y no existe otra cuenta con el mismo identificador
Cuando se solicita crear la cuenta
Entonces el sistema debe registrar la cuenta con un identificador único
  Y la cuenta debe quedar activa con saldo inicial de Q0.00
  Y el sistema debe confirmar la creación
```

---

## CA-07 · Rechazo de identificador duplicado
**RF:** RF-01 · **CP:** CP-07

```gherkin
Dado que ya existe la cuenta CTA-10025
Cuando se intenta crear otra cuenta con el identificador CTA-10025
Entonces la operación debe ser rechazada
  Y la cuenta original debe permanecer sin cambios
  Y el sistema debe indicar que el identificador ya existe
```

---

## CA-08 · Consulta de historial
**RF:** RF-08 · **CP:** CP-08

```gherkin
Dado que la cuenta CTA-10001 tiene 3 transacciones registradas
  Y el usuario tiene permisos de consulta
Cuando el usuario consulta el historial de CTA-10001
Entonces el sistema debe mostrar las 3 transacciones
  Y cada transacción debe incluir fecha, monto, cuenta destino y estado
  Y debe distinguir las operaciones EXITOSA de las RECHAZADA
```

---

## CA-09 · Consulta sin resultados
**RF:** RF-08 · **CP:** CP-09

```gherkin
Dado que la cuenta CTA-10044 no tiene transacciones en el período consultado
Cuando el usuario consulta su historial para ese período
Entonces el sistema debe mostrar un resultado vacío
  Y debe informar "Sin operaciones"
  Y no debe producirse ningún error
```

---

## Resumen de criterios

| Criterio | RF | Caso de prueba |
|----------|-----|----------------|
| CA-01 Transferencia exitosa | RF-03, RF-06, RF-07 | CP-01 |
| CA-02 Fondos insuficientes | RF-04 | CP-02 |
| CA-03 Cuenta inexistente | RF-04 | CP-03 |
| CA-04 Prevención de duplicados | RF-05 | CP-04 |
| CA-05 Monto inválido | RF-04 | CP-05 |
| CA-06 Creación de cuenta | RF-01 | CP-06 |
| CA-07 Identificador duplicado | RF-01 | CP-07 |
| CA-08 Consulta de historial | RF-08 | CP-08 |
| CA-09 Consulta sin resultados | RF-08 | CP-09 |
