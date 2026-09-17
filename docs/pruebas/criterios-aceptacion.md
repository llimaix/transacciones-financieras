# Criterios de Aceptación

> **Responsable:** Luis  
> **Tarea:** T-14  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-13 (Casos de prueba)

---

## Instrucciones

Los criterios deben ser **verificables** (no subjetivos). Formato sugerido: **Dado / Cuando / Entonces** (Gherkin).  
Cada criterio debe estar ligado a un requerimiento funcional y a un caso de prueba.

---

## CA-01 · Transferencia exitosa
**RF:** RF-02.1, RF-02.2  
**Caso de prueba:** CP-01

```gherkin
Dado que la cuenta C-001 tiene saldo de Q1,000.00
  Y la cuenta C-002 existe en el sistema
Cuando el usuario solicita transferir Q500.00 de C-001 a C-002
Entonces el saldo de C-001 debe ser Q500.00
  Y el saldo de C-002 debe aumentar en Q500.00
  Y debe existir un registro de transacción con estado "EXITOSA"
  Y el usuario debe recibir confirmación con número de comprobante
```

---

## CA-02 · Rechazo por fondos insuficientes
**RF:** RF-03.2  
**Caso de prueba:** CP-02

```gherkin
Dado que la cuenta C-001 tiene saldo de Q100.00
Cuando el usuario solicita transferir Q500.00 desde C-001
Entonces la transferencia debe ser rechazada
  Y el saldo de C-001 no debe modificarse
  Y debe existir un registro de transacción con estado "RECHAZADA"
  Y el mensaje de error debe indicar "Fondos insuficientes"
```

---

## CA-03 · Rechazo por cuenta inexistente
**RF:** RF-03.1  
**Caso de prueba:** CP-03

```gherkin
Dado que la cuenta C-999 no existe en el sistema
Cuando el usuario intenta transferir a C-999
Entonces la transferencia debe ser rechazada antes de cualquier modificación
  Y el sistema debe responder con el mensaje "Cuenta destino no encontrada"
  Y ningún saldo debe modificarse
```

---

## CA-04 · Prevención de duplicados
**RF:** RF-03.3  
**Caso de prueba:** CP-04

```gherkin
Dado que se ejecutó una transferencia de C-001 a C-002 por Q200.00 hace 30 segundos
Cuando el usuario intenta realizar la misma transferencia nuevamente
Entonces el sistema debe rechazar la operación
  Y el mensaje debe indicar "Operación duplicada detectada"
  Y los saldos no deben modificarse
```

---

## CA-05 · Registro de historial
**RF:** RF-04.1  
**Caso de prueba:** CP-07

```gherkin
Dado que la cuenta C-001 ha realizado 3 transferencias
Cuando el usuario consulta el historial de C-001
Entonces el sistema debe mostrar las 3 transacciones
  Y cada transacción debe incluir: fecha, monto, cuenta destino y estado
```

---

## CA-06 · Creación de cuenta
**RF:** RF-01.1, RF-01.2  
**Caso de prueba:** CP-05

```gherkin
Dado que el usuario proporciona datos válidos para una nueva cuenta
Cuando se solicita crear la cuenta
Entonces el sistema debe asignar un ID único
  Y la cuenta debe quedar activa y con saldo inicial de Q0.00
  Y el sistema debe confirmar la creación exitosa
```

---

_Completa los criterios faltantes y cambia el estado a ✅._
