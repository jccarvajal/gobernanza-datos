# Anexo F: Protocolo de Adecuación Chile 2026 (Ley 21.719)

> **CLASIFICACIÓN:** CRÍTICO / NORMATIVO LOCAL

> **NORMATIVA:** LEY 21.719 (PROTECCIÓN DE DATOS PERSONALES)

> **OBJETIVO:** ADECUACIÓN TÉCNICA FORZOSA ANTE LA ENTRADA EN VIGENCIA

> **DEADLINE:** 01 DE DICIEMBRE DE 2026

> **INSTRUMENTO DE CONTROL:** AUDITABLE MEDIANTE EL CHECKLIST DEL ANEXO E.

---

## 1. EL CAMBIO DE RÉGIMEN (FISCALIZACIÓN TÉCNICA)

A partir del **01/12/2026**, la Agencia de Protección de Datos fiscalizará la **arquitectura misma** de tratamiento. En un entorno de fiscalización proactiva y responsabilidad demostrable, la "buena fe" no es defensa válida; la única prueba eximente de responsabilidad es la **evidencia técnica inmutable**.

---

## 2. OBLIGACIONES TÉCNICAS (ESTADOS DEL SISTEMA)

A las salvaguardas generales del libro (Cap. 1-15), se integran estos bloques críticos exigidos específicamente por la Ley 21.719.

### 2.1. Evaluación de Impacto (EIPD) como Pipeline
La EIPD no es un informe estático en PDF; es un **Gate de Despliegue** bloqueante en el flujo de CI/CD.

* **Control:** El pipeline de despliegue valida la existencia de un `EIPD_ID` aprobado en el sistema de gestión.
* **Criterio de Riesgo:** Se consideran de alto riesgo (y requieren EIPD obligatoria) los Datos Sensibles (salud, biometría), tratamientos masivos y uso de IA/Perfilamiento.
* **Regla de Bloqueo:** `IF (risk_level == HIGH) AND EIPD_status != APPROVED -> BLOCK_DEPLOY`.

### 2.2. Decisiones Automatizadas y Perfilamiento
* **Metadatos:** Todo registro de una decisión automatizada debe incluir `is_automated = TRUE`, `model_version` y `logic_hash`.
* **Derecho a Explicación:** El sistema debe tener la capacidad de reconstruir el contexto de la decisión (variables de entrada exactas y pesos ponderados) en lenguaje comprensible para el titular.

### 2.3. Transparencia Activa y Rectificación
* **Endpoint de Transparencia:** API `/privacy/my-status` que expone al titular la finalidad, base legal y fecha de caducidad (TTL) de sus datos.
* **Rectificación Sistémica:** El sistema debe permitir la actualización de datos incorrectos y **propagar el cambio** a todos los sistemas derivados mediante linaje activo (evitando la inconsistencia de datos).

### 2.4. Control de Encargados de Tratamiento (SaaS)
* **Auditoría Técnica:** Exigencia contractual de ingestión de logs de acceso del proveedor hacia el SIEM central de la organización.
* **Borrado Verificable:** Capacidad técnica de ejecutar y auditar una purga efectiva en el entorno del encargado (SaaS).

### 2.5. Registro de Incidentes
Todo evento de seguridad o desviación normativa debe quedar registrado sistemáticamente.

* **Bitácora Inmutable:** Registro de causa raíz, alcance, impacto y medidas correctivas (Ver **Anexo D**).

### 2.6. Delimitación del Alcance Legal del Tratamiento
No todos los tratamientos están sujetos a idénticos requisitos operativos. La arquitectura debe clasificar cada flujo en el **Catálogo de Datos** según su base de legitimidad:

* **Obligación Legal / Interés Público:** Tratamiento forzoso (no borrable a petición).
* **Ejecución Contractual:** Necesario para el servicio.
* **Consentimiento Expreso:** Revocable y requiere gestión de estado (`boolean`).
* **Interés Legítimo:** Requiere prueba de ponderación de derechos.

> **Regla de Diseño:** La exigencia de bloqueo o borrado se aplica diferenciada según esta clasificación técnica.

---

## 3. RÉGIMEN SANCIONATORIO Y RESPONSABILIDAD

| Falla Arquitectónica | Infracción (Ley 21.719) | Sanción / Riesgo Potencial |
| :--- | :--- | :--- |
| **Falta de EIPD en IA** | Gravísima | Multa hasta 20.000 UTM / Suspensión de IA |
| **Opacidad en Scoring** | Grave | Vulneración del Derecho a Explicación |
| **Dato sin base legal** | Gravísima | Orden de eliminación total de la base |
| **Falta de Registro** | Gravísima | Agravante por reincidencia sistémica |

> **NOTA DE INTERPRETACIÓN DE RIESGO:**
> Las presunciones de negligencia y clasificaciones descritas en este protocolo corresponden a una **política interna de gestión de riesgo**, diseñada bajo el escenario más estricto posible para exceder el estándar legal mínimo. Su finalidad es anticipar el criterio fiscalizador de la Agencia, asegurando la defendibilidad de la organización ante el peor escenario, sin perjuicio de la defensa legal específica en cada caso.

### 3.1. Responsabilidad del Directorio (Gobierno Corporativo)
La aprobación, financiamiento y priorización de este protocolo constituye un acto de **Gobierno Corporativo**.

* **Defensa de Diligencia:** Este anexo y su ejecución operan como evidencia de advertencia temprana y control activo.
* **Riesgo de Omisión:** La ausencia de ejecución será considerada internamente como una decisión consciente de asumir el riesgo sancionatorio, debilitando la defensa de "desconocimiento" o "buena fe".

### 3.2. Responsabilidad Personal (Sector Público)

> **ADVERTENCIA AL JEFE DE SERVICIO (ALERTA DE RESPONSABILIDAD PERSONAL)**
>
> Bajo la Ley 21.719, la protección de datos deja de ser una función técnica delegable y pasa a ser un **deber directo de dirección**.
> En una fiscalización de la Agencia, la ausencia de evidencia técnica (linaje, logs inmutables, borrado seguro) no se interpreta como una carencia tecnológica, sino como una **falta de control directivo sobre activos críticos**.
>
> **En el sector público, esta omisión activa consecuencias directas:**
> 
> * **Responsabilidad Administrativa:** Sumarios por falta al deber de dirección y control jerárquico.
> * **Afectación Patrimonial:** Riesgo de descuentos en remuneraciones y pérdida de asignaciones de modernización/gestión.
> * **Evaluación ADP:** Riesgo de no renovación o remoción por pérdida de confianza (falta de probidad administrativa).
> * **Agravantes:** Si la falta de controles sugiere negligencia sistemática en el tiempo.
>
> **PRINCIPIO DE DEFENSA:**
> La arquitectura es el **único escudo funcional** que permite al Jefe de Servicio demostrar que actuó con la debida diligencia. Operar sin una **Arquitectura Defensiva** implementada constituye una **aceptación implícita del riesgo personal y profesional** asociado a su cargo.

---

## 4. CRONOGRAMA DETALLADO DE ADECUACIÓN (BATTLE PLAN 2026)

> **ADVERTENCIA EJECUTIVA:**
> Este cronograma no es una recomendación técnica opcional; es la **última ventana operativa razonable** antes de la pérdida de control y la exposición a pasivos legales irreversibles.

### FASE 1: DIAGNÓSTICO Y CUARENTENA (Q1: Enero - Marzo)
*Estado: **CRÍTICO / EN CURSO**.*

* **Discovery:** Escaneo de bases de datos buscando PII no gobernada.
* **Congelamiento:** Se prohíbe la creación de nuevas tablas productivas sin esquema validado (Ver **Cap. 9 - Airlock**).

### FASE 2: INGENIERÍA DE DEFENSA (Q2: Abril - Junio)
*Objetivo: Construir los muros.*

* **Gate EIPD:** Bloqueo automatizado en CI/CD para modelos de IA y tratamientos masivos.
* **Motor de Rectificación:** Scripts de propagación de cambios en el Data Lake.

### FASE 3: PURGA Y TRANSPARENCIA (Q3: Julio - Septiembre)
*Objetivo: Eliminar pasivos.*

* **La Gran Purga:** Ejecución de *Crypto-shredding* sobre datos tóxicos o caducos identificados en Fase 1.
* **Ultimátum SaaS:** Bloqueo o migración de proveedores que no certifiquen cumplimiento técnico.

### FASE 4: SIMULACRO Y GO-LIVE (Q4: Octubre - Diciembre)
*Objetivo: Estrés y Operación.*

* **Simulacro de Brecha:** Prueba de notificación en <72h usando Linaje de Datos y Logs WORM.
* **Code Freeze:** Auditoría final de "caja negra" simulando a la Agencia.
* **01/12/2026:** **INICIO DE VIGENCIA.** Riesgo legal activo al 100%.

> **Veredicto Final:**
> Si la Agencia fiscaliza y no encuentra estos bloques operativos, la arquitectura se considera **indefensa**. Cumplir con la Ley 21.719 no es un ejercicio de redacción de políticas; es un ejercicio de **ingeniería con conciencia legal**.