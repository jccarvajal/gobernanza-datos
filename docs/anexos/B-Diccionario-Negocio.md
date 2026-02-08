# Anexo B: Diccionario de Negocio y Taxonomía

> **CLASIFICACIÓN DEL DOCUMENTO:** ESTRATÉGICO / TÉCNICO
> **VIGENCIA:** DINÁMICA (ACTUALIZACIÓN CONTINUA BAJO CONTROL DE CAMBIOS)
> **RESPONSABLE:** COMITÉ GRC (GOBIERNO) / DATA STEWARDS (EJECUCIÓN OPERATIVA BAJO SUPERVISIÓN DEL CDO)
> **ALCANCE:** DATOS OFICIALES Y COMPARTIDOS (EXCLUYE ENTORNOS DE LABORATORIO/SANDBOX)

---

## 1. PROPÓSITO: LA PIEDRA ROSETTA

Este documento define el lenguaje oficial de la organización. Su objetivo es eliminar la ambigüedad semántica que genera la "Guerra de Métricas" y establecer la base de la evidencia corporativa.

**Distinción de Alcance (Blindaje a la Innovación):**

* **Espacio Oficial (Fábrica):** Aplica obligatoriamente para reportes de directorio, estados financieros, cumplimiento regulatorio y APIs de integración entre sistemas. Si un término no está definido aquí, **no es un dato oficial**, es una opinión no regulada.
* **Espacio de Exploración (Laboratorio):** Para análisis ad-hoc, ciencia de datos y prototipos. Los analistas tienen libertad de crear métricas provisorias e innovar.
    * *Regla de Nomenclatura (Anti-Confusión):* Todo dato o métrica generada en el espacio de laboratorio debe llevar obligatoriamente un prefijo distintivo (ej. `tmp_`, `exp_`, `lab_`) que señale explícitamente su naturaleza provisional y evite su consumo accidental como "verdad oficial".

**Excepción de Continuidad Operacional:**

En situaciones excepcionales debidamente documentadas (ej. contingencias operativas, cierres contables urgentes, requerimientos regulatorios inmediatos), se permitirá el uso transitorio de métricas no certificadas, siempre que:

1.  Quede explícitamente registrado su carácter provisional y el responsable de su uso.
2.  Se inicie su regularización en el Diccionario dentro de un plazo máximo de **30 días**.

---

## 2. PLANTILLA MAESTRA DE DEFINICIÓN (METADATOS)

Todo término crítico debe estar documentado con los siguientes campos obligatorios.

**Criterio de Criticidad:**

Se consideran términos críticos aquellos con impacto en Estados Financieros, Cumplimiento Regulatorio, Derechos de Titulares o Estrategia de Directorio.

* **Alcance Extendido (IA y Modelos):** Todo score, probabilidad, ranking automático, clasificación o representación vectorial (embedding) derivada de datos que sea utilizada directa o indirectamente para toma de decisiones corporativas o que afecte derechos de terceros, se considera un término crítico.
* **Criterio de Aplicación:** El impacto decisional será evaluado según su **uso efectivo y reiterado en procesos formales**, y no por su mera disponibilidad técnica o exploratoria (evitando la regulación excesiva de notebooks experimentales).

**Estados de Certificación:**

1.  **Certificado Vigente:** Cumple con todos los metadatos y validaciones.
2.  **Certificado Condicional:** Admisible temporalmente cuando faltan metadatos no estructurales (ej. descripción extendida), pero **NUNCA** cuando falta la Trazabilidad Técnica, Fuente de Verdad o Artefacto de Ejecución.
3.  **No Certificado:** No apto para uso oficial.

| Campo | Descripción | Ejemplo Real |
| :--- | :--- | :--- |
| **Término (ID)** | Nombre único y estandarizado. | `Venta_Neta_Mensual` |
| **Definición de Negocio** | Explicación en lenguaje natural (sin tecnicismos). | *Suma de facturas emitidas menos notas de crédito y devoluciones.* |
| **Dueño (Owner)** | Rol responsable de la definición (No el nombre de la persona). | `Gerente de Finanzas` |
| **Fuente de Verdad (SSOT)** | Sistema o Tabla certificada de origen. | `ERP_SAP.FCT_BILLING` |
| **Lógica de Cálculo** | Fórmula exacta o SQL simplificado. | `SUM(amount) WHERE status = 'PAID' AND date IN current_month` |
| **Artefacto de Ejecución** | **Vínculo al Código:** ID del Job, Modelo, Script o Vista en producción. | `dbt_prod.finance.mrt_monthly_sales_v2` |
| **Nivel de Clasificación** | Según Anexo A (L0 - L3). | `L2 - CONFIDENCIAL` |
| **Versión** | Número de versión vigente. | `v2.1` |

> **Blindaje Técnico (Neutralidad Tecnológica):** El campo "Artefacto de Ejecución" es el puente entre la semántica y la ingeniería. Garantiza que lo que dice el diccionario es exactamente lo que está ejecutando el código.

---

## 3. VERSIONADO Y DEFENSA HISTÓRICA

La realidad del negocio cambia, y las definiciones también. Cuando se modifica una lógica de cálculo (ej. cambiar cómo calculamos el "Churn"):

1.  **No se sobrescribe:** Se crea una nueva versión (`v1.0` -> `v2.0`).
2.  **Inmutabilidad Histórica:** Las versiones anteriores permanecen congeladas y consultables.
3.  **Defensa de Auditoría:** Esto permite explicar por qué el reporte de 2023 dio un número distinto al de 2025 ("En 2023, la definición vigente y correcta era la v1.0").

**Principio de Decisión Contextual:**

Las decisiones adoptadas conforme a una versión vigente del término se considerarán **técnicamente válidas al momento de su adopción**, aun cuando versiones posteriores modifiquen la definición o el algoritmo de cálculo. (El cambio de criterio futuro no invalida la diligencia pasada).

---

## 4. TAXONOMÍA Y JERARQUÍA (SSOT vs. DATA MESH)

Para resolver la tensión entre la unicidad de la evidencia y la autonomía de los dominios (Cap. 13), establecemos tres niveles taxonómicos:

### Nivel 1: Master Data (Identidad - Centralizado)
* **Qué es:** La definición ontológica de las entidades principales.
* **Regla:** Debe ser **ÚNICA** para toda la empresa.
* **Ejemplo:** `Cliente_ID` (RUT/TaxID). Un cliente es legalmente la misma persona para todos.

### Nivel 2: Datos de Dominio (Representación - Federado)
* **Qué es:** Atributos contextuales o comportamiento específico de un área.
* **Regla:** Puede ser **POLIMÓRFICA**. Cada dominio puede tener su propia "vista" del ente.
* **Límite de Dominio:** Ninguna definición de dominio podrá ser utilizada fuera de su contexto operativo (exportada a Directorio o Regulatorio) sin ser elevada y certificada como métrica derivada (Nivel 3).
* **Ejemplo:** Finanzas define `Cliente_Activo` distinto a Marketing. Ambas son válidas *dentro* de sus silos, pero no pueden salir como "Verdad Corporativa" sin conciliación.

### Nivel 3: Métricas Derivadas (Reporting)
* **Qué es:** Cálculos agregados para toma de decisiones ejecutivas.
* **Regla:** Deben tener trazabilidad completa hacia el Nivel 1 o 2.

---

## 5. RESOLUCIÓN DE CONFLICTOS SEMÁNTICOS

> **PROTOCOLO DE PODER (ANTI-BLOQUEO):** Los conflictos de definición no se resuelven por consenso horizontal eterno, sino por **Arbitraje Vertical**.

**Mecanismo de Disputa:**

1.  **Detección:** El Data Steward identifica la colisión de términos.
2.  **Mediación:** Se intenta unificar criterios técnicos entre los dominios.
3.  **Arbitraje y Clasificación:** Si no hay acuerdo, el CDO clasifica el conflicto (**Crítico, Operativo o Analítico**) y establece un SLA de resolución acorde al impacto regulatorio o financiero.
4.  **Resolución:** El CDO emite la "Resolución de Definición".
    * *Válvula de Continuidad:* El plazo podrá extenderse excepcionalmente cuando exista justificación técnica documentada, **sin suspender la validez temporal de la definición vigente**.
5.  **Acatamiento:** Los dominios deben ajustar sus ETLs a la nueva norma.
    * *Escalamiento:* El incumplimiento del SLA de adecuación sin justificación técnica documentada será escalado como **incumplimiento de control** al Comité GRC.

---

## 6. MANDATO DE VISIBILIDAD

Para garantizar la adopción y proteger a la Alta Dirección de decisiones erróneas, se establece la siguiente regla operativa:

**"Solo los términos certificados en este Diccionario Oficial, que cuenten con un Artefacto de Ejecución validado, tienen permiso técnico para ser desplegados como información oficial."**

* **Universalidad del Canal:** Este mandato aplica a cualquier canal de consumo corporativo (BI, reportes automáticos, APIs, integraciones sistema-a-sistema o exportaciones programadas), independientemente del formato o herramienta.
* **Marca de Agua:** Cualquier otra métrica experimental o de laboratorio puede existir, pero debe llevar obligatoriamente una marca de agua visible o descargo de responsabilidad: `NO CERTIFICADO / BORRADOR`.

**Principio de Validez:**

Las métricas no certificadas carecen de validez oficial para la toma de decisiones corporativas vinculantes. El uso operativo reiterado de términos críticos no definidos o no vigentes en este Diccionario constituye una **desviación de control (Incidente de Gobernanza)** que debe ser reportada como **riesgo operativo** y está sujeta a revisión por el Comité GRC.