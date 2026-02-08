# Anexo E: Checklist de Supervivencia del CDO (Primeros 90 Días)

> **CLASIFICACIÓN:** CONFIDENCIAL / USO EXCLUSIVO CDO

> **OBJETIVO:** DIAGNÓSTICO BINARIO DE INTEGRIDAD ARQUITECTÓNICA

> **DESTINATARIO:** COMITÉ DE RIESGOS / DIRECTORIO

> **INSTRUCCIÓN:** ESTE DOCUMENTO NO ACEPTA "EN PROCESO". SOLO ADMITE "SÍ" (EVIDENCIA DISPONIBLE) O "NO" (RIESGO ACTIVO).

---

## 1. PRINCIPIO DE USO (CLAÚSULA DE SALVAGUARDA)

Este checklist no mide el "cumplimiento legal" (tarea de abogados). Mide la **desviación técnica** entre la realidad operativa y la arquitectura de defensa necesaria.

**Momento de Corte:**
El estado consignado en este checklist corresponde exclusivamente a la evidencia disponible al **momento exacto de su firma**. Cualquier avance posterior no altera retroactivamente el diagnóstico emitido.

**Alcance Probatorio del Diagnóstico:**
Este checklist constituye una herramienta de diagnóstico interno de riesgos. La identificación de un “NO” no implica incumplimiento legal, negligencia profesional ni responsabilidad individual del CDO, sino la detección temprana de una brecha técnica que debe ser evaluada y priorizada por la Administración Superior.

**Exención de Responsabilidad (Deber de Advertencia):**
El levantamiento y comunicación de estos riesgos constituye el cumplimiento del **Deber de Advertencia** por parte del CDO. La decisión corporativa de continuar operando con estos riesgos abiertos **traslada la decisión informada sobre la asunción del riesgo a la Administración Superior**. La continuidad operacional posterior a este diagnóstico, sin mitigación efectiva de los riesgos identificados, constituye una decisión de gestión ajena al rol técnico del CDO.

**Criterio de Evidencia:**
Un “SÍ” solo es válido si la evidencia es actual, verificable, trazable y reproducible. La validación de la evidencia corresponde al CDO en base a criterios técnicos objetivos definidos en los Anexos A–D. **La presión jerárquica o las interpretaciones laxas no constituyen evidencia válida.**

**Obligación del Receptor:**
La recepción formal de este documento (mediante acta o minuta) implica la obligación del órgano destinatario de deliberar, priorizar y dejar constancia expresa de la aceptación, mitigación o transferencia del riesgo identificado.

---

## 2. FUNDAMENTOS DE INFRAESTRUCTURA (EL MAPA)

*Nota: Este documento no acepta estados intermedios ("EN PROCESO") al momento del diagnóstico. La planificación de mitigaciones se gestiona fuera de este instrumento.*

| ID | Control de Integridad | Estado (SÍ/NO) | Evidencia Requerida (Si es SÍ) |
| :--- | :--- | :--- | :--- |
| **I.1** | ¿Existe un inventario automatizado de activos de datos (Tablas, Buckets, Topics)? | [ ] | Link al Catálogo de Datos vivo (no Excel). |
| **I.2** | ¿Podemos identificar técnicamente qué procesos escriben en cada tabla crítica (Linaje)? | [ ] | Gráfico de dependencia (DAG) de Airflow/dbt. |
| **I.3** | ¿Están separados físicamente los entornos de Desarrollo y Producción? | [ ] | IAM Policies diferenciadas por cuenta/proyecto. |
| **I.4** | ¿Existe un mecanismo de "Kill Switch" probado, documentado y con control de activación conforme al **Anexo D**? | [ ] | Procedimiento + Log de simulacro + Roles habilitados. |

---

## 3. GOBERNANZA Y PROPIEDAD (EL MANDO)

| ID | Control de Autoridad | Estado (SÍ/NO) | Evidencia Requerida (Si es SÍ) |
| :--- | :--- | :--- | :--- |
| **G.1** | ¿Tienen dueño formal (Data Owner) todos los activos clasificados como L2/L3? | [ ] | Metadato `owner` en el catálogo. |
| **G.2** | ¿Existe un proceso de "Airlock" que impida la ingesta de datos sin esquema validado? | [ ] | Configuración del pipeline (Schema Registry/Tests). |
| **G.3** | ¿Están definidos y versionados los KPIs críticos (o el conjunto mínimo definido formalmente) en el Diccionario Oficial? | [ ] | Link al Anexo B (Diccionario) con artefacto de ejecución. |
| **G.4** | ¿Existe un procedimiento de resolución de conflictos semánticos con SLA definido? | [ ] | Acta de constitución del Comité de Datos / GRC. |

---

## 4. DEFENSA LEGAL Y PRIVACIDAD (EL ESCUDO)

| ID | Control de Derechos | Estado (SÍ/NO) | Evidencia Requerida (Si es SÍ) |
| :--- | :--- | :--- | :--- |
| **L.1** | ¿Están clasificados todos los datos con etiquetas de sensibilidad (L0-L3)? | [ ] | Reporte de cobertura de tags. |
| **L.2** | ¿Existe capacidad técnica para ejecutar un "Borrado Lógico" (Crypto-shredding)? | [ ] | Demo técnica o script de borrado de llaves. |
| **L.3** | ¿Se gestiona el consentimiento como una variable de estado que bloquea flujos? | [ ] | Código que consulta el estado del consentimiento antes del ETL. |
| **L.4** | ¿Están los logs de auditoría en almacenamiento inmutable (WORM)? | [ ] | Configuración de Object Lock en S3/Storage. |

---

## 5. INTELIGENCIA ARTIFICIAL Y VECTORES (FRONTERA EMERGENTE)

| ID | Control Cognitivo | Estado (SÍ/NO) | Evidencia Requerida (Si es SÍ) |
| :--- | :--- | :--- | :--- |
| **A.1** | ¿Heredan los vectores (Embeddings) los permisos de acceso del documento original? | [ ] | Test de ACL en la Vector DB. |
| **A.2** | ¿Existe un filtro de sanitización (PII/Toxicidad) antes de la vectorización? | [ ] | Logs del servicio de DLP en la ingesta. |
| **A.3** | ¿Es posible trazar qué fragmentos (Chunks) usó el modelo para una respuesta específica? | [ ] | Log de respuesta incluyendo `source_documents`. |
| **A.4** | ¿Existe un inventario y mecanismo de bloqueo o mitigación de "Shadow AI" (cuentas de OpenAI/SaaS no corporativas)? | [ ] | Reporte de CASB / Firewall / Bloqueo técnico documentado. |

> **Nota de Riesgo Crítico:** Un “NO” en A.4 implica exposición directa a fuga de información confidencial, decisiones no gobernadas y responsabilidad indirecta por uso de herramientas no autorizadas.

---

## 6. RESUMEN DE ESTADO (SCORECARD)

* **Cobertura de Integridad:** ____ % (SÍ / Total)
* **Nivel de Riesgo Arquitectónico:**
    * [ ] **CRÍTICO:** < 50% (La organización opera a ciegas).
    * [ ] **VULNERABLE:** 50-80% (Defensa parcial, riesgo legal activo).
    * [ ] **DEFENDIBLE:** > 80% (Debida diligencia demostrable).

**Criterio de Acción Esperado:**

* **CRÍTICO:** Requiere plan de contención inmediato y sesión extraordinaria de riesgos.
* **VULNERABLE:** Requiere priorización formal y seguimiento trimestral.
* **DEFENDIBLE:** Requiere monitoreo continuo.

> **Nota de Cierre:** Este documento es una fotografía del estado del arte técnico al momento de la firma. Los "NO" representan deuda técnica que se asume conscientemente como **Riesgo Operacional**.

<br>
<br>

__________________________
**Firma del CDO**

*Nota: La firma del CDO acredita la emisión del diagnóstico y su comunicación formal, no la conformidad con el estado resultante, ni la validación de suficiencia, ni la aceptación de la exposición al riesgo residual.*
*Fecha del Diagnóstico:*