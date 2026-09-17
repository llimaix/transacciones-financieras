# Diseño de Componentes

> **Responsable:** Fabiola  
> **Tarea:** T-06  
> **Estado:** ⬜ Pendiente  
> **Depende de:** T-04 (Decisión arquitectónica)

---

## Objetivo

Dividir el sistema en módulos con responsabilidades claras, garantizando **alta cohesión** y **bajo acoplamiento**.

---

## Componentes del sistema

| ID   | Componente             | Responsabilidad                                      | Interfaz expuesta              |
|------|------------------------|------------------------------------------------------|--------------------------------|
| C-01 | _(nombre)_             | _(qué hace)_                                         | _(métodos o endpoints)_        |
| C-02 | _(nombre)_             | _(qué hace)_                                         | _(métodos o endpoints)_        |
| C-03 | _(nombre)_             | _(qué hace)_                                         | _(métodos o endpoints)_        |
| C-04 | _(nombre)_             | _(qué hace)_                                         | _(métodos o endpoints)_        |
| C-05 | _(nombre)_             | _(qué hace)_                                         | _(métodos o endpoints)_        |

---

## Relaciones entre componentes

> Describe cómo se comunican los componentes entre sí.  
> _(Ej: C-01 llama a C-02 para validar fondos antes de ejecutar la transferencia)_

```
C-01 → C-02 : _(describe la interacción)_
C-02 → C-03 : _(describe la interacción)_
```

---

## Justificación de cohesión y acoplamiento

> Explica por qué este diseño logra alta cohesión y bajo acoplamiento.  
> _(Ej: Cada componente tiene una única razón para cambiar; los componentes no dependen de implementaciones sino de interfaces)_

---

## Notas para Wuilli

> Wuilli usará este documento como base para:
> - T-07: Diagrama de componentes
> - T-08: Diagrama de clases
>
> Por favor asigna **IDs claros** (C-01, C-02...) a cada componente para que la trazabilidad funcione.

---

_Cambia el estado a ✅ cuando termines._
