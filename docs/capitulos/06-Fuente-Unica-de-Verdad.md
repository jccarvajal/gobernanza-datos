# Capítulo 06. La Fuente Única de Verdad (SSOT)
### De la Filosofía a la Evidencia Forense

> *"En un juicio o una auditoría, no importa qué sistema tiene la razón filosófica. Importa qué sistema fue declarado previamente como la Autoridad de Registro. La Fuente Única de Verdad (SSOT) no es una búsqueda epistemológica sobre la realidad; es una designación política y técnica de responsabilidad."*

## 6.1. La Falacia de la Verdad Absoluta

Las organizaciones pierden años intentando que "todos los datos coincidan" en todos los sistemas. Es una batalla perdida contra la entropía.
En la **Gobernanza de Datos Defensiva**, no buscamos obsesivamente que el Marketing y Finanzas tengan *la misma opinión* sobre un cliente. Buscamos saber exactamente **a quién atribuir la responsabilidad** si el dato es incorrecto.

El SSOT (*Single Source of Truth*) se redefine aquí no como "el dato perfecto", sino como el **Dato Oficial Defendible**.
Si la organización tiene dos relojes (dos bases de datos de clientes) y marcan horas distintas, no tiene "más información"; tiene **parálisis cognitiva** y debilidad legal. Ante una discrepancia, el sistema designado como SSOT prevalece por decreto, no por democracia.

---

## 6.2. El Golden Record como Activo Legal

Cuando consolidamos datos de múltiples fuentes (CRM, ERP, Legacy) en un "Golden Record" (Registro de Oro), estamos realizando un acto editorial: estamos creando una nueva **entidad legal**.

Este registro debe cumplir con el principio de **Inmutabilidad de Origen**:

* Si el SSOT dice que el cliente aceptó el contrato el día 12, ese dato es la verdad oficial de la empresa.
* Cualquier otro sistema (Excel local, App departamental) que diga "día 13" es, por definición técnica, **ruido o error**.

El Golden Record no busca la perfección platónica; busca la **Trazabilidad**. Su función es concentrar la titularidad del error en un solo punto para que pueda ser auditado y corregido.

> **Nota de Arquitectura (Log Inmutable):** Cuando hablamos de inmutabilidad, nos referimos al *Log de Cambios*. Si hay un error en el Golden Record, no se "sobrescribe" el pasado borrándolo; se añade un nuevo evento de corrección que anula el estado anterior. Esto garantiza que siempre podamos reconstruir qué creía la empresa que era verdad en cualquier fecha pasada.

---

## 6.3. Arquitectura de la Consistencia

Para lograr esto, la arquitectura debe prohibir las copias no gobernadas.
Implementamos el patrón de **Pub/Sub con Validación**:

1.  **Emisión:** El Sistema Productor emite el evento (ej. `ClienteCreado`, `DireccionActualizada`).
2.  **Validación:** El Hub de Gobernanza (SSOT) valida el evento contra las reglas de calidad y lo registra como "Hecho Confirmado".
3.  **Consumo:** Los Sistemas Consumidores (Marketing, Riesgo) leen *solo* del Hub, nunca se conectan entre ellos punto a punto.

**El Rol del Excel:**
Excel es bienvenido como herramienta de **laboratorio** (análisis de hipótesis, proyecciones), pero está vetado como herramienta de **fábrica** (reporte oficial). Un reporte que nace en Excel y cuyos datos no pueden ser replicados automáticamente desde el SSOT es una opinión personal, no un hecho corporativo.

---

## 6.4. Conclusión: El Dato como Testigo

Al final del día, el SSOT es su testigo estrella ante la Agencia de Protección de Datos o el Tribunal.

* Si usted tiene tres sistemas diciendo cosas distintas sobre un usuario, su testigo se contradice bajo juramento y usted pierde el caso.
* Si usted tiene una Fuente Única, aunque contenga un error humano puntual, usted tiene una **historia coherente y auditable** que demuestra debida diligencia en la gestión de la información.

La SSOT impone un régimen autoritario sobre los **Hechos Base** (lo que ocurrió), para permitir una democracia liberal sobre la **Analítica** (qué decisiones tomamos al respecto).