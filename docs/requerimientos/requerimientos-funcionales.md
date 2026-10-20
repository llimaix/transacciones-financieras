# Requerimientos Funcionales

> **Responsable:** Astrid
> **Tarea:** T-01
> **Estado:** ✅ Completado
> **Depende de:** —

---

## 1. Propósito

Este documento define, de manera concreta y **verificable**, las acciones que el Sistema de Transferencias Financieras debe permitir realizar. Expande la lista base del planteamiento del problema con el análisis de las deficiencias identificadas en el sistema actual: inconsistencias de saldos, falta de validación, operaciones duplicadas o incompletas, ausencia de registro y dificultad de auditoría.

Cada requerimiento se redacta de forma que pueda comprobarse mediante un caso de prueba, lo que habilita la trazabilidad obligatoria `Requerimiento → Caso de uso → Diseño → Prueba`.

---

## 2. Requerimientos funcionales

| Código | Requerimiento | Comportamiento esperado | Prioridad |
|--------|---------------|-------------------------|-----------|
| **RF-01** | Crear cuentas | Registrar una cuenta nueva y asignarle un identificador único. Si el identificador lo genera el sistema, debe garantizarse su unicidad. | Alta |
| **RF-02** | Consultar cuentas | Verificar si una cuenta existe y consultar sus datos autorizados, estado y saldo disponible. | Alta |
| **RF-03** | Solicitar transferencias | Permitir indicar cuenta de origen, cuenta de destino y monto a transferir, junto con una referencia única de solicitud. | Alta |
| **RF-04** | Validar transferencias | Comprobar existencia y habilitación de ambas cuentas, que sean distintas, que el monto sea válido (> 0) y que existan fondos suficientes en el origen. | Crítica |
| **RF-05** | Evitar duplicados | Identificar solicitudes repetidas por su referencia única y evitar que una misma operación se ejecute dos veces. | Crítica |
| **RF-06** | Procesar transferencias | Descontar el monto de la cuenta de origen y acreditarlo en la cuenta de destino como **una sola operación atómica**. | Crítica |
| **RF-07** | Registrar transacciones | Guardar referencia única, fecha, monto, cuentas involucradas y resultado de cada operación (completada o rechazada). | Alta |
| **RF-08** | Consultar historial | Permitir consultar transferencias anteriores según los permisos del usuario, con filtros por cuenta y período. | Media |
| **RF-09** | Gestionar errores | Informar el motivo por el que una operación fue rechazada o no pudo completarse, **sin dejar saldos inconsistentes**. | Crítica |

> **Nota de análisis:** los requerimientos RF-02, RF-05, RF-06 y RF-09 no estaban en la lista inicial del planteamiento. Se incorporan porque responden directamente a los errores identificados en el sistema actual (duplicados, operaciones incompletas, falta de trazabilidad y manejo de errores).

---

## 3. Reglas de negocio asociadas

Las reglas de negocio son la base que hace confiables las operaciones financieras. Cada regla respalda uno o más requerimientos funcionales.

| Código | Regla de negocio | RF relacionados |
|--------|------------------|-----------------|
| **RB-01** | **Identificación:** cada cuenta y cada transferencia tendrán una referencia única. | RF-01, RF-03, RF-07 |
| **RB-02** | **Fondos suficientes:** no se permitirá transferir un monto superior al saldo disponible. | RF-04 |
| **RB-03** | **Cuentas válidas:** origen y destino deben existir y estar habilitadas para operar. | RF-04 |
| **RB-04** | **Integridad financiera:** el monto debitado debe ser exactamente igual al monto acreditado. | RF-06 |
| **RB-05** | **Procesamiento único:** repetir una solicitud no genera una segunda transferencia; la referencia única reconoce los reintentos. | RF-05 |
| **RB-06** | **Registro trazable:** cada transferencia conserva su resultado, incluida la causa del rechazo cuando corresponda. | RF-07, RF-09 |
| **RB-07** | **Operación atómica:** débito y crédito se confirman juntos o se cancelan juntos; ante un error no queda modificación parcial. | RF-06, RF-09 |

Estas reglas tienen mayor peso que la apariencia de la aplicación: son las que protegen el dinero y la confiabilidad de la información.

---

## 4. Trazabilidad hacia casos de uso

Los requerimientos funcionales se verán ejercidos por los casos de uso del sistema:

| RF | Caso(s) de uso que lo ejercen |
|----|-------------------------------|
| RF-01 | CU-01 Crear una cuenta |
| RF-02 | CU-01, CU-02 (verificación previa) |
| RF-03, RF-04, RF-06 | CU-02 Realizar una transferencia |
| RF-04, RF-05, RF-09 | CU-03 Rechazar transferencia inválida o duplicada |
| RF-07 | CU-02, CU-03 (registro del resultado) |
| RF-08 | CU-04 Consultar el historial de transacciones |

---

## 5. Alcance y exclusiones

- **Dentro de alcance (fase 1):** crear cuentas, validar y procesar transferencias, registrar operaciones y consultar historial.
- **Fuera de alcance (fase 1):** integración con bancos externos, pasarelas de pago, servicios antifraude de terceros, cambio de divisas y migración de datos. Estos aspectos se abordarán en fases posteriores.
