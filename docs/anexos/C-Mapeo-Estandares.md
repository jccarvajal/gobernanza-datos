# Anexo C: Mapeo de Estándares (La Piedra Rosetta)

> **CLASIFICACIÓN:** REFERENCIA TÉCNICA / AUDITORÍA
> **PROPÓSITO:** TRADUCCIÓN NORMATIVA PARA AUDITORES Y REGULADORES
> **AUDIENCIA:** AUDITORES INTERNOS, REGULADORES, OFICIALES DE CUMPLIMIENTO

---

## 1. PRINCIPIO DE OPERACIONALIZACIÓN

Este libro propone una **Gobernanza de Datos Defensiva** que satisface los objetivos **relevantes** de control de los marcos tradicionales (DAMA-DMBOK2, ISO 27001, GDPR, MGDE), entendidos como aquellos directamente vinculables a **evidencia técnica verificable y trazable**, conforme a los principios de auditabilidad objetiva.

**Complementariedad Documental:**
Este enfoque **no elimina** la documentación normativa exigida por cada marco (políticas, manuales), sino que la subordina a evidencia técnica inmutable que respalda su cumplimiento efectivo. La política define la regla; la arquitectura demuestra su ejecución.

**Exención de Certificación:**
Este anexo no constituye una declaración de certificación formal ni sustituye los procesos de auditoría externa requeridos por cada estándar. Su propósito es demostrar la **capacidad técnica de control** alineada con los objetivos de cada norma. La existencia de estos mecanismos no implica, por sí sola, el cumplimiento íntegro de los requisitos del estándar, el cual depende también de su alcance, operación continua, revisión periódica y del contexto organizacional evaluado en cada auditoría.

---

## 2. TABLA DE EQUIVALENCIAS (CONTROL VS. ARQUITECTURA)

| Marco / Estándar | Requisito Tradicional (Lo que pide la norma) | Solución Arquitectónica (Cómo lo resolvemos) | Tipo de Evidencia Primaria |
| :--- | :--- | :--- | :--- |
| **DAMA-DMBOK2** | "Diccionario de Datos Documentado" | **Metadatos Vivos:** El diccionario se genera desde el código y se valida en el despliegue. | Automática / Trazable |
| **ISO 27001** | "Control de Acceso y Segregación de Funciones" | **IAM & Policy as Code:** Permisos definidos por rol en infraestructura. Nadie tiene acceso *root* directo a datos productivos. | Configuración / Logs |
| **GDPR / LDP** | "Derecho de Supresión (Borrado)" | **Crypto-shredding:** Destrucción probatoria de las llaves de cifrado del titular. | Log de revocación |
| **MGDE (Chile)** | "Integridad y Autenticidad del Expediente" | **Dato como Pre-Documento:** Linaje e inmutabilidad extendidos desde el origen transaccional. | Trazabilidad de Origen |
| **COBIT** | "Trazabilidad de Cambios" | **GitOps:** Todo cambio en el modelo de datos queda registrado en el control de versiones con autor y fecha. | Commit History |
| **Data Mesh** | *Evolución Funcional* | **Federación de Responsabilidad:** La propiedad del dato se asigna por dominio, no por silo tecnológico. | Asignación en Catálogo |

> **Nota de Alcance (Blindaje Normativo):** Las equivalencias aquí descritas representan mecanismos técnicos que satisfacen los **objetivos de control** de cada marco.
>
> **Suficiencia Probatoria:** El "Tipo de Evidencia" indicado corresponde al artefacto primario de verificación técnica. Ante la ausencia de esta evidencia técnica ("Logs", "Commits"), el control se considerará **no demostrable mediante evidencia técnica automatizada**, sin perjuicio de controles manuales o administrativos evaluados separadamente.

---

## 3. DETALLE DE EVIDENCIA POR MARCO

### 3.1. DAMA-DMBOK2 (Calidad y Gobierno)
* **Objetivo:** Asegurar que los datos sean entendibles, confiables y gestionados.
* **Enfoque Propuesto:** El **Contrato de Datos (Data Contract)** actúa como especificación técnica y de negocio vinculante. Si el dato no cumple el contrato (schema, tipo, reglas), el pipeline falla automáticamente antes de contaminar los sistemas analíticos.
* **Punto de Auditoría:** Revisar los tests de contrato en el pipeline CI/CD y el historial de ejecuciones fallidas (evidencia de control activo).
* **Alcance:** Este enfoque constituye una **interpretación operativa** del marco DAMA-DMBOK2, orientada a su implementación técnica, y no una redefinición formal de sus dominios conceptuales.

### 3.2. ISO 27001 (Seguridad de la Información)
* **Objetivo:** A.9.2.3 Restricción de acceso a la información y Segregación de Funciones (SoD).
* **Implementación:** SoD vía **GitOps**.
    * El Desarrollador escribe código (Rama Feature).
    * El Data Steward/Senior aprueba (Merge Request).
    * El Sistema despliega (Automated Deploy).
    * *Resultado:* Ningún humano puede alterar datos en producción directamente sin dejar rastro y sin aprobación de un segundo par.
* **Riesgo Residual:** Los accesos privilegiados de emergencia (*Break-glass*) se consideran una excepción controlada, sujeta a logging reforzado y revisión obligatoria ex-post.
* **Alcance:** Los controles aquí descritos corresponden a mecanismos técnicos que apoyan objetivos específicos del estándar, y deben coexistir con el **sistema de gestión de seguridad de la información (SGSI)** definido por la organización.

### 3.3. GDPR / Regulaciones de Privacidad (Ley 21.719)
* **Objetivo:** Privacy by Design, Minimización y Derechos ARCO.
* **Enfoque Propuesto:**
    * **The Airlock:** Sanitización preventiva de PII antes de la ingesta al lago de datos.
    * **TTL Estructural:** Eliminación automática basada en políticas de retención configuradas en la infraestructura de almacenamiento.
    * **Decisiones Automatizadas:** Trazabilidad técnica de las variables y versiones de lógica utilizadas, permitiendo reconstruir y explicar el resultado en un nivel **proporcional, razonable y comprensible**, conforme a la naturaleza del tratamiento y a los derechos del titular.
* **Punto de Auditoría:** Revisar las políticas de ciclo de vida (Lifecycle Policies) y los logs inmutables de la API de ARCO. La responsabilidad probatoria recae en los roles definidos en el **Anexo A**.

### 3.4. MGDE / Normativa Pública Chilena
* **Objetivo:** Garantizar que los documentos electrónicos y sus datos base sean íntegros, auténticos y disponibles.
* **Enfoque Propuesto:**
    * **Extensión de Principios:** En el contexto de organismos sujetos al MGDE y entidades privadas **únicamente en la medida en que actúan como proveedores, encargados de tratamiento o actores intervinientes en expedientes administrativos electrónicos**, esta arquitectura no redefine el MGDE, sino que extiende sus principios de integridad hacia el origen digital del acto administrativo (la base de datos).
    * **Firma y Trazabilidad:** Uso de mecanismos criptográficos para asegurar que el dato que genera el documento no ha sido manipulado.
* **Punto de Auditoría:** Cotejar el linaje del dato en el sistema de gestión documental con los logs de la base de datos transaccional.

---

## 4. FILOSOFÍA DE LA PRUEBA (FACILITACIÓN DE AUDITORÍA)

Este enfoque busca facilitar la labor del auditor, reduciendo la dependencia de entrevistas subjetivas y muestreos manuales propensos a error. En la **Gobernanza Defensiva**, **la configuración del sistema es la primera línea de evidencia**.

**Guía para el Auditor:**

Para verificar la efectividad de los controles, recomendamos priorizar la evidencia sistémica sobre la declarativa:

1.  En lugar de solo revisar la "Política de Contraseñas" (PDF), solicitar la configuración de IAM que fuerza dicha política.
2.  En lugar de solo revisar el "Manual de Borrado", solicitar el log de ejecución del proceso de *Crypto-shredding*.

La documentación tradicional explica la intención del control; la evidencia técnica (Logs, Historial de Versiones, Configuraciones) demuestra su operación real e ininterrumpida.
Este enfoque no excluye el juicio profesional del auditor ni otras técnicas de auditoría, sino que prioriza evidencia objetiva cuando esta se encuentra disponible.

> **Integridad de la Evidencia (WORM):** Los logs de auditoría de esta plataforma se almacenan en repositorios de escritura única (*Write-Once-Read-Many*), garantizando que la evidencia histórica de las acciones del sistema no puede ser alterada ni siquiera por los administradores con mayores privilegios.

**Cláusula de Interpretación:** Este anexo debe ser interpretado como un instrumento de facilitación técnica para auditorías, no como una autoevaluación ni como una declaración de suficiencia normativa.