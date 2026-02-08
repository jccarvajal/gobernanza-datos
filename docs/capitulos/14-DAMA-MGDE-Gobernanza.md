# Capítulo 14. DAMA, MGDE y la Gobernanza Ejecutable

> *"Un marco de gobernanza que no puede ejecutarse ni auditarse en tiempo real no es una arquitectura: es una aspiración. Mientras la gobernanza permanezca en documentos, el sistema seguirá decidiendo solo."*

## 14.1. Por qué DAMA y MGDE siguen siendo necesarios (pero insuficientes)

Los marcos tradicionales de gobernanza de datos —en particular **DAMA-DMBOK2** a nivel global y el **Modelo de Gestión de Documentos Electrónicos (MGDE)** en el sector público chileno— han cumplido un rol histórico fundamental: proporcionar un lenguaje común, una taxonomía compartida y una estructura conceptual para ordenar el caos informacional.

Sin DAMA y MGDE, la gobernanza se fragmenta en iniciativas aisladas, dependientes de "héroes" y sin coherencia institucional. Son la base semántica indispensable.

> **Nota de Contexto Institucional:** El MGDE no es una recomendación técnica opcional; es una **política pública transversal del Estado de Chile**, impulsada por la División de Gobierno Digital y exigible por los organismos de control. Ignorarlo no es una decisión tecnológica, sino un incumplimiento normativo.

Sin embargo, estos marcos nacieron en una época tecnológica distinta:

* Previa a la IA Generativa masiva.
* Previa a la fiscalización técnica automatizada (APIs de control).
* Previa a la exigencia de responsabilidad proactiva verificable (Ley 21.719).

**El Problema del Tramo Final**

El problema no es DAMA ni MGDE; el problema es detenerse en ellos.
Ambos marcos describen brillantemente **qué** debería gobernarse, pero carecen de mecanismos nativos para garantizar que el sistema **obedezca**. Definen principios, roles y artefactos documentales, pero dejan abierta la brecha crítica entre la *declaración de cumplimiento* (el papel) y el *comportamiento real del sistema* (el log).

Este libro no busca reemplazar DAMA ni MGDE. Busca absorberlos, endurecerlos y convertirlos en **estados técnicos ejecutables**.

---

## 14.2. Gobernanza Declarativa vs. Gobernanza Ejecutable

La distinción central de la **Gobernanza de Datos Defensiva** radica en el tipo de respuesta que el sistema puede ofrecer ante una auditoría.

| Enfoque | Pregunta que responde | Artefacto Típico |
| :--- | :--- | :--- |
| **Gobernanza Declarativa** | *"¿Qué deberíamos estar haciendo?"* | Políticas PDF, Manuales, Comités. |
| **Gobernanza Ejecutable** | *"¿Puede el sistema demostrar que lo hizo?"* | Logs WORM, Bloqueos de Pipeline, Código. |

DAMA y MGDE operan mayoritariamente en el primer nivel (normativo). La **Gobernanza Defensiva** opera estrictamente en el segundo (operativo).

> **Principio de Auditoría:** La gobernanza ejecutable no elimina la declarativa (necesitamos saber las reglas), pero la vuelve exigible. Exige que cada principio normativo se materialice como una restricción técnica, un control automatizado o un registro inmutable. Si un control no puede auditarse sin intervención humana (entrevistas), no es gobernanza; es confianza.

---

## 14.3. Traducción Directa: DAMA $\rightarrow$ Arquitectura

Para evitar la reinvención de la rueda, adoptamos los dominios de conocimiento de DAMA, pero los reinterpretamos como componentes de arquitectura defensiva.

| Dominio DAMA | Enfoque Tradicional (Declarativo) | Gobernanza Defensiva (Ejecutable) |
| :--- | :--- | :--- |
| **Data Lifecycle** | Política de Retención (Papel) | **TTL** (Time-To-Live) automático + Linaje activo. |
| **Data Quality** | Reportes de Calidad ex-post | **ETL-V** (Verificación) y Gates de bloqueo en pipeline. |
| **Metadata** | Diccionario en Excel / Wiki | **Metadatos Computables** (consumibles por el sistema). |
| **Stewardship** | Rol humano de supervisión | **Observabilidad** automática + Circuit Breakers. |
| **Ownership** | Designación formal de cargo | **Responsabilidad Probatoria** (Anexo A). |
| **Master Data** | Modelo Lógico / Diagramas | **SSOT** (Fuente Única) forzada por API. |
| **Data Security** | Controles de acceso (Matriz) | **IAM** + Cifrado BYOK + Logs WORM. |

La diferencia no es semántica; es operativa. En esta arquitectura, ningún dominio crítico depende exclusivamente de la disciplina humana. El error humano se asume como inevitable y se mitiga con diseño restrictivo.

---

## 14.4. MGDE: El Dato como Pre-Documento

El **MGDE** introduce una distinción vital para la administración del Estado: no todo archivo es un documento, y no todo documento tiene valor probatorio. Exige cuatro atributos: **Autenticidad, Integridad, Disponibilidad y No Repudio**.

Tradicionalmente, se intenta garantizar estos atributos solo al final del proceso, cuando se genera el PDF firmado. Este libro extiende el principio aguas arriba:

**El documento administrativo comienza antes del documento. Comienza en el dato que lo origina.**

En los sistemas modernos, el acto administrativo, la fiscalización, la sanción, el informe y la resolución son **derivados de datos transaccionales**.

* Si el dato de origen no tiene linaje...
* Si no tiene control de versiones...
* Si su integridad no es verificable criptográficamente...

Entonces el documento final generado puede ser *formalmente válido*, pero es *materialmente impugnable*.

> **Ruptura de la Cadena de Custodia:** En este marco, los **procesos híbridos papel-digital** (donde un dato se imprime, se firma a mano y se escanea) no son una etapa intermedia aceptable, sino una fuente estructural de ruptura de la cadena de custodia y de pérdida de integridad del dato original.

**Extensión de Autenticidad:**
La **Firma Electrónica Avanzada** y los mecanismos de autenticación oficial (como **ClaveÚnica**) no son accesorios tecnológicos externos; son la extensión natural de los principios de autenticidad y no repudio definidos por el MGDE, aplicados ahora al nivel del dato.

---

## 14.5. Ciclo de Vida: Del Concepto al Código

MGDE y DAMA definen ciclos de vida conceptuales. Nosotros los traducimos a mecanismos de ingeniería forense.

| Fase MGDE | Estado en Arquitectura | Implementación Técnica |
| :--- | :--- | :--- |
| **Archivo Corriente** | Producción (Hot) | Acceso controlado, alta disponibilidad, CDC activo. |
| **Archivo Intermedio** | Retención (Warm) | Acceso restringido, solo lectura, TTL configurado. |
| **Archivo Histórico** | Preservación (Cold) | **Logs WORM**, Snapshots forenses, Inmutabilidad. |
| **Eliminación** | Destrucción Final | **Crypto-shredding** verificable (Borrado de llaves). |

Aquí ocurre un quiebre doctrinal importante:

1.  No todo dato debe conservarse (contra la acumulación del "Dato Uranio").
2.  Pero todo borrado debe poder probarse.

El borrado deja de ser una acción administrativa ("limpiar la carpeta") para convertirse en un **evento técnico auditable** necesario para la defensa legal.

---

## 14.6. Resolución Técnica de Roles

Este libro no elimina los roles clásicos definidos por los marcos teóricos; los protege del colapso operativo mediante herramientas.

| Rol Tradicional | Riesgo Clásico | Resolución en la Arquitectura |
| :--- | :--- | :--- |
| **Data Owner** | Figura nominal (firma sin mirar) | Se le asigna **Responsabilidad Probatoria** real. |
| **Data Steward** | Sobrecarga operativa y burnout | Se le da **Automatización** y Observabilidad. |
| **Archivista** | Aislado al final del proceso | Se integra al **Linaje** desde el origen. |
| **TI** | Ejecutor ciego de tickets | **Arquitecto Responsable** (Garante de integridad). |

La arquitectura asume tres verdades incómodas:

1.  Ningún rol humano puede garantizar cumplimiento 24/7 por sí solo.
2.  Ningún comité puede reaccionar a la velocidad de la IA.
3.  Ninguna política manual sobrevive al primer atajo operativo urgente.

Por eso, el control primario se mueve de las personas al sistema, permitiendo que las personas ejerzan una supervisión de alto nivel (auditoría de reglas) en lugar de una revisión mecánica de filas.

---

## 14.7. Conclusión: El Contrato y el Mecanismo

Este libro no compite con DAMA ni con MGDE. Define su lugar exacto en la estrategia de supervivencia:

* **DAMA y MGDE** establecen el **Contrato Social** de la información (el *Qué* y el *Por Qué*).
* **La Gobernanza Defensiva** define el **Mecanismo de Ejecución** (el *Cómo* forzoso).

Sin DAMA/MGDE, la arquitectura carecería de legitimidad institucional y taxonomía estándar.
Sin una arquitectura ejecutable, DAMA/MGDE carecen de poder real ante una crisis.

La convergencia de ambos no es opcional. Es el único camino viable en un entorno donde la fiscalización ya no lee intenciones, sino que audita resultados.