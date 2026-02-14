# ANEXO G: ESTÁNDAR DE GOBERNANZA PROPORCIONAL (EGP)
**(Criterios de Clasificación, Contención y Accountability)**

!!! abstract "Contexto Estratégico (No Normativo)"
    Este anexo no busca anticipar regulaciones específicas, sino corregir una asimetría estructural: la gestión de sistemas de alto impacto bajo lógicas de **producto experimental** (caracterizadas por la rapidez de despliegue, iteración continua y responsabilidad difusa).

    Dicho modelo es funcional en entornos de bajo riesgo, pero resulta insuficiente cuando el sistema:

    * Intermedia derechos fundamentales.
    * Opera a escala masiva.
    * O genera contenido con implicancias legales o económicas significativas.

    **Principio Rector:** A mayor poder sistémico, mayor formalidad decisional y trazabilidad de responsabilidad.

    La elevación del estándar puede realizarse internamente, mediante una arquitectura de gobernanza verificable, o externamente, mediante regulación prescriptiva. La diferencia fundamental no es moral, sino estratégica: se trata de definir **quién controla el diseño de los mecanismos de accountability**.

---

## 1. PROPÓSITO

Este estándar tiene por objeto complementar el marco general de Gobernanza de Datos y Gestión de Riesgos Tecnológicos. En ausencia de un marco corporativo previo, este documento operará como el estándar mínimo exigible para la gestión de activos tecnológicos de alta criticidad.

---

## 2. PRINCIPIOS FUNDAMENTALES

### 2.1. Producto vs Infraestructura Funcional
Para efectos de gobierno interno, la clasificación de todo activo tecnológico deberá basarse en su naturaleza funcional y no exclusivamente en su tecnología base:

* **Producto Digital:** Software cuyo eventual fallo produce impactos reversibles, confinados a un entorno limitado o de bajo costo sistémico.
* **Infraestructura Funcional:** Sistema que intermedia derechos, opera a escala masiva, genera contenido con impacto legal o soporta operaciones críticas para la continuidad del negocio.

### 2.2. Integridad Funcional (Anti-Fragmentación)
La clasificación de criticidad aplica a la **capacidad funcional completa del sistema**, independientemente de su arquitectura técnica subyacente.

> **Regla de Blindaje:** La fragmentación de un sistema clasificado como "Infraestructura" en múltiples microservicios o componentes menores **no reduce su clasificación de riesgo**. Si la orquestación del conjunto produce un impacto sistémico, la gobernanza aplicará a todos los componentes críticos de la cadena de valor.

---

## 3. TAXONOMÍA DE CRITICIDAD

### 3.1. Matriz de Decisión Rápida

| Criterio | NIVEL 1 (Bajo Impacto) | NIVEL 2 (Significativo) | NIVEL 3 (Sistémico) |
| :--- | :--- | :--- | :--- |
| **Impacto en Derechos** | Ninguno | Fricción operativa | Intermediación o Denegación |
| **Escala de Afectación** | Individual / Aislada | Segmento de Clientes | Masiva / Poblacional |
| **Reversibilidad** | Alta (Rollback simple) | Media (Compensable) | Baja / Irreversible |
| **Intervención Humana** | Total o Híbrida | Supervisión Pasiva | Delegación en la Máquina |
| **Gobernanza Exigible** | Estándar SDLC | Reforzada | **Ingeniería de Contención** |

### 3.2. Procedimiento de Clasificación
La clasificación no podrá ser auto-declarativa; deberá realizarse mediante una evaluación estructurada de impacto y el análisis de escenarios de falla crítica (*Worst-Case Scenario*).

> **Integración con ERM:** La clasificación resultante deberá integrarse formalmente a la matriz corporativa de riesgos (*Enterprise Risk Management*), reflejando su impacto en el perfil de riesgo global de la organización.

### 3.3. Re-evaluación por Cambios (Gestión de Deriva)
La clasificación de un activo no es estática. Cualquier modificación sustantiva en la arquitectura, el modelo de datos o el alcance funcional del sistema deberá gatillar una **re-evaluación obligatoria de su nivel de criticidad**.

---

## 4. DEFINICIÓN DE NIVELES Y RESPONSABLES

### NIVEL 1: BAJO IMPACTO
* **Requisitos:** Cumplimiento del Ciclo de Vida de Desarrollo de Software (SDLC) formal, pruebas funcionales y registro de logs básico.
* **Responsable:** Product Owner / Líder Técnico.

### NIVEL 2: IMPACTO SIGNIFICATIVO
* **Requisitos Adicionales:** Evaluación de riesgo documentada, trazabilidad completa de cambios y aprobación formal de pase a producción.
* **Responsable:** Gerente de Área (1ª Línea de Defensa).

### NIVEL 3: IMPACTO SISTÉMICO
* **Correspondencia:** Aplica a todo activo que haya sido clasificado como **Infraestructura Funcional** (Ver punto 2.1).
* **Requisitos Adicionales:** Implementación obligatoria de la Arquitectura de Contención descrita en la Sección 5.
* **Responsable:** **Ejecutivo C-Level (Nominativo)**. No se admitirá la propiedad difusa ni la delegación exclusiva en órganos colegiados.

---

## 5. ARQUITECTURA MÍNIMA DE CONTENCIÓN (Exclusivo Nivel 3)

Ningún sistema clasificado como Nivel 3 podrá entrar en operación productiva sin la evidencia documentada de los siguientes controles de ingeniería:

### 5.1. Capacidad de Degradación Controlada (Kill Capability)
Debe existir un mecanismo técnico probado que permita desactivar o limitar la funcionalidad crítica de inmediato (modo degradado) sin requerir el apagado total de la organización.

> **Estándar:** El mecanismo deberá ser probado **al menos una vez al año mediante simulación controlada**.
> 
> **Trazabilidad de la Omisión:** La decisión de **no activar** el mecanismo ante una alerta crítica deberá quedar documentada con su respectiva justificación técnica y la firma del responsable nominativo.

### 5.2. Trazabilidad Decisional (Registro Forense)
Implementación de logs inmutables (WORM) que registren los parámetros de decisión y el versionamiento de los modelos utilizados, permitiendo la reconstrucción ex-post del proceso decisional.

### 5.3. Escalamiento Automático
El sistema deberá generar alertas directas al nivel ejecutivo responsable cuando se superen los umbrales de error o deriva (*drift*) predefinidos.

### 5.4. Revisión Independiente Calificada
Evaluación periódica realizada por la 2ª Línea de Defensa o un auditor externo calificado.

> **Criterio de Independencia:** El revisor designado no deberá tener objetivos ni incentivos vinculados al *time-to-market* o al desempeño financiero del producto evaluado.

---

## 6. INDICADORES DE DILIGENCIA (KPIs)

Para la supervisión de sistemas Nivel 3, se monitorearán al menos los siguientes indicadores:

1.  **MTTD (Mean Time to Detect):** Tiempo promedio para la detección de una anomalía.
2.  **MTTC (Mean Time to Contain):** Tiempo promedio para la neutralización del impacto.
3.  **Tasa de incidentes por millón de operaciones.**

> **Principio de Sustancia:** La medición de estos indicadores no sustituye el análisis cualitativo. Un MTTC sistemáticamente elevado constituirá un indicio de debilidad arquitectónica y requerirá una revisión estructural del sistema.

---

## 7. ACCOUNTABILITY Y CONTROL

### 7.1. Principio de Competencia
La designación de un Ejecutivo C-Level como responsable no exime la obligación de asegurarse de contar con la capacidad técnica suficiente para comprender los riesgos inherentes. La ignorancia técnica no será considerada un eximente de responsabilidad en la supervisión.

### 7.2. Anti-Gaming (Reclasificación)
La sub-clasificación deliberada de un activo (por ejemplo, mediante fragmentación para evitar el Nivel 3) constituirá un **incumplimiento grave del sistema de control interno**.

> **Facultad:** La 2ª Línea de Defensa tendrá la facultad de **reclasificar unilateralmente** un sistema cuando detecte inconsistencias, activando de inmediato los controles de Nivel 3.
> **Contrapeso:** Toda reclasificación deberá ser reportada formalmente al Comité de Riesgos (o instancia equivalente) en el siguiente ciclo de gobernanza, acompañando la justificación y evidencia técnica. La eventual reversión de esta medida requerirá una resolución trazable a nivel ejecutivo.

---

## 8. SUPERVISIÓN FIDUCIARIA

El Directorio (o el órgano de gobierno delegado) deberá:

1.  Recibir un reporte periódico y extraordinario sobre el estado de los sistemas Nivel 3.
2.  Aprobar formalmente el nivel de riesgo residual aceptado.
3.  Considerar la omisión sistemática de supervisión como una debilidad material de Gobierno Corporativo.

---

## 9. NOTA ESTRATÉGICA FINAL

La ausencia de mecanismos verificables de contención y accountability en sistemas de impacto sistémico incrementa significativamente la probabilidad de una regulación prescriptiva posterior a un incidente material.

El propósito fundamental del EGP es reducir dicho riesgo sistémico y preservar el **control arquitectónico sobre el diseño del cumplimiento.**