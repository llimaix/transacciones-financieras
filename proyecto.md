# Proyecto

## Sistema de transferencias financieras

---

## Justificación

El proyecto del curso ha sido diseñado con el propósito de evaluar de manera integral las competencias desarrolladas durante la asignatura, particularmente en las áreas de:

- Análisis de requerimientos
- Modelado de sistemas
- Diseño arquitectónico
- Diseño de componentes
- Validación mediante pruebas
- Comunicación técnica

A diferencia de enfoques centrados en la implementación, este proyecto prioriza el pensamiento ingenieril, la toma de decisiones fundamentadas y la coherencia entre artefactos.

---

## Planteamiento del problema

Una institución financiera requiere modernizar su sistema de transferencias entre cuentas, ya que el proceso actual presenta deficiencias en control, validación y trazabilidad de operaciones.

Los problemas identificados incluyen:

- Inconsistencias en los saldos de las cuentas
- Falta de validación adecuada en las transacciones
- Errores en transferencias (duplicadas, incompletas o inválidas)
- Ausencia de un modelo claro para el registro de operaciones
- Dificultad para auditar transacciones

Adicionalmente, el sistema actual no contempla correctamente escenarios de error, lo que genera incertidumbre en el resultado de las operaciones y pérdida de confianza por parte de los usuarios.

Esto provoca:

- Riesgos financieros
- Pérdida de integridad de la información
- Dificultad para detectar errores o fraudes
- Baja confiabilidad del sistema

Se requiere diseñar un sistema que permita realizar transferencias de forma controlada, asegurando consistencia lógica y manejo adecuado de errores.

---

## Requerimientos funcionales

> *(NO son exhaustivos — el grupo debe analizarlos y completarlos)*

### Gestión de cuentas

- El sistema debe permitir crear cuentas.
- Cada cuenta debe tener un identificador único.

### Transferencias

- El sistema debe permitir transferir fondos entre cuentas.
- El sistema debe registrar cada transacción realizada.

### Validaciones

- El sistema debe validar la existencia de cuentas.
- El sistema debe validar disponibilidad de fondos.
- El sistema debe evitar duplicidad de operaciones.

### Historial

- El sistema debe permitir consultar el historial de transacciones.

---

## Requerimientos no funcionales

### Consistencia (crítico)

- El sistema debe garantizar que las operaciones sean coherentes (no pérdida ni creación indebida de dinero).

### Confiabilidad

- El sistema debe manejar correctamente escenarios de error.

### Mantenibilidad

- El diseño debe permitir cambios en reglas sin afectar el sistema completo.

### Seguridad (conceptual)

- El sistema debe contemplar validaciones que eviten operaciones inválidas.

---

## Requerimientos técnicos (de diseño)

### Arquitectura

- El equipo debe seleccionar un estilo arquitectónico adecuado.
- Debe justificarse en función del problema.
- Deben compararse al menos dos alternativas descartadas.

### Diseño de componentes

- El sistema debe dividirse en módulos con responsabilidades claras.
- Debe garantizarse alta cohesión y bajo acoplamiento.

### Modelado

- Se deben elaborar diagramas UML:
  - Casos de uso
  - Clases
  - Secuencia
  - Componentes

### Trazabilidad obligatoria

- Requerimiento → Caso de uso → Diseño → Prueba

### UX / IX

- Se debe diseñar el flujo de:
  - Solicitud de turno
  - Atención
- Se deben presentar wireframes funcionales.

### Pruebas

- Se deben definir casos de prueba por cada caso de uso.
- Se deben incluir:
  - Escenarios normales
  - Escenarios alternos
  - Escenarios de error
- Se deben definir criterios de aceptación verificables.

---

## Restricciones del proyecto

- El sistema debe centrarse únicamente en el alcance definido.
- No se evaluará la cantidad de funcionalidades, sino la profundidad del diseño.
- Todas las decisiones deben estar justificadas.
- No se aceptarán soluciones genéricas sin adaptación al problema.

---

## Supuestos (obligatorio documentar)

El equipo deberá documentar supuestos como:

- Disponibilidad de usuarios
- Contexto de uso
- Número de agentes
- Condiciones de operación

---

## Criterios de validación

El sistema será considerado válido si:

- Los requerimientos son claros y completos
- Existe coherencia entre artefactos
- La arquitectura está justificada
- Las pruebas validan el sistema
- El equipo puede defender todas sus decisiones
