# TASKS — Sistema de Transferencias Financieras

> Guía de trabajo, asignación de responsabilidades y tracking de estado.  
> **Leyenda de estado:** `⬜ Pendiente` · `🔄 En progreso` · `✅ Completado` · `🔒 Bloqueado`

---

## Resumen de asignaciones

| Entregable                          | Responsable | Depende de        |
|-------------------------------------|-------------|-------------------|
| Requerimientos funcionales          | Astrid      | —                 |
| Requerimientos no funcionales       | Astrid      | —                 |
| Supuestos documentados              | Josue       | —                 |
| Casos de uso                        | Astrid      | Requerimientos    |
| Decisión arquitectónica             | Fabiola     | Requerimientos    |
| Alternativas descartadas            | Fabiola     | —                 |
| Diseño de componentes               | Fabiola     | Arquitectura      |
| Diagrama de clases                  | Wuilli      | Diseño componentes|
| Diagrama de secuencia               | Wuilli      | Casos de uso      |
| Diagrama de componentes             | Wuilli      | Diseño componentes|
| Flujos UX + Wireframes              | Josue       | Casos de uso      |
| Casos de prueba                     | Luis        | Casos de uso      |
| Criterios de aceptación             | Luis        | Casos de prueba   |
| Matriz de trazabilidad              | Luis        | Todo lo anterior  |

---

## MÓDULO 1 — Requerimientos
> **Responsable principal: Astrid**

### T-01 · Completar requerimientos funcionales
**Archivo:** `docs/requerimientos/requerimientos-funcionales.md`  
**Estado:** ✅ Completado  
**Depende de:** —  
**Notas:**  
El PDF entrega una lista base que NO es exhaustiva. Astrid debe analizar el problema y expandirlos cubriendo al menos:
- Gestión de cuentas (crear, consultar, desactivar)
- Transferencias (iniciar, confirmar, cancelar)
- Validaciones (existencia, fondos, duplicados, límites)
- Historial (consulta por cuenta, por rango de fecha, por estado)

---

### T-02 · Documentar requerimientos no funcionales
**Archivo:** `docs/requerimientos/requerimientos-no-funcionales.md`  
**Estado:** ✅ Completado  
**Depende de:** T-01  
**Notas:**  
Desarrollar en detalle los 4 RF no funcionales del PDF:
- Consistencia (crítico): atomicidad de operaciones
- Confiabilidad: manejo de errores y rollback
- Mantenibilidad: separación de responsabilidades
- Seguridad conceptual: validaciones anti-fraude

---

### T-03 · Elaborar casos de uso
**Archivo:** `docs/diagramas/casos-de-uso/`  
**Estado:** ✅ Completado  
**Depende de:** T-01  
**Notas:**  
- Diagrama de casos de uso general (actores + sistema)
- Al menos 1 descripción expandida por caso de uso (flujo normal, alterno, error)
- Actores mínimos: Cliente, Auditor, Sistema

---

## MÓDULO 2 — Arquitectura y Diseño
> **Responsable principal: Fabiola**

### T-04 · Decisión arquitectónica
**Archivo:** `docs/arquitectura/decision-arquitectonica.md`  
**Estado:** ✅ Completado  
**Depende de:** T-01  
**Notas:**  
- Seleccionar y justificar el estilo arquitectónico elegido (ej. Capas, Hexagonal, Microservicios, Event-Driven)
- Argumentar por qué es adecuado para este problema específico
- Conectar la decisión con los requerimientos no funcionales (especialmente consistencia)

---

### T-05 · Documentar alternativas descartadas
**Archivo:** `docs/arquitectura/alternativas-descartadas.md`  
**Estado:** ✅ Completado  
**Depende de:** —  
**Notas:**  
- Describir al menos 2 estilos arquitectónicos alternativos
- Para cada uno: ventajas, desventajas y razón de descarte
- El proyecto exige explícitamente este ejercicio de comparación

---

### T-06 · Diseño de componentes
**Archivo:** `docs/arquitectura/`  
**Estado:** ✅ Completado  
**Depende de:** T-04  
**Notas:**  
- Dividir el sistema en módulos con responsabilidades claras
- Garantizar alta cohesión y bajo acoplamiento
- Documentar las interfaces entre componentes
- Será la base para los diagramas UML de Wuilli (T-08, T-09)

---

## MÓDULO 3 — Modelado UML
> **Responsable principal: Wuilli**

### T-07 · Diagrama de componentes
**Archivo:** `docs/diagramas/componentes/`  
**Estado:** ✅ Completado  
**Depende de:** T-06 (Diseño de componentes — Fabiola)  
**Notas:**  
- Representar visualmente los módulos definidos por Fabiola
- Mostrar relaciones, dependencias e interfaces
- Herramienta sugerida: draw.io, Lucidchart o PlantUML

---

### T-08 · Diagrama de clases
**Archivo:** `docs/diagramas/clases/`  
**Estado:** ✅ Completado  
**Depende de:** T-06 (Diseño de componentes — Fabiola)  
**Notas:**  
- Clases mínimas esperadas: `Cuenta`, `Transaccion`, `TransferenciaService`, `ValidadorFondos`, `HistorialRepository`
- Incluir atributos, métodos y relaciones (herencia, composición, dependencia)

---

### T-09 · Diagramas de secuencia
**Archivo:** `docs/diagramas/secuencia/`  
**Estado:** ✅ Completado  
**Depende de:** T-03 (Casos de uso — Astrid)  
**Notas:**  
- Un diagrama por flujo principal, mínimo:
  - Transferencia exitosa
  - Transferencia fallida (fondos insuficientes)
  - Transferencia duplicada detectada
- Mostrar interacción entre actores y componentes del sistema

---

## MÓDULO 4 — UX / Experiencia de usuario
> **Responsable principal: Josue**

### T-10 · Documentar supuestos
**Archivo:** `docs/requerimientos/supuestos.md`  
**Estado:** ✅ Completado  
**Depende de:** —  
**Notas:**  
El PDF exige documentar supuestos obligatoriamente. Mínimo:
- Disponibilidad de usuarios
- Contexto de uso (web, app, API)
- Número de agentes / operadores
- Condiciones de operación (horarios, volumen de transacciones)
- Restricciones regulatorias asumidas

---

### T-11 · Diseño de flujos UX
**Archivo:** `docs/ux/flujos/`  
**Estado:** ✅ Completado  
**Depende de:** T-03 (Casos de uso — Astrid)  
**Notas:**  
El PDF pide diseñar explícitamente el flujo de:
- Solicitud de turno / inicio de operación
- Atención / ejecución de transferencia
- Confirmación / resultado

---

### T-12 · Wireframes funcionales
**Archivo:** `docs/ux/wireframes/`  
**Estado:** ✅ Completado  
**Depende de:** T-11  
**Notas:**  
- Wireframes de baja/media fidelidad para cada flujo
- Cubrir: pantalla de inicio, ingreso de datos, confirmación, resultado exitoso, resultado de error
- Herramienta sugerida: Figma, Balsamiq, draw.io o similar

---

## MÓDULO 5 — Pruebas y Trazabilidad
> **Responsable principal: Luis**

### T-13 · Definir casos de prueba
**Archivo:** `docs/pruebas/casos-de-prueba.md`  
**Estado:** ✅ Completado  
**Depende de:** T-03 (Casos de uso — Astrid)  
**Notas:**  
Por cada caso de uso se necesitan al menos 3 escenarios:
- **Normal**: operación exitosa
- **Alterno**: variación válida del flujo
- **Error**: condición inválida o falla del sistema

---

### T-14 · Definir criterios de aceptación
**Archivo:** `docs/pruebas/criterios-aceptacion.md`  
**Estado:** ✅ Completado  
**Depende de:** T-13  
**Notas:**  
- Criterios verificables (no subjetivos)
- Formato sugerido: dado/cuando/entonces (Gherkin)
- Cada criterio debe estar ligado a un requerimiento funcional

---

### T-15 · Construir matriz de trazabilidad
**Archivo:** `trazabilidad/matriz-trazabilidad.md`  
**Estado:** ✅ Completado  
**Depende de:** T-01, T-03, T-06, T-08, T-13, T-14 (requiere que todos entreguen)  
**Notas:**  
El PDF exige trazabilidad obligatoria:  
`Requerimiento → Caso de uso → Diseño → Prueba`  
- Tabla cruzada que conecte cada RF con su caso de uso, componente/clase y caso de prueba
- Este es el artefacto integrador del proyecto — **Luis coordina que cada área le entregue sus IDs**

---

## Orden de ejecución sugerido

```
Semana 1 — Base
  Astrid:   T-01 Requerimientos funcionales
  Fabiola:  T-05 Alternativas descartadas
  Josue:    T-10 Supuestos
  (paralelo — sin dependencias)

Semana 2 — Diseño
  Astrid:   T-02 RF no funcionales  →  T-03 Casos de uso
  Fabiola:  T-04 Decisión arquitectónica  →  T-06 Diseño de componentes
  Josue:    T-11 Flujos UX  (depende de T-03)

Semana 3 — Modelado y UX
  Wuilli:   T-07 Diagrama componentes  (depende de T-06)
             T-08 Diagrama clases       (depende de T-06)
             T-09 Diagramas secuencia   (depende de T-03)
  Josue:    T-12 Wireframes             (depende de T-11)

Semana 4 — Pruebas y cierre
  Luis:     T-13 Casos de prueba        (depende de T-03)
             T-14 Criterios aceptación  (depende de T-13)
             T-15 Matriz trazabilidad   (depende de TODO)
```

---

## Notas de coordinación

- **Dependencia crítica**: Astrid debe completar T-01 y T-03 en la primera semana porque varios integrantes dependen de ello.
- **Dependencia crítica**: Fabiola debe entregar T-06 antes de que Wuilli pueda avanzar con T-07 y T-08.
- **Luis no puede cerrar T-15** hasta tener IDs de requerimientos (Astrid), IDs de casos de uso (Astrid), IDs de componentes/clases (Wuilli/Fabiola) y casos de prueba propios. Coordinar en la semana 4.
- Usar los nombres de archivo/carpeta definidos en este documento para mantener consistencia.
- Hacer PR o commits directamente a `main` según acuerden como equipo.
