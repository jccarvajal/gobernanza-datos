# Anexo F: Protocolo de Adecuación Técnica (Ley 21.719)

> **CLASIFICACIÓN:** CRÍTICO / NORMATIVO LOCAL
>
> **MARCO JURÍDICO:** LEY 21.719 SOBRE PROTECCIÓN DE DATOS PERSONALES
>
> **OBJETIVO:** ESTÁNDAR DE CUMPLIMIENTO TÉCNICO Y TRAZABILIDAD
>
> **PLAZO PERENTORIO:** 01 DE DICIEMBRE DE 2026
>
> **VINCULACIÓN:** ESTE DOCUMENTO ES AUDITABLE MEDIANTE EL CHECKLIST DEL ANEXO E.

---

## PARTE I — MARCO NORMATIVO Y ESTÁNDAR ARQUITECTÓNICO

### 1. CONTEXTO Y CAMBIO DE RÉGIMEN DE FISCALIZACIÓN

Con la entrada en vigencia plena de la Ley 21.719 el **01 de diciembre de 2026**, la Agencia de Protección de Datos iniciará sus facultades fiscalizadoras. A diferencia de normativas anteriores, la Agencia no solo auditará la existencia de políticas escritas, sino que fiscalizará la **arquitectura efectiva** de los sistemas de tratamiento de información.

**1.1. Hipótesis Operativa de Riesgo**
Para efectos de la gestión de riesgos de esta organización, se establece la siguiente premisa operativa: bajo el escenario fiscalizador más estricto razonablemente previsible, la mera "buena fe" o la declaración de intenciones no constituirán, por sí solas, defensas suficientes ante un procedimiento sancionatorio.

En consecuencia, esta política define que la **principal prueba de diligencia demostrable** será la evidencia técnica inmutable y verificable de cumplimiento (principio de Responsabilidad Proactiva Demostrable), sin perjuicio de otros medios de prueba admisibles en derecho.

> **Nota de Alcance:** Este criterio no pretende fijar el estándar jurídico definitivo —competencia exclusiva de los tribunales—, sino establecer un **umbral interno de diligencia técnica reforzada** para blindar a la organización.

---

### 2. OBLIGACIONES TÉCNICAS Y ESTADOS DEL SISTEMA

Además de las salvaguardas generales descritas en los capítulos 1 a 16 del Manual de Gobernanza, se integran los siguientes **bloques de control crítico**, de implementación obligatoria para cumplir con la nueva legislación.

#### 2.1. La Evaluación de Impacto (EIPD) en el Ciclo de Desarrollo

La Evaluación de Impacto en Protección de Datos (EIPD) dejará de ser un documento administrativo estático para convertirse en un **Gate de Despliegue (Deployment Gate)** dentro del flujo de CI/CD.

* **Mecanismo de Control:** El pipeline de integración continua deberá validar programáticamente la existencia de un `EIPD_ID` aprobado antes de permitir el paso a producción.
* **Criterio de Aplicación:** Será obligatorio para tratamientos que involucren datos sensibles, volúmenes masivos u operaciones de IA/Perfilamiento.

**Regla de Bloqueo Automático:**
Se instruye la implementación de la siguiente lógica de bloqueo en los sistemas de despliegue:

> SI (Nivel_Riesgo == ALTO) Y (Estado_EIPD != APROBADO) ENTONCES -> BLOQUEAR_DESPLIEGUE

* **Excepción Controlada:** Únicamente la Administración Superior podrá autorizar un despliegue manual saltando este control, asumiendo el riesgo residual explícito. El uso reiterado de esta excepción será auditado como un indicador de riesgo sistémico.

#### 2.2. Transparencia en Decisiones Automatizadas y Perfilamiento

Para dar cumplimiento al derecho a explicación consagrado en la ley, todo sistema que ejecute decisiones automatizadas deberá registrar metadatos suficientes para su auditabilidad.

* **Requisitos del Registro:** Cada transacción deberá almacenar los campos `is_automated`, `model_version` y `logic_hash`.
* **Capacidad de Explicación:** El sistema deberá mantener la capacidad técnica de reconstruir los **factores determinantes** de la decisión en un lenguaje comprensible para el titular. Esto no implica la revelación de secretos comerciales o propiedad intelectual del algoritmo, sino la entrega de una explicación funcional suficiente.

#### 2.3. Transparencia Activa y Gestión de Derechos

La organización debe garantizar que el ejercicio de derechos no dependa de procesos manuales lentos.

* **Disponibilidad de Información:** Se habilitará un endpoint o servicio de consulta (`/privacy/my-status`) que permita al titular conocer la finalidad, base legal y tiempo de vida (TTL) de sus datos en tiempo real.
* **Integridad en la Rectificación:** Los sistemas deben implementar un "Linaje Activo". Al rectificarse un dato maestro, el cambio debe propagarse automáticamente a los sistemas descendentes para evitar inconsistencias que vulneren la calidad del dato.

#### 2.4. Control de la Cadena de Suministro (Proveedores SaaS)

La responsabilidad por los datos no se extingue al contratar servicios de terceros (Encargados de Tratamiento).

* **Visibilidad:** Se exigirá contractualmente la ingesta de logs de actividad del proveedor hacia el SIEM central de la organización.
* **Soberanía de Datos:** El proveedor deberá demostrar capacidad técnica de borrado seguro y verificable.
* **Consecuencia:** La imposibilidad técnica o contractual de un proveedor para cumplir estos estándares constituirá causal válida para la no contratación, terminación anticipada o migración del servicio.

#### 2.5. Registro Inmutable de Incidentes

Todo evento de seguridad con potencial afectación a datos personales deberá ser registrado sistemáticamente, independientemente de si el incidente se materializa o descarta posteriormente. El registro deberá ser inmutable e incluir análisis de causa raíz, alcance y medidas correctivas (conforme al Anexo D).

#### 2.6. Clasificación y Alcance Legal del Tratamiento

Para evitar borrados indebidos o retenciones ilegales, el Catálogo de Datos deberá clasificar cada activo según su base de legitimidad:

1. **Obligación Legal / Interés Público:** Datos no borrables a petición.
2. **Ejecución Contractual:** Datos necesarios para la vigencia del servicio.
3. **Consentimiento Expreso:** Datos sujetos a revocación inmediata.
4. **Interés Legítimo:** Datos sujetos a prueba de ponderación.

> **Regla de Diseño:** Los mecanismos de bloqueo y supresión deberán comportarse de manera diferenciada según esta etiqueta técnica.

---

### 3. MATRIZ DE RIESGO Y RESPONSABILIDAD

Esta sección tipifica las consecuencias de las fallas arquitectónicas bajo una interpretación de severidad máxima, con el fin de priorizar la inversión en seguridad.

| Falla Arquitectónica | Calificación de Riesgo Interno | Sanción Potencial (Ref. Ley 21.719) |
| :--- | :--- | :--- |
| **Falta de EIPD en IA** | Máxima Severidad | Multa hasta 20.000 UTM / Suspensión del tratamiento |
| **Opacidad en Scoring** | Alta | Vulneración del derecho a explicación |
| **Dato sin base legal** | Máxima Severidad | Orden de eliminación total de la base de datos |
| **Falta de Registro** | Alta | Agravante por reincidencia sistémica |

#### 3.1. Responsabilidad del Gobierno Corporativo
La aprobación y financiamiento de este protocolo se considera un acto esencial de Gobierno Corporativo. La falta de implementación de estas medidas dificulta la capacidad de la organización para demostrar la "diligencia debida" exigida por la ley ante una fiscalización.

#### 3.2. Responsabilidad Directiva (Aplicable al Sector Público)

> **ADVERTENCIA DE RESPONSABILIDAD ADMINISTRATIVA**
>
> Se hace presente a las jefaturas de servicio y directivos que, bajo el nuevo estándar, la ausencia de controles técnicos (trazabilidad, logs, borrado seguro) puede ser interpretada por el ente fiscalizador como una **falta al deber de control jerárquico** sobre los activos de información.
>
> Esta omisión puede derivar en:
> 
> * Responsabilidad administrativa (sumarios).
> * Afectación patrimonial institucional y personal.
> * Impacto negativo en evaluaciones de Alta Dirección Pública (ADP).
>
> **Principio de Defensa:** Esta arquitectura no es opcional; constituye el **mecanismo estructural de defensa** para acreditar que la autoridad actuó con la diligencia debida.

---

## PARTE II — PLAN ESTRATÉGICO DE IMPLEMENTACIÓN 2026

Para asegurar el cumplimiento en la fecha límite, se establece el siguiente cronograma de ejecución forzosa.

### FASE 1: DIAGNÓSTICO Y CONTENCIÓN (Q1: Enero – Marzo)
*Objetivo: Determinar la exposición real y detener la creación de nueva deuda técnica.*

* **Congelamiento:** Se prohíbe la creación de nuevas tablas productivas sin esquema validado (Airlock activo).
* **Discovery:** Escaneo automatizado de bases de datos buscando PII no gobernada.
* **Clasificación:** Etiquetado masivo por base legal (Verde / Amarillo / Rojo).

### FASE 2: INGENIERÍA DE DEFENSA (Q2: Abril – Junio)
*Objetivo: Implementar los bloqueos estructurales en el software.*

* **Gate EIPD:** Implementación del bloqueo en CI/CD.
* **Airlock:** Validación obligatoria en la ingesta de datos.
* **Automatización:** Despliegue de APIs de derechos ARCO.

### FASE 3: PURGA Y NORMALIZACIÓN (Q3: Julio – Septiembre)
*Objetivo: Reducir los pasivos acumulados.*

* **Crypto-shredding:** Eliminación verificable de datos clasificados como "Rojo" (sin base legal).
* **Auditoría SaaS:** Evaluación técnica de proveedores críticos.
* **Registro:** Generación automática del registro de actividades derivado del catálogo.

### FASE 4: SIMULACIÓN Y VALIDACIÓN (Q4: Octubre – Noviembre)
*Objetivo: Probar la resistencia de la organización antes de la vigencia.*

* **Simulacro de Brecha:** Prueba de notificación a la Agencia en <72 horas.
* **Auditoría Externa:** Revisión de "caja negra" simulando una fiscalización hostil.
* **Code Freeze:** Congelamiento pre-vigencia para asegurar estabilidad.

### 01 DE DICIEMBRE 2026: INICIO DE RÉGIMEN SANCIONATORIO
Desde este momento, la exposición legal depende íntegramente de la capacidad del sistema para generar evidencia continua de cumplimiento.

---

## CRITERIOS DE CONTROL (DEFINITION OF DONE)

| Fase | Criterio de Éxito (Booleano) |
| :--- | :--- |
| **Fase 1** | ☑ 100% bases escaneadas <br> ☑ PII sin dueño < 5% <br> ☑ Airlock bloqueando |
| **Fase 2** | ☑ Gate EIPD bloqueando despliegues reales <br> ☑ API derechos funcional |
| **Fase 3** | ☑ Evidencia técnica de eliminación <br> ☑ 100% proveedores críticos evaluados |
| **Fase 4** | ☑ Informe forense generado en <72h <br> ☑ Sin hallazgos críticos en auditoría |

## MATRIZ DE RESPONSABILIDAD (RACI)

| Fase | Responsible (Ejecuta) | Accountable (Responde) | Consulted (Experto) | Informed (Notificado) |
| :--- | :--- | :--- | :--- | :--- |
| **Q1** | Arquitecto Datos | CDO | DPO / Legal | Directorio |
| **Q2** | Data Eng / DevOps | CTO | CDO / DPO | Directorio |
| **Q3** | CISO / Operaciones | Gerencia General | Legal / Compras | Directorio |
| **Q4** | CISO / Red Team | CDO | Auditoría | Directorio |

## INDICADORES CRÍTICOS (RED FLAGS)

Se establece la obligación de escalamiento formal al Comité de Riesgos si ocurre cualquiera de los siguientes eventos:

1.  **> 15% de datos históricos** sin base legal trazable identificada.
2.  Imposibilidad técnica de implementar el **Gate EIPD** en sistemas core del negocio.
3.  Un proveedor crítico **impide la auditoría** o el borrado verificable de datos.
4.  El simulacro de brecha demora **>72 horas** en la generación del informe forense preliminar.

*El escalamiento debe constar en acta y activar una decisión formal de mitigación o aceptación de riesgo.*

---

> **Nota de Flexibilidad Normativa:**
> Las fechas indicadas responden a la entrada en vigencia prevista en la Ley 21.719. Si la autoridad administrativa o legislativa modifica los plazos de vacancia legal, este cronograma se ajustará proporcionalmente sin alterar la secuencia lógica de implementación técnica.

> **Veredicto Final:**
> Desde la perspectiva de esta **política interna de gestión de riesgos**, si la Agencia fiscaliza y no encuentra estos bloques operativos, la arquitectura se considera **estructuralmente insuficiente para efectos de defensa técnica**. Cumplir con la Ley 21.719 no es un ejercicio de redacción de políticas; es un ejercicio de **ingeniería con conciencia legal**.