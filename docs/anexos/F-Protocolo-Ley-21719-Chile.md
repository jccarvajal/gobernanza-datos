# Anexo F: Protocolo de Adecuación Ley 21.719 (Chile 2026)
**(Plan de Batalla y Gestión de Riesgo Personal)**

### Situación: Estado de Guerra Regulatoria

La **Ley 21.719** sobre Protección de Datos Personales en Chile transforma la gestión de datos de un problema técnico a un riesgo legal de nivel directorio.
A partir de su entrada en vigencia, la "buena fe" deja de ser eximente. La carga de la prueba se invierte: la organización debe demostrar matemáticamente (trazabilidad) que sus datos son lícitos.

Este anexo es un **cronograma de supervivencia**.
Está diseñado para un CDO que asume en **Enero 2026** y tiene menos de 12 meses para evitar sanciones que pueden alcanzar el 4% de los ingresos anuales o 20.000 UTM, además de la responsabilidad civil personal.

---

### Cronograma de Ejecución 2026 (Defcon 1)

Este cronograma no es una recomendación técnica opcional; es la última ventana operativa razonable antes de la pérdida de control y la exposición a pasivos legales irreversibles.

#### Fase 1: Diagnóstico y Cuarentena (Q1 - Enero/Marzo)
**Objetivo:** Detener la hemorragia y mapear el "Dato-Uranio".
* **Acción 1 (Día 0): Congelamiento de Esquemas.** Se prohíbe la creación de nuevas tablas productivas o ingestión de nuevas fuentes sin un esquema validado y clasificado (Ver Cap. 09 - Airlock).
* **Acción 2: Inventario de Pasivos.** Ejecución de descubrimiento automatizado (Data Discovery) para identificar PII (Información Personal Identificable) en bases de datos legadas, logs y ambientes de desarrollo.
* **Acción 3: Clasificación Legal.** Etiquetado masivo de datos según base de licitud:
    * *Verde:* Contrato vigente o Ley.
    * *Amarillo:* Interés legítimo (requiere prueba de ponderación).
    * *Rojo:* Consentimiento tácito, datos antiguos o sin origen claro (Tóxicos).

#### Fase 2: Ingeniería de Defensa (Q2 - Abril/Junio)
**Objetivo:** Construir los muros de contención (Privacy by Design).
* **Acción 1: Implementación de Airlock.** Despliegue de barreras de entrada en el Data Lake. Ningún dato entra sin metadatos de origen, propósito y retención (TTL).
* **Acción 2: Gate EIPD en CI/CD.** Bloqueo automatizado en los pipelines de despliegue para cualquier software que procese datos personales sin una Evaluación de Impacto (EIPD) aprobada.
* **Acción 3: Derechos ARCO Automatizados.** Desarrollo de APIs para responder a solicitudes de Acceso, Rectificación, Cancelación y Oposición en <48 horas, sin intervención humana manual.

#### Fase 3: Purga y Transparencia (Q3 - Julio/Septiembre)
**Objetivo:** Neutralizar el material peligroso y cortar cadenas de suministro tóxicas.
* **Acción 1: La Gran Purga (Crypto-shredding).** Eliminación verificable de datos clasificados como "Rojos" (Tóxicos) o con TTL vencido. En sistemas distribuidos, esto se ejecuta mediante el borrado de las llaves de cifrado.
* **Acción 2: Ultimátum SaaS.** Auditoría de terceros. Bloqueo o migración de proveedores (CRM, Marketing, RRHH) que no certifiquen cumplimiento técnico de la Ley 21.719 o GDPR.
* **Acción 3: Registro de Actividades.** Generación del "Inventario de Tratamiento" exigido por la ley, derivado automáticamente del Catálogo de Datos (no de entrevistas).

#### Fase 4: Simulacro y Go-Live (Q4 - Octubre/Noviembre)
**Objetivo:** Validar la resistencia bajo fuego real.
* **Acción 1: Simulacro de Brecha.** Ejecución de un incidente controlado (Red Team). Prueba de notificación a la Agencia en <72 horas utilizando Linaje de Datos y Logs Inmutables.
* **Acción 2: Auditoría de "Caja Negra".** Revisión forense externa simulando una fiscalización hostil. Búsqueda de discrepancias entre la "Verdad Documental" y la "Verdad del Sistema".
* **Acción 3: Code Freeze Pre-Vigencia.** Congelamiento total de cambios arquitectónicos no críticos hasta enero 2027.

---

### Hito Crítico: 01 de Diciembre 2026
**Inicio de Vigencia Sancionatoria.**

A partir de este segundo, cualquier dato no gobernado es un pasivo financiero y legal activo. La arquitectura debe operar en modo "Zero Trust" y generar evidencia continua de cumplimiento (Accountability).

---

### Criterios de Control y Escalamiento (El Tablero de Mando)

Para asegurar que este plan no sea una fantasía administrativa, se establecen los siguientes controles binarios y responsabilidades.

#### 1. Definition of Done (¿Cuándo termina una fase?)
* **Fase 1 (Diagnóstico):**
    * [ ] 100% de las bases de datos productivas escaneadas.
    * [ ] Inventario de PII Huérfana (sin dueño) < 5% del total.
    * [ ] Gate de "Congelamiento de Esquemas" activo y bloqueando.
* **Fase 2 (Ingeniería):**
    * [ ] Gate EIPD bloqueando despliegues en CI/CD (al menos 1 bloqueo real demostrado y documentado).
    * [ ] API de Derechos ARCO funcional en ambiente de Staging.
* **Fase 3 (Purga):**
    * [ ] Evidencia criptográfica de destrucción de datos "Rojos" (Logs de borrado de llaves).
    * [ ] 100% de proveedores SaaS críticos certificados o bloqueados por firewall.
* **Fase 4 (Simulacro):**
    * [ ] Notificación de brecha simulada generada en <72 horas con linaje completo.
    * [ ] 0 Hallazgos Críticos en auditoría externa de caja negra.

#### 2. Matriz de Responsabilidad (RACI de Crisis)
*Quien figura como "Accountable" responde con su cargo ante el fallo de la fase.*

| Fase | Responsible (Ejecuta) | Accountable (Responde) | Consulted (Opina) | Informed (Sabe) |
| :--- | :--- | :--- | :--- | :--- |
| **Q1: Diagnóstico** | Arquitecto de Datos | **CDO** | DPO, Legal | Directorio |
| **Q2: Ingeniería** | Lead DevOps / Data Eng | **CTO** | CDO, DPO | Directorio |
| **Q3: Purga** | CISO / Ops | **CEO / Gerente General** | Legal, Compras | Directorio |
| **Q4: Simulacro** | CISO / Red Team | **CDO** | Legal, Auditoría | Directorio |

*> Nota: El CEO/Gerente General es Accountable en Fase 3 porque la purga de datos históricos y el bloqueo de proveedores críticos constituyen decisiones de continuidad de negocio con impacto directo en ingresos y operación. La arquitectura propone; la gerencia general decide y asume el riesgo comercial.*

#### 3. Red Flags de Escalamiento (Gatillos Automáticos)
El CDO tiene la **obligación** de escalar formalmente al Directorio (mediante Acta) si ocurre cualquiera de los siguientes eventos:

1.  **Hallazgo Masivo (Q1):** El diagnóstico revela que >15% de los datos históricos carecen de base legal trazable.
2.  **Bloqueo Técnico (Q2):** La deuda técnica impide implementar el Gate EIPD en sistemas core.
3.  **Resistencia de Proveedor (Q3):** Un proveedor SaaS crítico se niega a firmar adendas de cumplimiento y no existe alternativa viable inmediata.
4.  **Fallo de Simulacro (Q4):** La organización tarda >72 horas en generar el informe forense de una brecha simulada.

*En caso de escalamiento, el Directorio debe firmar una **Transferencia de Riesgo** (ver Anexo A) o aprobar un presupuesto de emergencia.*

#### 4. Conexión con Anexo E
Este cronograma opera en conjunto con el **Anexo E (Checklist de Supervivencia)**.

* El **Anexo E** es la evaluación de estado *inmediata* (Día 1 a Día 90).
* El **Anexo F** es la hoja de ruta de *transformación* anual (Mes 1 a Mes 12).
* *Advertencia:* Si el Anexo E arroja un resultado de "Indefenso", la Fase 1 de este cronograma debe ejecutarse en modo de emergencia (doble turno).
