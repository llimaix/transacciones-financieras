# Diseño de Componentes

> **Responsable:** Fabiola
> **Tarea:** T-06
> **Estado:** ✅ Completado
> **Depende de:** T-04 (Decisión arquitectónica)

---

## 1. Objetivo

Dividir el sistema en componentes con responsabilidades claras, garantizando **alta cohesión** (cada componente tiene una única razón para cambiar) y **bajo acoplamiento** (los componentes dependen de interfaces, no de implementaciones). Cada componente se ubica en una de las cinco capas definidas en la decisión arquitectónica y es la base para el diagrama de componentes y el diagrama de clases.

---

## 2. Catálogo de componentes

| ID | Componente | Capa | Responsabilidad | Interfaz expuesta |
|------|-----------|------|-----------------|-------------------|
| **C-01** | API / Controlador | Presentación | Recibir peticiones, autenticar/autorizar por rol y delegar en los servicios de aplicación. | `crearCuenta()`, `transferir()`, `consultarHistorial()` |
| **C-02** | Servicio de Transferencias | Aplicación | Orquestar el caso de uso de transferencia: abrir la transacción, coordinar validación, proceso atómico y registro, controlar la idempotencia por referencia única. | `ejecutarTransferencia(solicitud)` |
| **C-03** | Servicio de Cuentas | Aplicación | Orquestar la creación y consulta de cuentas. | `crearCuenta(datos)`, `consultarCuenta(id)` |
| **C-04** | Servicio de Consulta | Aplicación | Orquestar la consulta de historial respetando permisos y filtros. | `consultarHistorial(criterios)` |
| **C-05** | Motor de Reglas / Validaciones | Dominio | Validar existencia y habilitación de cuentas, monto válido, fondos suficientes y duplicados. Concentra las reglas de negocio. | `validarTransferencia(solicitud)`, `esDuplicada(ref)` |
| **C-06** | Procesador de Transacción Atómica | Dominio | Ejecutar débito en origen y crédito en destino como una sola operación ACID; revertir ante fallo. | `procesar(origen, destino, monto)` |
| **C-07** | Repositorio de Cuentas | Infraestructura | Persistir y recuperar cuentas y saldos con garantías transaccionales. | `obtener(id)`, `actualizarSaldo(id, saldo)` |
| **C-08** | Repositorio de Historial | Infraestructura | Guardar y consultar el registro de transacciones con su estado. | `guardar(transaccion)`, `buscar(criterios)` |
| **C-09** | Adaptador de Integración on-premise | Anticorrupción | Traducir entre el dominio y los sistemas on-premise vía API/SOAP sobre VPN, sin contaminar el núcleo. | `invocarServicioExterno(peticion)` |

---

## 3. Relaciones entre componentes

```
C-01 (API)            → C-02, C-03, C-04   : delega la orquestación de cada caso de uso
C-02 (Transferencias) → C-05               : solicita validación de la transferencia
C-02 (Transferencias) → C-06               : ordena el procesamiento atómico débito/crédito
C-02 (Transferencias) → C-08               : registra el resultado de la transacción
C-03 (Cuentas)        → C-07               : crea y consulta cuentas
C-04 (Consulta)       → C-08               : consulta el historial
C-05 (Reglas)         → C-07, C-08         : lee saldos y verifica duplicados para validar
C-06 (Proceso atómico)→ C-07               : debita y acredita dentro de una transacción ACID
C-02 (Transferencias) → C-09               : invoca sistemas on-premise cuando el flujo lo requiere
```

- **C-02 es el orquestador central** del caso de uso crítico (transferencia): abre la transacción, coordina a C-05, C-06 y C-08, y es el responsable de la idempotencia.
- **C-06 es el único componente que modifica saldos**, y siempre dentro de una transacción atómica. Esto concentra el invariante financiero en un solo punto.

> **Versión editable (draw.io):** `../arquitectura/diagrama-relaciones-componentes.drawio` muestra estas relaciones con cada interacción etiquetada (qué solicita cada componente a cuál) y las capas diferenciadas por color.

---

## 4. Justificación de cohesión y bajo acoplamiento

**Alta cohesión:**
- Cada componente tiene una sola responsabilidad: C-05 solo valida, C-06 solo ejecuta el movimiento atómico, los repositorios (C-07, C-08) solo persisten. Ninguno mezcla responsabilidades de otra capa.
- Las reglas de negocio están aisladas en el dominio (C-05, C-06), de modo que un cambio en una regla no afecta a presentación ni a persistencia (sostiene la mantenibilidad, RNF-07).

**Bajo acoplamiento:**
- Los servicios de aplicación dependen de las **interfaces** de los repositorios y del dominio, no de sus implementaciones. Cambiar la base de datos o el mecanismo de integración on-premise no obliga a tocar la lógica de negocio.
- El adaptador C-09 actúa como barrera: los detalles de SOAP/VPN quedan encapsulados y no permean al dominio (patrón anticorrupción).

**Concentración del invariante crítico:**
- Solo C-06 altera saldos y siempre atómicamente. Esto hace que garantizar "ningún débito sin su crédito" (RNF-01, RB-04, RB-07) sea verificable en un único punto del diseño.

---

## 5. Trazabilidad componente → requerimiento / caso de uso

| Componente | RF que soporta | Caso de uso |
|------------|----------------|-------------|
| C-01 API / Controlador | RF-01, RF-03, RF-08 | CU-01, CU-02, CU-04 |
| C-02 Servicio de Transferencias | RF-03, RF-05, RF-06 | CU-02, CU-03 |
| C-03 Servicio de Cuentas | RF-01, RF-02 | CU-01 |
| C-04 Servicio de Consulta | RF-08 | CU-04 |
| C-05 Motor de Reglas / Validaciones | RF-04, RF-05 | CU-02, CU-03 |
| C-06 Procesador de Transacción Atómica | RF-06 | CU-02 |
| C-07 Repositorio de Cuentas | RF-01, RF-02 | CU-01, CU-02 |
| C-08 Repositorio de Historial | RF-07 | CU-02, CU-03, CU-04 |
| C-09 Adaptador de Integración on-premise | RF-04 (apoyo) | CU-02 |

---

## 6. Correspondencia con las clases de diseño

Estos componentes se implementan mediante las siguientes clases (detalladas en el diagrama de clases):

| Componente | Clase(s) principal(es) |
|------------|------------------------|
| C-02 | `TransferenciaService` |
| C-03 | `CuentaService` |
| C-04 | `ConsultaService` |
| C-05 | `ValidadorFondos` (y reglas asociadas) |
| C-06 | `ProcesadorTransaccion` |
| C-07 | `CuentaRepository` (sobre entidad `Cuenta`) |
| C-08 | `HistorialRepository` (sobre entidad `Transaccion`) |
| C-09 | `AdaptadorOnPremise` |
