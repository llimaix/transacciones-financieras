# Flujos UX

> **Responsable:** Josue  
> **Tarea:** T-11  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-03 (Casos de uso — Astrid)

---

## Instrucciones

El PDF exige diseñar explícitamente los flujos de:
1. **Solicitud / inicio de operación** (el usuario inicia una transferencia)
2. **Atención / ejecución** (el sistema procesa la operación)

Documenta cada flujo como un diagrama de flujo o mapa de pantallas. Exporta como imagen en esta carpeta.

---

## Flujo 1 — Inicio de transferencia (perspectiva del usuario)

> Insertar imagen: `flujo-inicio-transferencia.png`

**Pasos del flujo:**
```
[Inicio]
  ↓
[Pantalla: Ingresar sesión]
  ↓
[Pantalla: Panel principal]
  ↓
[Seleccionar "Nueva transferencia"]
  ↓
[Pantalla: Formulario de transferencia]
  → Ingresar cuenta destino
  → Ingresar monto
  → (Opcional) Descripción / referencia
  ↓
[Pantalla: Confirmación de datos]
  ↓
[¿Confirma?]
  → No → volver al formulario
  → Sí → enviar al sistema
  ↓
[Pantalla: Resultado]
  → Exitosa → mostrar comprobante
  → Error → mostrar motivo y opciones
  ↓
[Fin]
```

---

## Flujo 2 — Atención del sistema (perspectiva del sistema)

> Insertar imagen: `flujo-procesamiento-sistema.png`

**Pasos del flujo:**
```
[Recibir solicitud de transferencia]
  ↓
[Validar existencia de cuentas]
  → Cuenta no existe → rechazar y notificar
  ↓
[Validar fondos disponibles]
  → Fondos insuficientes → rechazar y notificar
  ↓
[Verificar duplicidad]
  → Es duplicada → rechazar y notificar
  ↓
[Ejecutar débito en cuenta origen]
  ↓
[Ejecutar crédito en cuenta destino]
  ↓
[Registrar transacción como EXITOSA]
  ↓
[Notificar al usuario]
  ↓
[Fin]
```

---

## Flujo 3 — Consulta de historial

> Insertar imagen: `flujo-historial.png`

```
[Usuario selecciona "Ver historial"]
  ↓
[Sistema consulta transacciones por cuenta]
  ↓
[Pantalla: Lista de transacciones con filtros]
  ↓
[Usuario selecciona una transacción]
  ↓
[Pantalla: Detalle de transacción]
  ↓
[Fin]
```

---

_Genera los diagramas visuales, agrega las imágenes y cambia el estado a ✅._
