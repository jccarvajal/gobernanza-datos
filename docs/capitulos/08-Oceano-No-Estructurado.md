# Capítulo 08. El Océano No-Estructurado

> *"El 80% del conocimiento de tu empresa no vive en bases de datos SQL ordenadas. Vive en correos electrónicos, contratos en PDF, chats de Slack y grabaciones de llamadas. Hasta ahora, ignorábamos este caos porque era difícil de procesar. Con la IA, ignorarlo ya no es una opción: es renunciar a la mayor fuente de valor o activar la mayor fuente de riesgo."*

## 8.1. Dark Data: El Activo Latente (y Tóxico)

Llamamos **Dark Data** (Datos Oscuros) a la información que la organización recolecta, procesa y almacena, pero que nunca utiliza para fines analíticos. Es el iceberg sumergido.
Históricamente, la mentalidad fue: "Guardémoslo, el almacenamiento es barato, ya veremos para qué sirve".

En la era de la IA, esta lógica es peligrosa. Un servidor de archivos lleno de documentos de hace 10 años contiene tanto **Valor** (Propiedad Intelectual) como **Riesgo** (PII olvidado, evidencia de malas prácticas). Si conectas un LLM a este repositorio sin auditar, la IA extraerá ambos con igual entusiasmo.

> **Regla de Descarte:** En ausencia de una **hipótesis de uso explícita aprobada por un Data Owner** o de una obligación regulatoria de retención (*Legal Hold*) documentada, el Dark Data se presume un pasivo. La política de gobernanza por defecto debe ser la eliminación segura, no la retención indefinida. Guardar "por si acaso" es una estrategia de riesgo, no de patrimonio.

---

## 8.2. Ingeniería de Corpus (Gestión Documental 2.0)

La antigua "Gestión Documental" trataba de organizar archivos en carpetas para humanos. La nueva **Ingeniería de Corpus** trata de preparar texto para máquinas.
El PDF escaneado (imagen) es el enemigo. Para una máquina, es una mancha de píxeles opaca. La **Gobernanza Defensiva** exige transformar todo el no-estructurado en formatos legibles (JSON, Markdown, Texto Plano).

> **Criterio de Existencia:** Un documento que no es **técnicamente legible** (OCR de alta calidad, texto extraíble) es invisible para la inteligencia corporativa. Puede seguir existiendo como evidencia forense en un "Archivo Muerto" para cumplimiento legal, pero deja de ser un activo de conocimiento explotable. Si la IA no puede leerlo, no puede aprender de él.

---

## 8.3. Los Metadatos como SSOT del No-Estructurado

En una base de datos SQL, la estructura (tablas, columnas) nos dice qué es el dato. En un documento de Word o un email, no hay estructura rígida; el contenido es libre.
Por eso, en el mundo no-estructurado, **el sistema de metadatos es la Fuente Única de Verdad (SSOT).**

No podemos confiar en que el usuario escriba "CONFIDENCIAL" dentro del cuerpo del documento. Debemos confiar en la etiqueta de metadato `classification_level: confidential` adherida al archivo por el sistema de gobierno.

> **Protocolo de Conflicto:** A menudo, el contenido contradice al metadato (ej. un documento marcado en el sistema como "Público" contiene tarjetas de crédito en el texto). En caso de conflicto, el sistema debe confiar en la evidencia de riesgo y **aplicar automáticamente la clasificación más restrictiva**. La seguridad siempre prevalece sobre la intención declarada del autor.

---

## 8.4. El "Wild West" del Texto Libre

El campo de "Texto Libre" (Comentarios, Notas, Chats) es la pesadilla del Oficial de Cumplimiento. Es donde los empleados escriben lo que no deberían: claves, insultos, diagnósticos médicos no oficiales.

La gobernanza moderna implementa **DLP (Data Loss Prevention) Semántico** en el flujo de ingestión. Antes de que un texto libre entre al Data Lake o al modelo de IA, pasa por filtros de Regex y modelos NLP que detectan patrones sensibles.

> **Blindaje Técnico (Defensa en Profundidad):** El DLP Semántico es un control probabilístico (puede fallar), por lo tanto, **no sustituye** los controles de acceso (IAM) ni la encriptación. Es una capa adicional de higiene. Un sistema que permite ingresar una tarjeta de crédito en un campo de comentarios sin alertar o enmascarar es un sistema defectuoso por diseño.

---

## 8.5. Conclusión: Higiene Alimentaria para la IA

Imagina que vas a cocinar para un banquete (entrenar una IA). El Capítulo 8 ha sido sobre la selección de ingredientes. Si lanzas al modelo todo lo que encuentras en la basura (Dark Data sin filtrar), el resultado será una intoxicación masiva.

La **Ingeniería de Corpus** es la higiene alimentaria de la IA. Limpiamos, etiquetamos, clasificamos y descartamos lo podrido *antes* de cocinar.

> **Advertencia de Irreversibilidad:** Una vez que el dato no-estructurado entra sin control al corpus de entrenamiento (*Fine-Tuning*), la corrección posterior es matemáticamente imposible sin reentrenar el modelo desde cero (costo masivo). En arquitecturas RAG (memoria externa), el daño es mitigable borrando el vector, pero el impacto de una respuesta tóxica ya emitida por el modelo es irreversible.