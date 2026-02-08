# Glosario Crítico
**(El Vocabulario de la Ingeniería de la Evidencia)**

### Introducción: El Contrato Semántico

Este anexo define el léxico operativo de la **"Gobernanza de Datos Defensiva"**. En la industria tecnológica, términos como "Gobernanza", "Inteligencia Artificial" o "Cumplimiento" han sido secuestrados por el marketing para vender humo. Este glosario no busca definiciones académicas, sino definiciones de **supervivencia legal y técnica**.

Aquí redefinimos conceptos blandos con rigor de código.
**Este glosario no es sugerencia: es la sintaxis del sistema.**
Quien no use estos términos con estas definiciones, está operando bajo deuda técnica y riesgo legal.

---

### Léxico de "Gobernanza de Datos Defensiva"

**Airlock (Esclusa de Datos)**

* **Definición:** Zona de cuarentena arquitectónica donde los datos entrantes son validados, sanitizados y etiquetados antes de permitírseles el ingreso al *Data Lake* productivo. Si un dato no pasa el Airlock, no existe para la organización.
* **Referencia Principal:** Capítulo 10 / Anexo F.

**Alucinación**

* **Definición:** Fenómeno probabilístico donde un modelo de IA Generativa inventa información con alta confianza sintáctica pero nula validez fáctica. En este marco, no es un "error curioso", es un fallo crítico de integridad que debe ser mitigado por arquitectura (RAG).
* **Referencia Principal:** Capítulo 09.

**Arquitectura Defendible**

* **Definición:** Arquitectura de datos y sistemas diseñada no para maximizar eficiencia o innovación, sino para resistir auditorías, litigios y fiscalizaciones técnicas adversas, produciendo evidencia verificable bajo escrutinio externo.
* **Referencia Principal:** Capítulo 15 / Anexos D–F.

**Arquitectura de la Evidencia**

* **Definición:** El conjunto de controles técnicos, criptográficos y legales que fuerzan a un sistema a mantener la integridad y trazabilidad de los datos, garantizando que sean admisibles como prueba forense ante una fiscalización.
* **Referencia Principal:** Prólogo / Ideas Centrales.

**BYOK (Bring Your Own Key)**

* **Definición:** Protocolo de soberanía donde la organización retiene las llaves criptográficas maestras, impidiendo que el proveedor de nube (AWS, Azure, Google) pueda leer los datos almacenados, incluso bajo orden judicial extranjera.
* **Referencia Principal:** Capítulo 04.

**Caja Negra Jurídica**

* **Definición:** Conjunto de registros técnicos inmutables (logs, CDC, snapshots, trazas de acceso) que permiten reconstruir ex-post un incidente, decisión o acceso a datos con valor probatorio. Es la fuente primaria de verdad ante tribunales y fiscalizadores. Lo que no está en la Caja Negra, no ocurrió.
* **Referencia Principal:** Anexo D / Capítulo 15.

**Carga de la Prueba (Invertida)**

* **Definición:** Condición regulatoria en la que la organización debe demostrar activamente que actuó con diligencia técnica, en lugar de que la autoridad pruebe negligencia. La ausencia de evidencia (logs, linaje) se interpreta como falla de control.
* **Referencia Principal:** Capítulo 15 / Anexo F.

**Catalogación (Data Catalog)**

* **Definición:** No es un inventario pasivo. Es el mapa activo de activos de datos que vincula metadatos técnicos (schema) con metadatos de negocio (propiedad) y metadatos legales (base de legitimidad). Sin catálogo, el dato es escombro.
* **Referencia Principal:** Capítulo 07 / Anexo B.

**Checklist como Acto de Gobierno**

* **Definición:** Uso de instrumentos técnicos (como el Anexo E) no como herramientas operativas, sino como actos formales de advertencia, escalamiento y transferencia consciente de riesgo hacia la Alta Dirección.
* **Referencia Principal:** Anexo E.

**Consentimiento Computable**

* **Definición:** Estado técnico (`boolean`) asociado a un registro de datos que habilita o bloquea su procesamiento en tiempo real. A diferencia del "consentimiento legal" (papel), este actúa como un *gate* lógico en el pipeline ETL.
* **Referencia Principal:** Capítulo 11 / Anexo F.

**Crypto-Shredding**

* **Definición:** Técnica de borrado verificable que consiste en destruir las llaves criptográficas que protegen un dato, volviéndolo matemáticamente irrecuperable sin necesidad de borrar físicamente cada copia. Constituye el mecanismo técnico más defendible para demostrar cumplimiento del derecho de supresión.
* **Referencia Principal:** Anexo C / Anexo F.

**Data Mesh (Malla de Datos)**

* **Definición:** Arquitectura federada donde la propiedad del dato se descentraliza a los dominios de negocio, pero la gobernanza y los estándares de seguridad se mantienen centralizados y obligatorios.
* **Referencia Principal:** Capítulo 13.

**Datos Tóxicos**

* **Definición:** Datos personales almacenados sin una base legal trazable (contrato, consentimiento o ley) o cuyo periodo de retención ha expirado. Bajo la Ley 21.719, su mera existencia constituye un pasivo sancionable.
* **Referencia Principal:** Capítulo 01 / Anexo F.

**Dato-Uranio**

* **Definición:** Tesis central que establece que los datos no son un activo libre de riesgo ("petróleo"), sino un material peligroso que genera valor solo bajo estricto confinamiento, y radiactividad (riesgo legal) si se filtra.
* **Referencia Principal:** Capítulo 01 / Prólogo.

**Decisión Automatizada**

* **Definición:** Cualquier resultado generado total o parcialmente por un sistema algorítmico que influye, condiciona o justifica una acción, omisión o priorización relevante. La etiqueta “solo informativo” no excluye impacto decisional ni responsabilidad legal.
* **Referencia Principal:** Capítulo 11 / Anexo F.

**Deuda Técnica Legal**

* **Definición:** La acumulación de procesos de datos que operan al margen de la regulación actual (ej: tablas sin dueño, scripts sin logs, modelos sin EIPD). Esta deuda se paga con multas y desprestigio.
* **Referencia Principal:** Prólogo / Anexo E.

**EIPD (Evaluación de Impacto en Protección de Datos)**

* **Definición:** En este marco, no es un documento legal, sino un *Pipeline Gate* en CI/CD. Proceso obligatorio que bloquea el despliegue de software si no se ha medido y mitigado el riesgo para los derechos de los titulares.
* **Referencia Principal:** Anexo F / Capítulo 11.

**ETL-V (Extract, Transform, Load, VERIFY)**

* **Definición:** Evolución del pipeline tradicional de datos que agrega una etapa obligatoria de verificación criptográfica y de calidad antes de considerar el dato como cargado.
* **Referencia Principal:** Capítulo 05.

**Evidencia Sistémica**

* **Definición:** Evidencia generada automáticamente por la operación normal del sistema (logs, commits, hashes, linaje), no producida ad-hoc para responder a una auditoría. Tiene prioridad técnica sobre declaraciones o entrevistas.
* **Referencia Principal:** Anexo D / Capítulo 15.

**Fricción Estratégica**

* **Definición:** Introducción deliberada de controles, validaciones y bloqueos técnicos que ralentizan acciones de alto riesgo. La fricción no es un costo político, sino un mecanismo de seguridad para evitar daño sistémico.
* **Referencia Principal:** Epílogo / Capítulo 15.

**Gobernanza como Código (Governance as Code)**

* **Definición:** La práctica de implementar políticas de cumplimiento (privacidad, seguridad, retención) directamente en la infraestructura y el software, en lugar de en manuales de procedimiento.
* **Referencia Principal:** Capítulo 02 / Capítulo 11.

**Gobernanza Defensiva**

* **Definición:** Modelo de gobernanza orientado prioritariamente a reducir exposición legal, regulatoria y reputacional, incluso a costa de eficiencia operativa. No busca “alinear a las personas”, sino hacer el error técnicamente difícil.
* **Referencia Principal:** Todo el libro.

**Human-in-the-Loop (HITL)**

* **Definición:** Mecanismo de seguridad donde un sistema de IA detiene su ejecución y solicita intervención humana antes de tomar una decisión de alto impacto (Zona Roja).
* **Referencia Principal:** Capítulo 15 / Anexo F.

**Incidente de Gobernanza**

* **Definición:** Evento en el que un dato crítico es creado, modificado, usado o expuesto fuera de los controles definidos (ej: KPI usado en Directorio sin definición certificada), aun cuando no exista brecha de seguridad inmediata.
* **Referencia Principal:** Anexo B / Anexo E.

**Inmutabilidad**

* **Definición:** Propiedad de un registro (log) que garantiza matemáticamente que no ha sido modificado desde su creación. Es la base de la defensa forense ante la Agencia.
* **Referencia Principal:** Anexo D.

**Kill Switch (Botón Rojo)**

* **Definición:** Mecanismo de aislamiento de emergencia que permite revocar accesos, cortar integraciones y congelar el estado del sistema ante un ataque activo o riesgo legal inminente. Su activación es excepcional, trazada y sujeta a revisión ex-post.
* **Referencia Principal:** Anexo D / Capítulo 15.

**Legal Engineering**

* **Definición:** Disciplina que traduce obligaciones legales abstractas en controles técnicos ejecutables (código, infraestructura, pipelines), eliminando la dependencia exclusiva de políticas declarativas. No interpreta la ley; la implementa.
* **Referencia Principal:** Anexo D / Anexo F.

**Linaje de Datos (Data Lineage)**

* **Definición:** La traza completa del ciclo de vida de un dato, desde su origen hasta su consumo. Responde a la pregunta: "¿De dónde salió este número y quién lo modificó?". Sin linaje, no hay evidencia.
* **Referencia Principal:** Capítulo 05 / Anexo E.

**Logs Inmutables (WORM)**

* **Definición:** Registros almacenados bajo un modelo *Write Once – Read Many* que impide su modificación o eliminación incluso por usuarios privilegiados. Constituyen la base técnica exigible de admisibilidad probatoria frente a la Agencia o tribunales.
* **Referencia Principal:** Anexo D.

**Masa Crítica de Riesgo**

* **Definición:** Punto a partir del cual la acumulación de datos no gobernados, deuda técnica y automatización produce una reacción en cadena de riesgo legal y operacional. Equivalente nuclear del “dato-uranio”.
* **Referencia Principal:** Prólogo / Capítulo 01.

**Océano No-Estructurado**

* **Definición:** El 80% de la información corporativa (correos, PDFs, chats, imágenes) que escapa a las bases de datos relacionales y representa el mayor riesgo de fuga y el mayor desafío de gobernanza.
* **Referencia Principal:** Capítulo 08.

**Override Ejecutivo**

* **Definición:** Decisión explícita y documentada de la Alta Dirección de continuar una operación en contra de la recomendación técnica, aceptando formalmente el riesgo residual. Protege al rol técnico al dejar trazabilidad.
* **Referencia Principal:** Anexo A / Anexo E.

**Privacy by Design (Privacidad por Diseño)**

* **Definición:** Ingeniería preventiva. Significa que la privacidad es la configuración por defecto del sistema y que las medidas de protección se integran en la arquitectura desde el día cero, no como un parche posterior.
* **Referencia Principal:** Capítulo 11.

**RAG (Retrieval-Augmented Generation)**

* **Definición:** Arquitectura cognitiva que obliga a un LLM (modelo de lenguaje) a consultar una base de conocimientos verificada (Vector DB) antes de generar una respuesta, reduciendo la alucinación.
* **Referencia Principal:** Capítulo 09.

**Realidad Sintética**

* **Definición:** Entorno informacional donde una proporción significativa de los contenidos y decisiones es generada por IA, dificultando distinguir entre hechos, inferencias y alucinaciones. Hace de la "Verdad Operativa" un activo estratégico.
* **Referencia Principal:** Epílogo / Capítulo 09.

**Responsabilidad Proactiva (Accountability)**

* **Definición:** Principio jurídico-técnico que invierte la carga de la prueba. La organización debe ser capaz de *demostrar* técnicamente que cumple la ley, no solo declarar que la cumple.
* **Referencia Principal:** Anexo F / Capítulo 15.

**Separación de Poderes**

* **Definición:** Principio de diseño organizacional que prohíbe que la persona que diseña y explota los datos (CDO) sea la misma que audita su cumplimiento legal (DPO).
* **Referencia Principal:** Capítulo 16.

**Shadow AI**

* **Definición:** Uso de modelos, APIs o plataformas de IA no autorizadas (cuentas personales, SaaS no gobernados) para procesar datos corporativos o sensibles. Implica fuga irreversible de información y decisiones no trazables.
* **Referencia Principal:** Anexo E / Anexo F.

**Shadow IT (TI en las Sombras)**

* **Definición:** Cualquier infraestructura, software o base de datos desplegada por unidades de negocio sin el conocimiento, control o aprobación del área de TI/Seguridad. Es la principal fuente de fugas de datos.
* **Referencia Principal:** Capítulo 07 / Anexo E.

**SSOT (Single Source of Truth - Fuente Única de Verdad)**

* **Definición:** El único repositorio autorizado donde reside un dato maestro. Cualquier otra copia en la organización es, por definición, una copia obsoleta o corrupta que debe ser eliminada.
* **Referencia Principal:** Capítulo 06.

**Transferencia de Riesgo (Formal)**

* **Definición:** Acto explícito mediante el cual la Alta Dirección asume un riesgo técnico previamente advertido, dejando constancia escrita de que la decisión excede la recomendación profesional. Libera al rol técnico de responsabilidad funcional.
* **Referencia Principal:** Anexo A / Anexo E.

**TTL (Time-To-Live)**

* **Definición:** Metadato que define la fecha de caducidad automática de un registro de datos. Implementar TTL es la única forma técnica de cumplir con el principio de "Limitación del Plazo de Conservación".
* **Referencia Principal:** Capítulo 11 / Anexo F.

**Vector Database (Base de Datos Vectorial)**

* **Definición:** Almacén de datos especializado en guardar el "significado" (embeddings) del texto, permitiendo búsquedas semánticas. Es la memoria a largo plazo de la IA corporativa.
* **Referencia Principal:** Capítulo 09.

**Verdad Forense**

* **Definición:** Estado del dato reconstruido a partir de evidencia sistémica inmutable (logs, CDC), no de declaraciones ni narrativas posteriores. Puede diferir de la verdad operativa y prevalece en contextos judiciales.
* **Referencia Principal:** Anexo D / Capítulo 15.

**Verdad Operativa (Ground Truth)**

* **Definición:** Conjunto mínimo de datos, definiciones y evidencias que la organización reconoce como factualmente válidos y legalmente defendibles. No emerge espontáneamente; debe ser construida y protegida.
* **Referencia Principal:** Epílogo / Capítulo 06 / Anexo B.