# Supuestos del Sistema

> **Responsable:** Josue
> **Tarea:** T-10
> **Estado:** ✅ Completado
> **Depende de:** —

---

## 1. Propósito

Documentar los supuestos bajo los que se diseña el sistema. Hacerlos explícitos evita que el equipo prometa funcionalidades o condiciones que el cliente todavía no ha confirmado, y delimita con claridad el alcance aprobado. **Todos los supuestos deberán validarse con la institución antes de aprobar el diseño definitivo.**

---

## 2. Usuarios y permisos

- Existirán usuarios autorizados para administrar cuentas y usuarios autorizados para solicitar o procesar transferencias, según los permisos que defina la institución.
- Cada usuario deberá identificarse antes de acceder a las funciones restringidas.
- Los permisos definitivos (quién crea cuentas, quién autoriza transferencias, quién consulta) serán confirmados con el cliente.

## 3. Contexto de uso

- El sistema se utilizará dentro de las operaciones de una institución financiera.
- Las transferencias se realizarán entre cuentas registradas en el sistema y contempladas dentro del alcance aprobado.
- Se asume que la institución dispone de reglas para determinar cuándo una cuenta puede operar (habilitada/inhabilitada).
- El despliegue se realizará en la nube (AWS); la integración con sistemas internos on-premise se hará mediante VPN sitio a sitio y servicios API/SOAP.

## 4. Número de agentes y usuarios

- La cantidad de usuarios administrativos, operadores y usuarios concurrentes está **pendiente de confirmación** con la institución.
- El diseño debe considerar el volumen de operaciones esperado y evitar que dos solicitudes simultáneas produzcan saldos incorrectos (control de concurrencia).

## 5. Condiciones de operación

- Los montos se manejarán con **precisión monetaria exacta** (tipo decimal, nunca punto flotante binario); la moneda aplicable deberá definirse con el cliente (se asume quetzales como moneda inicial).
- Cada cuenta tendrá un identificador único y cada solicitud de transferencia tendrá una referencia única que permita reconocer reintentos.
- El sistema protegerá la integridad de los saldos ante errores, interrupciones o solicitudes duplicadas.
- Se asume que las cuentas y sus saldos iniciales serán registrados o cargados mediante un procedimiento autorizado y verificable.

## 6. Alcance y restricciones

- **Fase 1 (dentro de alcance):** crear cuentas, validar y procesar transferencias, registrar operaciones y consultar historiales.
- **Fuera de alcance en fase 1:** integración con bancos externos, pasarelas de pago, servicios antifraude de terceros y cambio de divisas.
- La migración de datos, las herramientas tecnológicas finales y los mecanismos de recuperación se definirán en fases posteriores.

## 7. Supuestos técnicos

- Se asume conectividad estable entre el cliente y el sistema, y entre AWS y los sistemas on-premise a través de la VPN.
- El sistema no maneja cambio de divisas en la fase 1.
- La persistencia se realizará sobre una base de datos relacional con soporte de transacciones ACID.

## 8. Aspectos pendientes de confirmar

Estos puntos deben acordarse con el cliente antes de la versión definitiva del diseño:

| Tema | Pendiente de confirmar |
|------|------------------------|
| Política de transferencias | Monedas, límites, comisiones, tipos de cuenta y condiciones para operar. |
| Usuarios y auditoría | Quién crea cuentas, autoriza transferencias, consulta información y revisa registros. |
| Requisitos operativos | Volumen de operaciones, tiempo máximo de respuesta (RNF-05), disponibilidad y recuperación (RNF-06). |
| Conservación del historial | Política de retención y requisitos de auditoría. |
| Recuperación ante interrupciones | Procedimiento para resolver operaciones cuyo resultado sea incierto tras una interrupción. |

---

> Documentar estos supuestos protege tanto a la institución como al equipo: delimita qué se compromete a entregar la fase 1 y qué queda sujeto a confirmación.
