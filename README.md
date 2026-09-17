# Sistema de Transferencias Financieras

**Universidad Mariano Gálvez**  
Facultad de Ingeniería en Sistemas de Información y Ciencias de la Computación  
Análisis de Sistemas II — Proyecto Final

---

## Descripción del proyecto

Diseño de un sistema que permita realizar transferencias de fondos entre cuentas de forma controlada, garantizando consistencia lógica, validación adecuada y manejo correcto de errores.

Este proyecto **no evalúa implementación de código**, sino la profundidad del diseño de ingeniería: requerimientos, modelado, arquitectura, componentes, pruebas y trazabilidad.

---

## Integrantes

| Nombre   | Responsabilidad principal              |
|----------|----------------------------------------|
| Astrid   | Requerimientos y Casos de Uso          |
| Fabiola  | Arquitectura y Diseño de Componentes   |
| Wuilli   | Modelado UML (Clases y Secuencia)      |
| Josue    | UX / Wireframes y Supuestos            |
| Luis     | Pruebas y Trazabilidad                 |

---

## Estructura del repositorio

```
transacciones-financieras/
├── README.md
├── TASKS.md                        ← Guía de tareas y tracking
├── docs/
│   ├── requerimientos/
│   │   ├── requerimientos-funcionales.md
│   │   ├── requerimientos-no-funcionales.md
│   │   └── supuestos.md
│   ├── arquitectura/
│   │   ├── decision-arquitectonica.md
│   │   └── alternativas-descartadas.md
│   ├── diagramas/
│   │   ├── casos-de-uso/
│   │   ├── clases/
│   │   ├── secuencia/
│   │   └── componentes/
│   ├── ux/
│   │   ├── flujos/
│   │   └── wireframes/
│   └── pruebas/
│       ├── casos-de-prueba.md
│       └── criterios-aceptacion.md
└── trazabilidad/
    └── matriz-trazabilidad.md
```

---

## Problema que resuelve

Una institución financiera necesita modernizar su sistema de transferencias entre cuentas. El sistema actual tiene:

- Inconsistencias en saldos
- Falta de validación en transacciones
- Errores (duplicados, incompletas o inválidas)
- Sin modelo claro para registro de operaciones
- Dificultad para auditar transacciones

---

## Requerimientos funcionales clave

- **Gestión de cuentas**: crear cuentas con identificador único
- **Transferencias**: transferir fondos y registrar cada transacción
- **Validaciones**: existencia de cuentas, disponibilidad de fondos, evitar duplicados
- **Historial**: consultar historial de transacciones

---

## Criterios de validación del proyecto

El sistema será considerado válido si:
- Los requerimientos son claros y completos
- Existe coherencia entre artefactos
- La arquitectura está justificada
- Las pruebas validan el sistema
- El equipo puede defender todas sus decisiones

---

## Tracking de avance

Ver [`TASKS.md`](./TASKS.md) para el detalle de tareas, asignaciones y estado actualizado.
