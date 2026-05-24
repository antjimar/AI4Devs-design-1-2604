# Prompts utilizados — LTI · Diseño del Sistema ATS

> Documento complementario a `LTI-AJM.md`
> Autor: Antonio Jiménez Martínez (AJM)
> Asistente: Claude
> Master AI4Devs · Módulo 4

Los prompts están ordenados por fase del proceso de diseño. Cada uno sigue la estructura **rol → contexto → tarea → formato esperado** y suele encadenarse con el resultado del anterior.

---

## Fase 1 · Descripción del producto y propuesta de valor

### Prompt 1.1 — Discovery del dominio ATS

```
Actúa como Product Manager senior con experiencia en HRTech.

Estoy diseñando LTI, un ATS (Applicant Tracking System) SaaS B2B
multi-tenant con IA integrada. Antes de definir nada, necesito asentar
el contexto del dominio:

1. ¿Cuáles son las funcionalidades nucleares que debe cubrir cualquier
   ATS moderno? Ordénalas por criticidad para una v1.
2. ¿Qué dolores específicos tiene un departamento de RRHH de una
   empresa mediana (50–500 empleados) al gestionar procesos de selección?
3. ¿Qué hace que un ATS sea "del futuro" frente a uno tradicional?
   Cita ejemplos concretos.
4. ¿Cómo se diferencian los líderes actuales (Greenhouse, Workday,
   Lever, Recruitee) entre sí?

Sé concreto y evita generalidades de marketing.
```

### Prompt 1.2 — Definición de valor añadido y ventajas competitivas

```
A partir del análisis anterior, ayúdame a redactar para el documento
final dos bloques:

A) **Descripción de LTI** (4–6 líneas) que deje claro:
   - Qué es (categoría de producto).
   - Para quién (segmento principal).
   - Qué problema resuelve.
   - Qué lo diferencia (en una sola frase).

B) **Tabla comparativa de ventajas competitivas** frente a la
competencia típica, en 5–7 ejes (IA, colaboración, pricing,
time-to-value, apertura, cumplimiento normativo…).

Tono profesional pero directo. Sin superlativos vacíos.
```

---

## Fase 2 · Funciones principales

### Prompt 2.1 — Listado de funciones principales agrupadas

```
El enunciado del ejercicio menciona 4 ejes clave que harán brillar a LTI:
- Eficiencia para los departamentos de HR
- Colaboración en tiempo real entre reclutadores y managers
- Automatizaciones
- Asistencia de IA en diversas tareas

Quiero que estructures las funcionalidades principales del sistema
agrupándolas exactamente en esos 4 ejes. Para cada eje:

- 4–6 funcionalidades concretas
- Una frase explicando qué hace cada una (no más)
- Evita repeticiones entre ejes

El resultado debe poder usarse tal cual en el documento de diseño.
```

---

## Fase 3 · Lean Canvas

### Prompt 3.1 — Construcción del Lean Canvas

```
Genera el Lean Canvas de LTI con sus 9 bloques completos:
1. Problema (top 3) + alternativas existentes
2. Segmentos de cliente (early adopters + core + secundario)
3. Propuesta única de valor + high-level concept
4. Solución
5. Métricas clave
6. Canales
7. Estructura de costes
8. Fuentes de ingreso
9. Ventaja especial (unfair advantage)

Contexto: ATS SaaS B2B multi-tenant con IA nativa, dirigido a empresas
medianas tech y de servicios (50–500 empleados) y, secundariamente,
agencias de selección.

Devuélvelo en formato compatible con Mermaid si es posible (flowchart
TB con subgraphs por fila para imitar el layout clásico de Lean Canvas),
o como tabla Markdown bien estructurada si Mermaid no permite un
resultado legible.
```

---

## Fase 4 · Casos de uso

### Prompt 4.1 — Identificación de casos de uso principales

```
Actúa como analista de software experto en sistemas de RRHH.

Para una primera versión funcional de LTI, identifica los 3 casos de
uso más importantes — los que, si funcionan, hacen que el producto
sea viable y suficiente para un cliente piloto.

Para cada caso de uso indica:
- Identificador (CU-01, CU-02, CU-03)
- Título descriptivo
- Actor principal y actores secundarios
- Precondiciones
- Flujo principal numerado paso a paso
- Flujos alternativos relevantes
- Postcondiciones

Los actores disponibles son: Reclutador, Hiring Manager, Entrevistador,
Candidato, Motor de IA, y los sistemas externos Job Boards, Servicios
de Calendario y HRIS.

Los 3 casos de uso deben cubrir entre sí el flujo de "publicar oferta
→ cribar candidatos → contratar".
```

### Prompt 4.2 — Diagramas UML de casos de uso

```
Para cada uno de los 3 casos de uso anteriores, genera el diagrama UML
de casos de uso correspondiente en formato Mermaid.

Requisitos:
- Diferenciar visualmente actores internos (Reclutador, Hiring Manager,
  Entrevistador) y externos (Candidato, Motor IA, Job Boards, Calendario,
  HRIS).
- Usar relaciones <<include>> para flujos obligatorios y <<extend>>
  para flujos opcionales.
- Agrupar los casos de uso dentro de un subgraph "Sistema LTI".
- Sintaxis Mermaid que renderice correctamente en GitHub.

Si Mermaid no soporta nativamente la notación UML de casos de uso al
100%, usa una aproximación con `graph TB`, formas redondeadas para
casos de uso y nodos `([texto])` para actores.
```

---

## Fase 5 · Modelo de datos

### Prompt 5.1 — Entidades esenciales

```
Actúa como arquitecto de software experto en SaaS B2B multi-tenant.

Diseña el modelo de datos de LTI que dé soporte a los 3 casos de uso
definidos. Identifica las entidades imprescindibles, considerando:

- Aislamiento multi-tenant por empresa.
- Roles diferenciados (admin, reclutador, hiring manager, entrevistador).
- Pipeline configurable por oferta.
- Pista de auditoría para decisiones automáticas (EU AI Act).
- Documentos asociados al candidato (CVs, cover letters).
- Resultados del cribado IA como entidad propia.
- Scorecards con criterios ponderados.
- Comentarios y notificaciones.
- Integraciones externas configuradas por empresa.

Para cada entidad lístame:
- Nombre
- Atributos principales con su tipo de dato (UUID, string, text,
  integer, decimal, timestamp, enum(...), jsonb, boolean)
- Marcando PK y FK

Devuélvelo como tabla Markdown para que pueda usarla en el documento.
```

### Prompt 5.2 — Diagrama entidad-relación

```
Con las entidades del prompt anterior, genera el diagrama ER en
formato Mermaid (`erDiagram`).

Requisitos:
- Cardinalidad explícita en cada relación (||--o{, }o--||, ||--||).
- Etiquetas de relación en español, breves y descriptivas.
- Bloque de atributos por entidad con tipo de dato.
- Que renderice limpio en GitHub.

Después del diagrama, añade 3–4 notas de diseño explicando decisiones
no obvias (aislamiento multi-tenant, soft-delete y derecho al olvido,
indexación de búsqueda, trazabilidad de decisiones IA).
```

---

## Fase 6 · Diseño de alto nivel

### Prompt 6.1 — Arquitectura de alto nivel

```
Actúa como arquitecto de software senior especializado en SaaS B2B.

Diseña la arquitectura de alto nivel de LTI considerando estos
requisitos no funcionales:

- Escalado independiente del cribado IA (CPU/GPU bound) respecto al
  resto del sistema.
- Colaboración en tiempo real entre usuarios de la misma empresa
  (presencia, co-edición de scorecards, notificaciones push).
- Integraciones con job boards, calendarios externos y HRIS.
- Envío de notificaciones asíncronas a gran volumen.
- Multi-tenant lógico con posibilidad de aislamiento físico futuro
  para clientes regulados.
- Alta disponibilidad y trazabilidad.

Propón un enfoque **monolito modular + servicios satélite** (no
microservicios completos para v1) y justifícalo brevemente.

Para cada componente del sistema indica:
- Nombre
- Responsabilidad
- Tecnología propuesta (con versión razonable)

Devuélvelo como tabla Markdown + lista de decisiones arquitectónicas
clave (4–6 viñetas).
```

### Prompt 6.2 — Diagrama de arquitectura

```
A partir del listado de componentes anterior, genera el diagrama de
arquitectura del sistema completo en Mermaid (`graph TB`).

Estructúralo en capas mediante subgraphs:
- Capa de clientes
- API Gateway
- Núcleo de la plataforma
- Capa de IA
- Capa de datos
- Sistemas externos

Usa diferentes formas para distinguir tipos de nodo: rectángulos para
servicios, cilindros para bases de datos (`[(...)]`), formas de cola
para mensajería (`[[...]]`), nodos con bordes redondeados para actores.

El diagrama debe poderse leer en una sola página de GitHub.
```

---

## Fase 7 · Diagramas C4

### Prompt 7.1 — Elección del componente para el zoom C4 nivel 3

```
Tengo que profundizar con C4 en uno de los componentes del sistema.
Recomiéndame cuál tiene más sentido para una entrega de máster donde
quiero mostrar:

- Comprensión del patrón C4 (3 niveles bien diferenciados).
- Diseño técnico no trivial (varios subcomponentes, interacciones).
- Alineación con la propuesta de valor diferencial del producto
  (IA integrada).

Valora también qué componente sería más útil documentar como
referencia para el equipo de ingeniería en una v1.
```

### Prompt 7.2 — C4 Nivel 1 (Contexto)

```
Genera el diagrama C4 Nivel 1 (Contexto del Sistema) para LTI.

Usa la sintaxis Mermaid `C4Context`.

Actores internos: Reclutador, Hiring Manager, Entrevistador.
Actor externo: Candidato.

Sistemas externos:
- Job Boards (LinkedIn, Indeed, InfoJobs)
- Servicios de Calendario (Google Calendar, Outlook)
- Proveedor de Email (SendGrid / Amazon SES)
- Proveedores LLM (OpenAI, Anthropic)
- HRIS (BambooHR, Personio, Workday)

Cada relación debe llevar una etiqueta breve en español que explique
qué intercambian el actor/sistema y LTI.
```

### Prompt 7.3 — C4 Nivel 2 (Contenedores)

```
Genera el diagrama C4 Nivel 2 (Contenedores) en Mermaid `C4Container`.

Contenedores a incluir dentro del `System_Boundary("LTI")`:
- Web App (React + Next.js)
- Candidate Portal (React PWA)
- API Gateway (AWS API Gateway + JWT)
- Core ATS Service (Node.js / NestJS)
- AI Screening Service (Python / FastAPI)
- Realtime Service (Node.js / Socket.IO)
- Notification Service (Node.js)
- Workers (BullMQ / Node.js)
- PostgreSQL (+ pgvector)
- Elasticsearch
- Redis
- Object Storage (S3)
- Message Queue (SQS / RabbitMQ)

Sistemas externos: LLM Providers, Job Boards, Email Provider, Calendars.

Cada `Rel(...)` debe incluir descripción y protocolo cuando aplique
(HTTPS, WSS, SQL, S3 API, AMQP).
```

### Prompt 7.4 — C4 Nivel 3 (Componentes del AI Screening Service)

```
Genera el diagrama C4 Nivel 3 (Componentes) del AI Screening Service
en Mermaid `C4Component`.

Este servicio es responsable de:
1. Consumir eventos "candidatura.creada" desde la cola.
2. Parsear CVs (PDF, DOCX) y extraer estructura.
3. Analizar la descripción del puesto y detectar lenguaje sesgado.
4. Generar embeddings semánticos de CV y JD.
5. Calcular similitud por dimensión (skills, experiencia, idiomas).
6. Generar resumen ejecutivo, fortalezas, riesgos y preguntas con LLM.
7. Combinar señales en un score final explicable.
8. Persistir el resultado y emitir "cribado.completado".
9. Registrar la decisión en AuditLog (EU AI Act).

Componentes esperados: REST API Controller, Queue Consumer,
Screening Orchestrator, CV Parser, JD Analyzer, Bias Detector,
Embedding Generator, Similarity Engine, LLM Insights Generator,
Scoring Aggregator, Result Publisher, Vector Store Client,
LLM Gateway, Result Cache, Audit Logger.

Dependencias externas (`Container_Ext` / `ContainerDb_Ext`):
PostgreSQL + pgvector, Object Storage (S3), Redis, Message Queue,
Proveedores LLM.

Tras el diagrama añade:
- Flujo extremo a extremo del cribado (numerado).
- 4–5 decisiones de diseño relevantes (pipeline explicable, LLM
  Gateway como punto único de control, audit logger transversal,
  idempotencia, human-in-the-loop).
```

---

## Fase 8 · Revisión y consolidación

### Prompt 8.1 — Revisión de coherencia entre artefactos

```
Antes de cerrar el documento, revisa la coherencia entre los
artefactos:

- Los actores que aparecen en los casos de uso, ¿están todos
  representados en el C4 Nivel 1?
- Las entidades del modelo de datos, ¿soportan todos los flujos
  descritos en los 3 casos de uso? Identifica cualquier campo
  o entidad que falte.
- Los componentes del diagrama de alto nivel, ¿coinciden con los
  contenedores del C4 Nivel 2?
- Los nombres de entidades, atributos y componentes, ¿son
  consistentes entre todas las secciones (español/inglés, snake_case,
  etc.)?

Devuélveme una lista de inconsistencias encontradas y propuesta de
arreglo para cada una. No me corrijas el documento todavía; quiero
revisar la lista primero.
```

### Prompt 8.2 — Ajustes finales

```
A partir de las inconsistencias que acabamos de identificar, aplica
los siguientes ajustes al documento:

[lista de cambios concretos derivados del prompt anterior]

No reescribas secciones enteras: haz solo las correcciones puntuales
necesarias. Mantén el resto del texto tal como está.
```

---

## Notas sobre la metodología

- Todos los prompts se ejecutaron con **Claude (Opus 4.7)** en una
única sesión, manteniendo el contexto entre fases.
- La estrategia de prompting siguió el patrón **rol + contexto +
tarea + formato esperado**, con prompts cada vez más específicos
conforme se afinaban los artefactos.
- Antes de redactar nada, se realizó una fase de discovery sobre el
dominio del ATS (Prompt 1.1) para asentar el contexto del producto
y del mercado.
- Los diagramas se generaron en **Mermaid** por su compatibilidad con
renderizado nativo en GitHub, lo que evita depender de imágenes
externas y facilita el versionado.

