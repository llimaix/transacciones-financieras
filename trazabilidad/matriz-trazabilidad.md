# Matriz de Trazabilidad

> **Responsable:** Luis
> **Tarea:** T-15
> **Estado:** ✅ Completado
> **Depende de:** T-01, T-03, T-06, T-08, T-13, T-14

---

## 1. Propósito

Artefacto integrador del proyecto. Conecta cada requerimiento funcional con su caso de uso, componente, clase de diseño, caso de prueba y criterio de aceptación, cumpliendo la trazabilidad obligatoria:

`Requerimiento → Caso de uso → Diseño → Prueba`

Todos los identificadores corresponden al esquema definitivo del proyecto.

---

## 2. Matriz principal (Requerimiento → Caso de uso → Diseño → Prueba)

| RF | Descripción | Regla(s) negocio | Caso de uso | Componente | Clase de diseño | Caso de prueba | Criterio aceptación |
|------|-------------|------------------|-------------|------------|-----------------|----------------|---------------------|
| **RF-01** | Crear cuentas | RB-01 | CU-01 | C-03, C-07 | `CuentaService`, `Cuenta`, `CuentaRepository` | CP-06, CP-07 | CA-06, CA-07 |
| **RF-02** | Consultar cuentas | RB-03 | CU-01 | C-03, C-07 | `CuentaService`, `CuentaRepository` | CP-06 | CA-06 |
| **RF-03** | Solicitar transferencias | RB-01 | CU-02 | C-01, C-02 | `TransferenciaService` | CP-01 | CA-01 |
| **RF-04** | Validar transferencias | RB-02, RB-03 | CU-02, CU-03 | C-05 | `ValidadorFondos` | CP-02, CP-03, CP-05 | CA-02, CA-03, CA-05 |
| **RF-05** | Evitar duplicados | RB-05 | CU-02, CU-03 | C-05 | `ValidadorFondos`, `HistorialRepository` | CP-04 | CA-04 |
| **RF-06** | Procesar transferencias | RB-04, RB-07 | CU-02 | C-06 | `ProcesadorTransaccion`, `Cuenta` | CP-01 | CA-01 |
| **RF-07** | Registrar transacciones | RB-06 | CU-02, CU-03 | C-08 | `HistorialRepository`, `Transaccion` | CP-01 | CA-01 |
| **RF-08** | Consultar historial | RB-06 | CU-04 | C-04, C-08 | `ConsultaService`, `HistorialRepository` | CP-08, CP-09 | CA-08, CA-09 |
| **RF-09** | Gestionar errores | RB-06, RB-07 | CU-03 | C-02, C-05 | `TransferenciaService`, `ValidadorFondos` | CP-02, CP-03, CP-05 | CA-02, CA-03, CA-05 |

---

## 2.1 Vista gráfica — cadena de trazabilidad por capa

El siguiente diagrama muestra la trazabilidad completa como un flujo de izquierda a derecha: cada requerimiento se conecta con su caso de uso, su diseño (componente/clase), su caso de prueba y su criterio de aceptación. Permite seguir visualmente cualquier cadena de extremo a extremo.

```mermaid
flowchart LR
    subgraph REQ["Requerimientos"]
        RF01["RF-01 Crear cuentas"]
        RF03["RF-03 Solicitar transf."]
        RF04["RF-04 Validar transf."]
        RF05["RF-05 Evitar duplicados"]
        RF06["RF-06 Procesar transf."]
        RF07["RF-07 Registrar transac."]
        RF08["RF-08 Consultar historial"]
    end
    subgraph CU["Casos de uso"]
        CU01["CU-01"]
        CU02["CU-02"]
        CU03["CU-03"]
        CU04["CU-04"]
    end
    subgraph DIS["Diseño (componentes)"]
        C03C07["C-03 / C-07 Cuentas"]
        C01C02["C-01 / C-02 Transferencia"]
        C05["C-05 Validación"]
        C06["C-06 Proceso atómico"]
        C08["C-08 Historial"]
        C04["C-04 Consulta"]
    end
    subgraph PRU["Pruebas"]
        CP06["CP-06 / CP-07"]
        CP01["CP-01"]
        CP0235["CP-02/03/05"]
        CP04["CP-04"]
        CP0809["CP-08 / CP-09"]
    end
    subgraph ACE["Criterios"]
        CA0607["CA-06 / CA-07"]
        CA01["CA-01"]
        CA0235["CA-02/03/05"]
        CA04["CA-04"]
        CA0809["CA-08 / CA-09"]
    end

    RF01 --> CU01 --> C03C07 --> CP06 --> CA0607
    RF03 --> CU02 --> C01C02 --> CP01 --> CA01
    RF06 --> CU02
    RF06 --> C06 --> CP01
    RF07 --> CU02
    RF07 --> C08 --> CP01
    RF04 --> CU03 --> C05 --> CP0235 --> CA0235
    RF05 --> CU03
    RF05 --> C05
    RF05 --> CP04 --> CA04
    RF08 --> CU04 --> C04 --> CP0809 --> CA0809
    C08 --> CP0809
```

---

## 3. Trazabilidad de requerimientos no funcionales

| RNF | Atributo | Se garantiza en (componente/clase) | Se verifica en |
|-----|----------|------------------------------------|----------------|
| RNF-01 | Consistencia (atomicidad) | C-06 `ProcesadorTransaccion` (transacción ACID) | CP-01, CP-02 |
| RNF-02 | Confiabilidad | C-02 `TransferenciaService` (resultado determinable, idempotencia) | CP-04 |
| RNF-03 | Seguridad | C-01 API (autenticación/autorización por rol) | CP-08 (permisos) |
| RNF-04 | Integridad y trazabilidad | C-08 `HistorialRepository` (referencia única + estado) | CP-01, CP-08 |
| RNF-07 | Mantenibilidad | C-05 dominio aislado + C-09 anticorrupción | (revisión de diseño) |
| RNF-08 | Privacidad | C-04 `ConsultaService` (consulta según permisos) | CP-08 |

### 3.1 Vista gráfica — atributos de calidad

```mermaid
flowchart LR
    RNF01["RNF-01 Consistencia"] --> G1["C-06 Transacción ACID"] --> V1["CP-01, CP-02"]
    RNF02["RNF-02 Confiabilidad"] --> G2["C-02 Idempotencia"] --> V2["CP-04"]
    RNF03["RNF-03 Seguridad"] --> G3["C-01 Auth por rol"] --> V3["CP-08"]
    RNF04["RNF-04 Trazabilidad"] --> G4["C-08 Referencia única"] --> V4["CP-01, CP-08"]
    RNF07["RNF-07 Mantenibilidad"] --> G7["C-05 + C-09 aislamiento"] --> V7["Revisión de diseño"]
    RNF08["RNF-08 Privacidad"] --> G8["C-04 Consulta por permisos"] --> V8["CP-08"]

    style RNF01 fill:#ffe6cc,stroke:#d79b00
    style RNF02 fill:#ffe6cc,stroke:#d79b00
    style RNF03 fill:#ffe6cc,stroke:#d79b00
    style RNF04 fill:#ffe6cc,stroke:#d79b00
    style RNF07 fill:#ffe6cc,stroke:#d79b00
    style RNF08 fill:#ffe6cc,stroke:#d79b00
```

> Cada atributo de calidad se lee: **se exige** (RNF) → **se garantiza en** (componente) → **se verifica en** (prueba).

---

## 4. Cobertura de casos de uso

| Caso de uso | RF cubiertos | Escenarios de prueba | Estado |
|-------------|--------------|----------------------|--------|
| CU-01 Crear cuenta | RF-01, RF-02 | CP-06 (normal), CP-07 (error) | ✅ Cubierto |
| CU-02 Realizar transferencia | RF-03, RF-04, RF-06, RF-07 | CP-01 (normal), CP-02 (alterno), CP-03/CP-04/CP-05 (error) | ✅ Cubierto |
| CU-03 Rechazar inválida/duplicada | RF-04, RF-05, RF-09 | CP-02, CP-03, CP-04, CP-05 | ✅ Cubierto |
| CU-04 Consultar historial | RF-08 | CP-08 (normal), CP-09 (alterno) | ✅ Cubierto |

### 4.1 Vista gráfica — cobertura de pruebas por caso de uso

```mermaid
flowchart LR
    CU01["CU-01 Crear cuenta"]
    CU02["CU-02 Realizar transferencia"]
    CU03["CU-03 Rechazar inválida/duplicada"]
    CU04["CU-04 Consultar historial"]

    CU01 --> N1["CP-06 Normal"]
    CU01 --> E1["CP-07 Error"]
    CU02 --> N2["CP-01 Normal"]
    CU02 --> A2["CP-02 Alterno"]
    CU02 --> E2["CP-03 / CP-04 / CP-05 Error"]
    CU03 --> E3["CP-02 / CP-03 / CP-04 / CP-05"]
    CU04 --> N4["CP-08 Normal"]
    CU04 --> A4["CP-09 Alterno"]

    style N1 fill:#e5f4ee,stroke:#1b9e77
    style N2 fill:#e5f4ee,stroke:#1b9e77
    style N4 fill:#e5f4ee,stroke:#1b9e77
    style A2 fill:#e8f1fb,stroke:#2b6cb0
    style A4 fill:#e8f1fb,stroke:#2b6cb0
    style E1 fill:#fdecea,stroke:#c0392b
    style E2 fill:#fdecea,stroke:#c0392b
    style E3 fill:#fdecea,stroke:#c0392b
```

> Verde = escenario normal · Azul = alterno · Rojo = error. Cada caso de uso tiene cobertura de prueba en los tipos que le aplican.

---

## 5. Verificación de integridad de la trazabilidad

- **Todos los RF (RF-01..RF-09)** tienen al menos un caso de uso, un componente, una clase, un caso de prueba y un criterio de aceptación asociados.
- **Todos los casos de uso (CU-01..CU-04)** están cubiertos por escenarios normal, alterno y/o error.
- **Todos los componentes (C-01..C-09)** aparecen referenciados por al menos un requerimiento.
- **Todas las clases de diseño** del diagrama de clases están ligadas a un componente y a un requerimiento.
- **Todos los casos de prueba (CP-01..CP-09)** tienen su criterio de aceptación verificable correspondiente.

> La cadena `Requerimiento → Caso de uso → Diseño → Prueba` está completa y sin eslabones huérfanos. El proyecto es internamente coherente y defendible de extremo a extremo.
