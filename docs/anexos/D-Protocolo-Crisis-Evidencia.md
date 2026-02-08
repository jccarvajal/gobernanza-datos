# Anexo D: Protocolos de Crisis y Evidencia Legal (Legal Engineering)

> **CLASIFICACIÓN:** RESTRINGIDO / USO EXCLUSIVO COMITÉ DE CRISIS

> **OBJETIVO:** DEFENSA JURÍDICA Y PRESERVACIÓN DE EVIDENCIA

> **ACTIVACIÓN:** INCIDENTE DE SEGURIDAD NIVEL 1 O REQUERIMIENTO JUDICIAL

---

## 1. INFRAESTRUCTURA DE PRESERVACIÓN (WORM)

Para **favorecer la admisibilidad de la evidencia en tribunales y maximizar su valor probatorio**, la arquitectura de logs de auditoría implementa **WORM (Write Once, Read Many)** en modo estricto (*Compliance Mode*).

**Garantía Técnica:**

* Una vez escrito, el log no puede ser modificado ni eliminado por ningún usuario, **incluyendo al Administrador del Sistema (Root)**, hasta que expire el periodo de retención legal configurado (ej. 5 años).
* **Alcance:** La inmutabilidad lógica se implementa mediante controles técnicos que impiden la modificación directa, sin perjuicio de las responsabilidades jerárquicas y administrativas asociadas a la gestión de la plataforma. Esta inmutabilidad protege contra corrupción interna, borrado accidental o ataque de *ransomware*.

> **Nota de Diligencia:** Las limitaciones físicas inherentes (ej. destrucción catastrófica del centro de datos) no invalidan la **debida diligencia** de la organización, en la medida que la arquitectura implemente redundancia geográfica y planes de continuidad acordes a la criticidad del tratamiento.

---

## 2. LA "CAJA NEGRA" JURÍDICA

En caso de litigio o investigación interna, la **principal fuente técnica de reconstrucción de los hechos** recae en los logs, **sin perjuicio de peritajes, declaraciones, documentación externa u otros medios de prueba legalmente pertinentes**. Para evitar la impugnación de la evidencia ("los logs fueron alterados"), el sistema mantiene una cadena de custodia criptográfica.

**Matriz de Evidencia:**

| Tipo de Evidencia | Fuente de Verdad | Integridad | Objetivo de Diseño (SLO) |
| :--- | :--- | :--- | :--- |
| **Quién entró** | Identity Provider (IdP) Logs | Hash Encadenado | Near Real-Time |
| **Qué vio** | Data Access Logs (S3/SQL Audit) | WORM Storage | < 15 min |
| **Qué cambió** | Change Data Capture (CDC) | Replicación Inmutable | < 5 min |
| **Intrusiones** | IDS / WAF Logs | Envío a SIEM externo | Inmediato |

*Nota Técnica:* El incumplimiento puntual de un SLO por falla sistémica constituye un evento de riesgo que debe ser registrado, pero no invalida *per se* la integridad de la evidencia histórica disponible.

> **Criterio Administrativo Interno:**
> La desactivación manual, alteración o interrupción deliberada de estos logs por parte de un usuario privilegiado constituye un **indicio administrativo relevante que amerita investigación prioritaria por posible ocultamiento**. Este indicio no produce efectos sancionatorios automáticos ni invierte la carga de la prueba, y su valoración se realizará exclusivamente dentro de un procedimiento contradictorio y fundado.

---

## 3. ROL DEL DPO (DATA PROTECTION OFFICER) EN CRISIS

Para garantizar la independencia y evitar conflictos de interés durante un incidente:

1.  **Acceso de Solo Lectura:** El DPO tiene acceso de auditoría irrestricto a la "Caja Negra", pero carece de permisos de escritura/configuración. No puede "arreglar" el problema, solo certificarlo.
2.  **Canal de Denuncia:** El DPO tiene la facultad de escalar el incidente conforme a los **estatutos de la organización, los protocolos formales de escalamiento vigentes** y, cuando la ley lo exija imperativamente, directamente a la Autoridad de Control si la Gerencia intenta ocultarlo.
3.  **No Intervención Operativa:** El DPO actúa como notario del desastre, no como bombero. La responsabilidad de contención técnica del incidente recae exclusivamente en los roles ejecutivos (CISO/CDO). La función del DPO es de garantía de derechos y fe pública, no de mitigación operativa.

> **Garantía de Independencia:** Esta limitación funcional no constituye pasividad ni negligencia, sino una garantía de independencia y segregación de funciones exigida por la normativa de protección de datos (Ley 21.719).

---

## 4. EL BOTÓN ROJO (KILL SWITCH)

Ante un ataque en curso (ej. Exfiltración masiva o Ransomware activo), el CISO o el CDO tienen la autoridad pre-delegada para activar el **Kill Switch** (Aislamiento de Emergencia).

**Criterio de Umbral:**
El Kill Switch solo podrá activarse cuando la no intervención inmediata implique un **riesgo cierto y superior** de daño legal, patrimonial o a los derechos de los titulares.

**Protocolo de Activación:**

1.  **Corte de Acceso:** Revocación inmediata de todas las sesiones de usuario y llaves de API externas.
2.  **Aislamiento de Red:** El Data Lake entra en modo "VPC Enclave" (sin salida a internet).
3.  **Congelamiento de Estado:** Se toman snapshots forenses de memoria y disco para análisis posterior.
4.  **Ratificación (Principio de Doble Llave Diferida):** Cuando la situación lo permita técnicamente, o a la mayor brevedad posible tras la activación, la medida deberá ser ratificada por un segundo rol ejecutivo habilitado (CEO, Gerente Legal o Riesgo), dejando constancia expresa en el expediente forense para evitar la concentración unipersonal de decisiones críticas.

> **Control Ex-Post (Proporcionalidad):**
> Toda activación del Kill Switch genera automáticamente un expediente forense con timestamp, responsable y justificación técnica. Este expediente será revisado *a posteriori* por el Comité de Crisis para validar que la medida fue **proporcional al riesgo** y se dejará constancia de las alternativas menos gravosas que fueron descartadas por inviabilidad técnica inmediata.

---

## 5. LISTA DE CONDUCTAS CRÍTICAS DE ALTO RIESGO

Las siguientes acciones ("Ingeniería Maliciosa"), **cuando concurran los elementos de dolo o negligencia inexcusable**, no se consideran errores de configuración estándar, sino tipos agravados de conducta en la normativa interna, sujetos a las **sanciones que correspondan conforme a la normativa interna aplicable y al debido proceso**:

1.  **Bypassing:** Crear túneles o accesos traseros (*Backdoors*) para evadir los controles de seguridad o el Airlock.
2.  **Hardcoding de Secretos:** Escribir contraseñas o llaves de API en código fuente o repositorios Git públicos/compartidos.
3.  **Ofuscación:** Usar técnicas para impedir deliberadamente la lectura de logs o la auditoría de código.
4.  **Exfiltración No Autorizada:** Mover datos clasificados a dispositivos personales o nubes no corporativas sin usar los canales oficiales.

> **Condición de Dolo:**
> Estas conductas se sancionarán conforme a la gravedad acreditada, la reiteración, el daño causado y demás criterios legales. Los errores técnicos involuntarios, derivados de la falta de capacitación o experiencia, serán tratados mediante planes de mejora y formación, no mediante medidas disciplinarias expulsivas.

---

**Alcance de Activación:** Este anexo se activa exclusivamente en escenarios de crisis definidos en su encabezado. **Cualquier aplicación de este anexo fuera de los supuestos de activación definidos se considerará una desviación de procedimiento.**