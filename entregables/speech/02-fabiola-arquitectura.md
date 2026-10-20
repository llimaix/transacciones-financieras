# Speech de exposición — Fabiola

### Arquitectura y Diseño de Componentes

> **Tiempo sugerido:** 4–5 minutos
> **Orden en la presentación:** 2.º (después de requerimientos)

---

## Qué mostrar en pantalla
Diagrama de arquitectura AWS, diagrama de capas y el catálogo de componentes C-01..C-09.

---

## Guion

**Apertura (la decisión).**
"Gracias, Astrid. Mi parte es la arquitectura. Elegimos una arquitectura en capas con un núcleo de dominio transaccional, desplegada en AWS. El principio que guía todo es uno solo: la transferencia, es decir el débito y el crédito, ocurre como una única transacción atómica sobre una sola base de datos. Eso es lo que garantiza que nunca se pierda ni se cree dinero."

**Por qué capas y no otra cosa.**
"No llegamos a esta decisión por descarte rápido; evaluamos alternativas con seriedad. Consideramos microservicios, que es una arquitectura muy potente, pero para este caso repartir el débito y el crédito entre servicios separados añadiría un riesgo de inconsistencia que preferimos evitar. También valoramos la arquitectura hexagonal pura, que es muy elegante; tomamos su mejor idea —aislar el núcleo del negocio— y la aplicamos sin sumar una complejidad que esta fase no necesita. En resumen, elegimos lo que mejor equilibra robustez y simplicidad para su problema."

**El despliegue en AWS.**
"Mapeamos cada capa a un servicio de AWS: API Gateway y un balanceador en la entrada, Cognito para autenticación, los contenedores de la lógica en ECS Fargate, y la base de datos en RDS PostgreSQL, que da transacciones ACID nativas. La integración con los sistemas internos del banco va por una VPN sitio a sitio."

**Por qué Fargate y no un servidor EC2.**
"También elegimos con cuidado dónde corre la aplicación. Los servidores EC2 nos darían más control, pero con la responsabilidad de parchearlos y asegurarlos, algo que en un sistema financiero preferimos no cargar sobre su equipo. Lambda es muy ágil, pero las transacciones de larga vida no se acomodan bien a su modelo. Fargate nos da el mejor punto medio: la potencia de los contenedores sin la carga de administrar servidores, para que ustedes se concentren en el negocio y no en la infraestructura."

**La opción on-premise (demuestra madurez).**
"También dejamos documentada la versión on-premise de la misma arquitectura, por si el banco tiene requisitos regulatorios de soberanía de datos. Como la lógica va en contenedores, el mismo sistema corre en la nube o en su centro de datos. No quedamos casados con un proveedor."

**Componentes.**
"Dividimos el sistema en nueve componentes, de C-01 a C-09, cada uno con una sola responsabilidad. El más importante es el C-06, el procesador de transacción atómica: es el único componente que modifica saldos, y siempre dentro de una transacción. Concentrar eso en un solo punto hace que la consistencia sea fácil de garantizar y de auditar."

**Transición a Wuilli.**
"Con los componentes definidos, Wuilli muestra cómo se modelan en UML."

---

## Preguntas probables y cómo responder

- **¿Por qué una base de datos relacional y no NoSQL?**
  "Las bases NoSQL son excelentes para otros escenarios, como alto volumen de lectura. Para este caso elegimos relacional porque el manejo de dinero exige transacciones que toquen varios registros a la vez con total garantía, y eso las relacionales lo ofrecen de forma nativa. Es la opción que más protege sus saldos."

- **¿Qué pasa si falla la transferencia a la mitad?**
  "Esa es justamente la situación que más cuidamos. Si algo falla, el sistema revierte todo automáticamente: o se aplican el débito y el crédito juntos, o no se aplica ninguno. Nunca queda un saldo a medias, bajo ninguna circunstancia."

- **¿No sería más moderno usar microservicios?**
  "Es una muy buena pregunta, y de hecho los consideramos seriamente. Son una arquitectura excelente para muchos escenarios. Para el suyo, donde lo primero es proteger el dinero, los microservicios reparten la operación entre varios servicios y eso añade un riesgo de inconsistencia que preferimos evitar. Elegimos la opción que da más garantías en lo que para ustedes es crítico; si en el futuro el sistema crece, la arquitectura permite evolucionar hacia ese modelo."
