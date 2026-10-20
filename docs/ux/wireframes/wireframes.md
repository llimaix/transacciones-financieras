# Wireframes Funcionales

> **Responsable:** Josue
> **Tarea:** T-12
> **Estado:** ✅ Completado
> **Depende de:** T-11 (Flujos UX)

---

## 1. Propósito

Wireframes de media/alta fidelidad para cada pantalla de los flujos UX. Representan la estructura, el contenido y el estilo visual propuesto de cada pantalla.

> **Prototipo visual:** las 8 pantallas están maquetadas en `prototipo.html` — un prototipo navegable autocontenido (sin dependencias) que se abre con doble clic en cualquier navegador. Es el artefacto principal de esta tarea y el recomendado para la presentación al cliente.

---

## 2. Inventario de pantallas

| ID | Pantalla | Aparece en el flujo | Caso de uso |
|------|----------|---------------------|-------------|
| WF-01 | Inicio de sesión / login | Flujo 1 | CU-02 (acceso) |
| WF-02 | Panel principal | Flujos 1 y 3 | CU-02, CU-04 |
| WF-03 | Formulario de transferencia | Flujo 1 | CU-02 |
| WF-04 | Confirmación de transferencia | Flujo 1 | CU-02 |
| WF-05 | Resultado exitoso | Flujo 1 | CU-02 |
| WF-06 | Resultado con error | Flujo 1 | CU-02 / CU-03 |
| WF-07 | Historial de transacciones | Flujo 3 | CU-04 |
| WF-08 | Detalle de transacción | Flujo 3 | CU-04 |

---

## 3. Descripción de cada pantalla

### WF-01 · Inicio de sesión
- Campos: usuario, contraseña.
- Botón: Ingresar.
- Enlace: ¿Olvidaste tu contraseña?

### WF-02 · Panel principal
- Saldo de las cuentas del usuario.
- Accesos directos: Nueva transferencia, Ver historial.
- Resumen de últimas transacciones.

### WF-03 · Formulario de transferencia
- Cuenta origen (selección), cuenta destino (ingreso/selección), monto, descripción (opcional).
- La referencia única de solicitud se genera automáticamente (no la ingresa el usuario).
- Botones: Continuar / Cancelar.

### WF-04 · Confirmación de transferencia
- Resumen de los datos ingresados (solo lectura).
- Botones: Confirmar / Editar.

### WF-05 · Resultado exitoso
- Mensaje de éxito con número de comprobante.
- Detalles de la operación (origen, destino, monto, fecha, estado EXITOSA).
- Botones: Nueva transferencia / Ir al inicio.

### WF-06 · Resultado con error
- Mensaje de error claro (p. ej. "Fondos insuficientes", "Cuenta destino no encontrada", "Operación duplicada detectada").
- Descripción del motivo.
- Botones: Intentar de nuevo / Ir al inicio.

### WF-07 · Historial de transacciones
- Lista con: fecha, monto, cuenta destino, estado.
- Filtros: por fecha, por estado.
- Paginación.

### WF-08 · Detalle de transacción
- Todos los campos de la transacción seleccionada (incluida la referencia única y el motivo de rechazo si aplica).
- Botón: Volver al historial.

---

## 4. Nota de diseño

El campo **referencia única** de la solicitud (clave para la idempotencia, RB-05) se genera del lado del sistema y no se expone como campo editable en WF-03, para evitar que el usuario pueda alterarlo. Sí se muestra, en cambio, en el comprobante (WF-05) y en el detalle (WF-08) como dato de trazabilidad.
