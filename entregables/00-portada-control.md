# Sistema de Transferencias Financieras

### Documento de Diseño de Ingeniería

**Universidad Mariano Gálvez de Guatemala**
Facultad de Ingeniería en Sistemas de Información y Ciencias de la Computación
Análisis de Sistemas II — Proyecto Final

---

## Información del documento

| Campo | Detalle |
|-------|---------|
| **Título del documento** | Documento de Diseño — Sistema de Transferencias Financieras |
| **Proyecto** | Sistema de Transferencias Financieras |
| **Curso** | Análisis de Sistemas II |
| **Versión actual** | 1.0 |
| **Estado** | Entregable final |
| **Fecha de emisión** | 15 de octubre de 2026 |
| **Clasificación** | Uso académico |

---

## Equipo de trabajo

| Nombre | Rol / Responsabilidad | Artefactos a cargo |
|--------|-----------------------|--------------------|
| Astrid | Requerimientos y Casos de Uso | Requerimientos funcionales, no funcionales y casos de uso |
| Fabiola | Arquitectura y Diseño de Componentes | Decisión arquitectónica, alternativas descartadas, diseño de componentes |
| Wuilli | Modelado UML | Diagramas de clases, componentes y secuencia |
| Josue | UX y Supuestos | Flujos UX, wireframes y supuestos del sistema |
| Luis | Pruebas y Trazabilidad | Casos de prueba, criterios de aceptación y matriz de trazabilidad |

---

## Control de versiones

| Versión | Fecha | Autor(es) | Descripción del cambio |
|---------|-------|-----------|------------------------|
| 0.1 | 01/10/2026 | Equipo | Estructura inicial del documento y definición de responsables. |
| 0.2 | 05/10/2026 | Astrid | Requerimientos funcionales (RF-01..RF-09), no funcionales (RNF-01..RNF-08) y reglas de negocio (RB-01..RB-07). |
| 0.3 | 08/10/2026 | Astrid | Casos de uso (CU-01..CU-04) con flujos normal, alterno y de error. |
| 0.4 | 10/10/2026 | Fabiola | Decisión arquitectónica (Capas + dominio transaccional sobre AWS) y alternativas descartadas. |
| 0.5 | 12/10/2026 | Fabiola | Diseño de componentes (C-01..C-09) con cohesión y acoplamiento. |
| 0.6 | 13/10/2026 | Wuilli | Diagramas UML: clases, componentes y secuencia. |
| 0.7 | 14/10/2026 | Josue | Supuestos del sistema, flujos UX y wireframes (WF-01..WF-08). |
| 0.8 | 15/10/2026 | Luis | Casos de prueba (CP-01..CP-09) y criterios de aceptación (CA-01..CA-09). |
| 0.9 | 15/10/2026 | Luis | Matriz de trazabilidad y verificación de integridad. |
| 1.0 | 15/10/2026 | Equipo | Unificación, revisión de coherencia y versión final para entrega. |

---

## Aprobaciones

| Rol | Nombre | Firma | Fecha |
|-----|--------|-------|-------|
| Responsable de requerimientos | Astrid | | |
| Responsable de arquitectura | Fabiola | | |
| Responsable de modelado | Wuilli | | |
| Responsable de UX | Josue | | |
| Responsable de pruebas | Luis | | |

---

## Propósito del documento

Este documento consolida el diseño de ingeniería del Sistema de Transferencias Financieras. Su objetivo es demostrar el análisis del problema, la toma de decisiones fundamentadas y la coherencia entre artefactos, desde los requerimientos hasta las pruebas, cubriendo:

- Requerimientos funcionales, no funcionales y supuestos.
- Arquitectura seleccionada y alternativas descartadas.
- Diseño de componentes y modelado UML (casos de uso, clases, secuencia, componentes).
- Diseño de experiencia de usuario (flujos y wireframes).
- Estrategia de pruebas y criterios de aceptación.
- Matriz de trazabilidad `Requerimiento → Caso de uso → Diseño → Prueba`.

El proyecto prioriza la **profundidad del diseño** sobre la cantidad de funcionalidades, garantizando como atributo crítico la **consistencia financiera**: ninguna operación crea ni destruye dinero.

---

## Alcance

- **Fase 1 (cubierta en este documento):** creación de cuentas, validación y procesamiento de transferencias, registro de operaciones y consulta de historial.
- **Fuera de alcance (fases posteriores):** integración con bancos externos, pasarelas de pago, servicios antifraude de terceros y cambio de divisas.

---

## Índice de contenido

1. Requerimientos funcionales
2. Requerimientos no funcionales
3. Supuestos del sistema
4. Casos de uso
5. Decisión arquitectónica
6. Alternativas arquitectónicas descartadas
7. Diseño de componentes
8. Diagrama de componentes
9. Diagrama de clases
10. Diagramas de secuencia
11. Flujos UX
12. Wireframes funcionales
13. Casos de prueba
14. Criterios de aceptación
15. Matriz de trazabilidad

---

## Glosario de identificadores

| Prefijo | Significado |
|---------|-------------|
| **RF** | Requerimiento funcional |
| **RNF** | Requerimiento no funcional |
| **RB** | Regla de negocio |
| **CU** | Caso de uso |
| **C** | Componente de diseño |
| **CP** | Caso de prueba |
| **CA** | Criterio de aceptación |
| **WF** | Wireframe (pantalla) |
