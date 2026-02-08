# Anexo A: Constitución de los Datos (Data Charter)

> **CLASIFICACIÓN DEL DOCUMENTO:** ESTRATÉGICO / NORMATIVO
> **VIGENCIA:** INMEDIATA A PARTIR DE SU FIRMA
> **ALCANCE:** TODA LA ORGANIZACIÓN (INCLUYENDO FILIALES Y CONTRATISTAS)
> **REFERENCIA:** POLÍTICA DE GOBERNANZA DE DATOS DEFENSIVA

---

## 1. PROPÓSITO Y MANDATO

Este documento establece los principios innegociables que rigen la creación, almacenamiento, uso y eliminación de datos dentro de la Organización. No es una guía de mejores prácticas; es el marco normativo vinculante que define las responsabilidades sobre el activo de información.

**Jerarquía Normativa:**
Este marco se interpreta y aplica en estricta concordancia con la legislación vigente, los contratos laborales individuales o colectivos y el Reglamento Interno de Orden, Higiene y Seguridad. En caso de conflicto normativo, prevalecerá siempre la norma de rango legal superior.

---

## 2. DISPOSICIONES FUNDAMENTALES Y OBLIGATORIAS

### 2.1. Propiedad Institucional y Derechos
**Principio:** Los datos generados, procesados o almacenados en sistemas corporativos son propiedad exclusiva de la Organización, en los términos y límites definidos por la legislación vigente, no de los individuos o departamentos que los crean.

* **Blindaje de Propiedad Intelectual:** Esta propiedad se refiere exclusivamente al **dato como activo informacional estructurado**, y no afecta la autoría intelectual individual ni los derechos morales protegidos por la legislación laboral y de propiedad intelectual vigente.

* **Salvaguarda Laboral y Privacidad:** Lo anterior aplica estrictamente a la información de negocio y operativa. Esta disposición **no habilita** el monitoreo indiscriminado ni el acceso a las comunicaciones personales de los trabajadores, las cuales permanecen protegidas por las garantías constitucionales y laborales, salvo en los casos y con las autorizaciones expresamente permitidas por el ordenamiento jurídico y el Reglamento Interno.

* **Indelegabilidad (Terceros):** La responsabilidad sobre la integridad y seguridad del dato es institucional e **indelegable**. Los proveedores, contratistas y encargados de tratamiento (SaaS) están sujetos a este marco normativo como extensión operativa de la Organización, sin perjuicio de las responsabilidades legales propias que correspondan a dichos terceros conforme a la ley y a los contratos suscritos.

**Prohibición de Acaparamiento:**
Ninguna unidad de negocio tiene derecho a ocultar, retener o bloquear el acceso a datos corporativos bajo la premisa de "propiedad departamental". El ocultamiento deliberado de información operativa se considera una obstrucción a la gestión.

### 2.2. Responsabilidad por Defecto
**Principio:** La ignorancia del estado de un dato no exime de responsabilidad funcional sobre el activo.

* **Asignación:** Todo activo de datos debe tener un **Dueño (Data Owner)** asignado explícitamente.
* **Efectividad del Rol:** La asignación formal de un Data Owner sin capacidad real de control operativo o sin acceso a la evidencia técnica se considerará **ineficaz** para efectos de responsabilidad funcional. (No existen "Owners de papel"). La determinación de dicha ineficacia se realizará exclusivamente para fines de gestión interna de riesgos, sin prejuzgar responsabilidad administrativa o laboral individual.
* **Datos de Origen:** Si un activo primario no tiene dueño, la responsabilidad funcional y de trazabilidad recae automáticamente en la Jefatura o Gerencia del área donde se originó el dato.
* **Datos Derivados:** Para datos transformados (KPIs, agregaciones) donde el origen es múltiple, la responsabilidad recae en el dueño del proceso o algoritmo que generó el dato derivado.

> *Nota:* La responsabilidad aquí definida es **funcional y probatoria** respecto a la calidad y seguridad del dato, y no sustituye los procedimientos formales de determinación de responsabilidad administrativa o laboral.

### 2.3. Integridad y Sanciones
**Principio:** Para efectos de la **política interna de seguridad de la información**, la corrupción deliberada de bases de datos, la falsificación de métricas, la alteración de logs o la negligencia grave en el manejo de credenciales de acceso constituye una **falta grave contra los activos de la organización**.

**Debido Proceso:**
Cualquier sanción derivada de estas conductas se aplicará respetando estrictamente los procedimientos de investigación y sanción establecidos en el Reglamento Interno y la legislación laboral vigente, garantizando la proporcionalidad de la medida y el derecho a defensa del trabajador. La organización perseguirá las responsabilidades civiles o penales cuando corresponda (ej. Ley de Delitos Informáticos).

**Estándar Probatorio:**
Para efectos de investigación interna y determinación de responsabilidad, la evidencia válida se constituirá primariamente por **registros técnicos inmutables** (logs de sistema, historial de versiones, trazas de acceso). Las declaraciones testimoniales no tendrán valor probatorio superior a la evidencia sistémica.
* **Presunción de Falla de Control:** La inexistencia de registros técnicos exigidos por este marco (ausencia de logs) se considerará, para efectos internos de gestión y priorización de riesgos, como **indicio de ausencia de control efectivo** del proceso, sin perjuicio de otros medios de prueba admisibles.

---

## 3. MARCO DE CLASIFICACIÓN Y HERENCIA

Todo dato debe estar clasificado. El tratamiento de datos "Sin Clasificar" está prohibido en ambientes productivos.

| Nivel | Etiqueta | Definición Operativa | Ejemplo |
| :--- | :--- | :--- | :--- |
| **L0** | `PÚBLICO` | Información para consumo externo. Sin riesgo. | Marketing, Memorias Anuales. |
| **L1** | `INTERNO` | Uso operativo estándar. Riesgo bajo si se filtra. | Directorio telefónico, Menús. |
| **L2** | `CONFIDENCIAL` | Datos de negocio sensibles. Riesgo financiero/estratégico. | Ventas, Márgenes, Estrategia. |
| **L3** | `RESTRINGIDO` | Datos protegidos por Ley (PII/PHI) o Secretos Comerciales. | Nómina, Salud, Claves, Fórmulas. |

**3.1. Principio de Contaminación (Herencia)**
La clasificación se hereda automáticamente a los datos derivados según el componente más restrictivo.
* **Alcance IA:** Los artefactos derivados del tratamiento de datos (incluyendo **modelos, features, embeddings, scores o representaciones vectoriales**) se consideran datos derivados a efectos de propiedad, clasificación, responsabilidad y control.
* *Limitación:* La clasificación heredada no implica, por sí sola, que el artefacto revele datos personales o sensibles, debiendo evaluarse caso a caso según su reversibilidad técnica.
* *Ejemplo:* Si un reporte mezcla datos `PÚBLICO` con datos `RESTRINGIDO`, el reporte completo se clasifica como `RESTRINGIDO`.
* *Excepción:* La desclasificación solo puede ocurrir mediante un proceso técnico de anonimización o segregación validado formalmente por el CDO.

---

## 4. ROLES Y AUTORIDAD (ESCALAMIENTO)

### 4.1. Chief Data Officer (CDO)
* **Mandato:** Autoridad delegada por el Directorio/Gerencia General para garantizar la veracidad, legalidad y defensabilidad de los datos.
* **Poder de Veto Motivado:** El CDO tiene la facultad de detener (vetar) cualquier proyecto, paso a producción o reporte que viole demostrablemente los estándares de integridad o privacidad.
    * *Condición:* El veto debe estar **fundamentado** en evidencia técnica o normativa (no es discrecional).
    * *Escalamiento y Override:* El veto es vinculante. Las situaciones de urgencia operativa podrán continuar únicamente mediante instrucción escrita de la Gerencia General, quedando **explícitamente registrado que el riesgo ha sido aceptado por la Administración Superior** fuera del marco técnico recomendado (Transferencia de Riesgo). Dicha instrucción libera al CDO de responsabilidad técnica sobre las consecuencias derivadas del riesgo aceptado.

### 4.2. Data Owner (Dueño de Dominio)
* **Mandato:** Responsable funcional de la calidad, definición y ciclo de vida de los datos en su dominio.
* **Responsabilidad:** Responde por la exactitud del dato frente a la organización.

### 4.3. Data Steward (Custodio)
* **Mandato:** Rol operativo que ejecuta las políticas de calidad y seguridad definidas por el Owner y el CDO.

---

## 5. CICLO DE VIDA Y ELIMINACIÓN

1.  **Minimización:** Solo se recolectan datos con una hipótesis de uso explícita, la cual debe estar **documentada y vinculada a un proceso de negocio en el Catálogo de Datos** antes de iniciar la recolección.
2.  **Caducidad (TTL):** Todo dato `RESTRINGIDO` debe tener una fecha de expiración técnica o regla de retención configurada desde su creación.
3.  **Derecho al Olvido:** La capacidad de borrar o anonimizar un registro individual es un requisito de arquitectura.
    * *Excepción:* Las obligaciones de eliminación se aplican sin perjuicio de los deberes legales de conservación (*Legal Hold*) ante juicios pendientes o normativas sectoriales específicas (ej. CMF, SII).

---

## 6. VIGENCIA Y RATIFICACIÓN

Esta Constitución de Datos entra en vigor a partir de su firma y deroga cualquier política interna anterior que la contradiga en materia de gestión de datos. El documento será revisado anualmente para asegurar su vigencia técnica y legal.

<br>
<br>

__________________________
**Gerente General (CEO)**
*(Por Resolución de Directorio)*
*Responsable Final del Riesgo a nivel de Gobierno Corporativo*

<br>
<br>

__________________________
**Chief Data Officer (CDO)**
*(Autoridad Delegada)*
*Responsable de la Gobernanza*