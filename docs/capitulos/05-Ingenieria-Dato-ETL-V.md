# Capítulo 05. Ingeniería del Dato: De ETL a ETL-V

> *"El modelo tradicional de ETL (Extraer, Transformar, Cargar) asumía que el ingeniero de datos era un conserje cuyo trabajo era limpiar silenciosamente el desastre que otros dejaban. Ese modelo es insostenible. En la nueva arquitectura, el ingeniero es un inspector de aduanas: si el dato no trae sus papeles en regla, se queda en la frontera."*

## 5.1. La Muerte del "Transform" Silencioso

Durante décadas, la "T" de ETL fue el refugio de la lógica sucia. Si Ventas ingresaba mal la región, Ingeniería escribía un script (`IF region IS NULL THEN 'Unknown'`) para que el reporte no fallara.
Esta práctica parece proactiva, pero es un cáncer de gobernanza: **oculta el error operativo del negocio**.

**El Nuevo Paradigma: ETL-V (Verificación)**
La tubería (*pipeline*) pierde el permiso para "adivinar", "maquillar" o "parchar" errores de negocio.

**Distinción Técnica Crítica:**
Debemos diferenciar estrictamente entre dos tipos de transformaciones:

1.  **Normalización Técnica (Permitida):** Convertir fechas a UTC, estandarizar monedas a ISO 4217, *trimming* de espacios, casting de tipos. Esto es higiene de formato necesaria para que el sistema funcione.
2.  **Sanitización de Negocio (Prohibida en Producción):** Rellenar campos obligatorios vacíos (imputación ciega), asumir valores por defecto en datos maestros o corregir lógica de negocio rota (ej. "si la edad es negativa, poner 0").

> **Línea de Corte:** En una arquitectura ETL-V, cualquier corrección automática que oculte un error de origen se considera una falla de gobernanza. Un dato de negocio corregido silenciosamente aguas abajo es evidencia de una falla aguas arriba que debe resolverse en el origen.
>
> *Nota:* Esta restricción aplica severamente al **Dato Certificado** para consumo oficial. Los entornos de *Sandbox* o Exploración pueden permitir reglas más laxas, pero ese dato tiene prohibido el paso a reportes financieros o regulatorios.

---

## 5.2. La Zona de Cuarentena (Dead Letter Queue)

Cuando un registro es rechazado por el validador (ej. "Edad: -5"), no se borra (perderíamos trazabilidad) ni se carga al destino (corromperíamos la verdad). Se envía a la **Zona de Cuarentena** o *Dead Letter Queue* (DLQ).

La Cuarentena es un estado formal de existencia del dato:

* **Existe físicamente:** Está guardado en el almacenamiento (S3/Blob) y es auditable.
* **No existe legalmente:** No es visible para consumo, no reporta, no decide y no entrena modelos.

**Mecanismo de Rehabilitación (Salida):**
La Cuarentena no es un cementerio; es una sala de espera. Para que un dato salga de ahí y entre al *Data Lake* oficial, se requiere una transacción explícita:

1.  **Reprocesamiento:** El productor corrige el dato en el origen y lo reenvía.
2.  **Excepción Firmada:** Un *Data Steward* autoriza la ingesta del dato defectuoso asumiendo el riesgo (trazable en logs).

**Higiene de la Cuarentena (TTL):**
La DLQ no puede ser un vertedero infinito. Se debe establecer una política de retención (ej. 30 días). Si el dato no es reclamado o corregido en ese plazo, se elimina o se archiva en frío (*Cold Storage*), asumiendo la pérdida como costo operativo.

---

## 5.3. Data Contracts: La Diplomacia Armada

Para evitar que la tubería se rompa cuando un sistema *legacy* cambia un esquema sin avisar, implementamos **Contratos de Datos** (*Data Contracts*).

Un contrato es una definición de interfaz (YAML/JSON) que estipula esquema, frescura, SLIs y semántica.
No es documentación en una Wiki que nadie lee; **es un test de integración que corre en el CI/CD del Productor.** Si el productor rompe el contrato, su propio despliegue falla antes de llegar a producción.

**Realidad Operativa:**
Sabemos que no siempre se puede controlar el sistema origen (ej. un SaaS externo tipo Salesforce o SAP). En esos casos, el Contrato actúa como **testigo de fallo**.
Si el proveedor rompe el contrato, el incidente se detecta inmediatamente en la ingesta, alertando al equipo antes de que el dato contamine los reportes. El contrato hace visible la fragilidad de la integración y asigna la responsabilidad de la reparación.

---

## 5.4. Observabilidad: Circuit Breakers

Monitorear no es solo ver dashboards de "jobs exitosos" (verde/rojo). En la **Ingeniería de Datos Defensiva**, monitoreamos la salud del activo, no solo la del servidor.

Implementamos **Observabilidad de Datos** para medir anomalías en volumen, distribución y frescura.
Pero la métrica sin acción es irrelevante. La arquitectura debe implementar el patrón de **Circuit Breaker** (Cortacircuitos).

* **Escenario:** Un proceso de carga diario suele traer 10.000 registros de ventas. Hoy trae solo 500. El job técnico dice "éxito" (porque corrió sin errores de código).
* **Acción:** El *Circuit Breaker* estadístico detecta la anomalía de volumen (-95%). Se dispara automáticamente, detiene el pipeline y evita que se actualicen los tableros.
* **Resultado:** Es preferible un reporte desactualizado (pero íntegro) a uno actualizado con datos parciales falsos que lleven a decisiones erróneas.

---

## 5.5. Conclusión: Certeza Industrial

El objetivo del Capítulo 5 es pasar de la "artesanía de datos" (arreglar cosas a mano para que funcionen) a la "ingeniería industrial".

Buscamos reducir la carga cognitiva del consumidor.
Cuando un ejecutivo ve un número en un tablero, no debería tener que preguntarse si pasó por el filtro de calidad o si fue "arreglado" creativamente en el camino.
La arquitectura ETL-V garantiza que el dato que llega al final es un **Dato Certificado**. No es un sobreviviente de la suerte; es un producto que ha pasado el control de calidad y aduana.