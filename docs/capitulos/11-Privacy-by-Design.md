# Capítulo 11. Privacy by Design: La Ley como Código

> *"Los abogados creen que protegen la privacidad escribiendo políticas de 50 páginas que nadie lee. Los ingenieros saben que la única forma de proteger la privacidad es haciendo técnicamente inviable violarla. La ley debe dejar de ser un documento PDF para convertirse en una restricción de clave foránea en la base de datos."*

## 11.0. Preámbulo: La Frontera de lo Posible (Doctrina de Mitigación)

Antes de detallar los mecanismos de privacidad, es imperativo establecer un acuerdo de realidad.
Entre la promesa de seguridad total (imposible) y la resignación ante el caos (negligente), existe el único terreno donde la ingeniería y el derecho pueden encontrarse: la **Debida Diligencia Demostrable**.

Esta arquitectura se rige por tres principios de honestidad técnica:

1.  **Inexistencia del Riesgo Cero:** No prometemos "inmunidad" o "seguridad perfecta". Prometemos **Defensabilidad**. No podemos garantizar matemáticamente que un sistema jamás fallará, pero sí que implementamos el estado del arte para impedirlo.
2.  **Mitigación Demostrable:** La ley no exige magia; exige diligencia. La diferencia entre una multa devastadora y una observación administrativa radica en la capacidad de probar que el riesgo fue identificado y que los controles eran proporcionales.
3.  **Riesgo Residual como Activo:** Todo lo que la tecnología no puede resolver al 100% (latencia de borrado, memoria profunda de LLMs) no se esconde. Se declara formalmente como **Riesgo Residual Documentado**. La culpa nace del ocultamiento, no de la limitación técnica conocida.

---

## 11.1. Policy as Code (La Ley como Código)

Tradicionalmente, Legal y Tecnología operan en universos paralelos. Legal dice "No conservar datos más de 5 años" y TI guarda backups eternos "por si acaso". Esta desconexión crea una brecha de cumplimiento masiva.

El paradigma de **Privacy by Design** se implementa mediante **Policy as Code**.
Las reglas legales se traducen en scripts que gobiernan la infraestructura.

* **Legal:** "Datos europeos no salen de la UE."
* **Código:** Una política IAM que bloquea replicación a `us-east-1`.

> **Atribución de Responsabilidad:** En esta **Gobernanza Defensiva**, un incumplimiento ya no es atribuible a un "error humano aislado" de un operador, sino a una decisión de diseño que la organización aprobó. Si el sistema permitió la infracción, la negligencia es estructural, no individual.
>
> *Nota:* Esto no elimina la responsabilidad personal en caso de dolo (saltarse un control deliberadamente), pero desplaza la carga de la prueba hacia la robustez del sistema.

---

## 11.2. La Arquitectura del Olvido (TTL)

El mayor riesgo legal no es perder datos, sino **tener datos que no deberías tener**.
La arquitectura debe implementar mecanismos de **Muerte Programada** o TTL (Time To Live).

**Mecanismos de Ejecución:**
El "Derecho al Olvido" no siempre implica `DELETE`. Dependiendo del contexto regulatorio, puede ejecutarse como:

1.  **Eliminación Física:** Borrado seguro (Crypto-shredding).
2.  **Anonimización Irreversible:** Retención con fines estadísticos.
3.  **Legal Hold (Excepción):** Bloqueo de borrado ante litigios pendientes.

> **Memoria de la Decisión:** El borrado elimina el registro físico del dato personal (ej. el sueldo exacto), pero **no invalida el log de la decisión histórica** tomada con él (ej. "Crédito rechazado por capacidad de pago insuficiente"). El diseño debe preservar la *trazabilidad del evento* sin retener la *materia prima sensible*.

---

## 11.3. Diferencial entre Anonimización y Pseudonimización

La ingeniería debe ser precisa, porque la ley castiga la ambigüedad.

1.  **Pseudonimización (Reversible):** Reemplazar "Juan" por "User_123" manteniendo la tabla de traducción. Sigue siendo dato personal bajo GDPR/Ley 21.719.
2.  **Anonimización (Irreversible):** Destruir matemáticamente la capacidad de reidentificar al sujeto.

> **Carga de la Prueba:** En un litigio, la anonimización no se presume: debe ser demostrable frente a técnicas razonables de reidentificación vigentes al momento del tratamiento. La empresa debe probar mediante peritaje que la re-identificación es inviable con el estado del arte actual.

---

## 11.4. Gestión del Consentimiento como Interruptor

El consentimiento no es un papel; es un **metadato de estado** que controla el flujo.
El sistema debe actuar como una compuerta lógica:

$$Flujo = Dato \times Base\_Legal$$

Si la base legal es el consentimiento y el valor cambia a `FALSE` (revocación), la tubería debe cerrarse automáticamente.

> **Gestión de Latencia:** En sistemas distribuidos, la revocación no es instantánea (caches, réplicas). Toda latencia entre la orden legal y su ejecución técnica final debe ser conocida, documentada y **aprobada explícitamente por el Comité de Datos**. "No sabíamos que estaba en el caché" es negligencia; "El sistema tarda 4 horas en purgar cachés por diseño aprobado" es una declaración de arquitectura defendible.

---

## 11.5. Conclusión: Defensa Estructural

Implementar *Privacy by Design* genera **Defensa Estructural**.
Cuando llega una auditoría, el argumento no es "nos esforzamos mucho", sino "el diseño del sistema impide esa acción".

**A partir de Privacy by Design, la privacidad deja de ser una promesa de marketing y se convierte en una propiedad demostrable del sistema.**

Esto no es solo cumplimiento administrativo; es la preparación de la evidencia técnica que exigirá la fiscalización descrita más adelante en el **Capítulo 14**. No prometemos inmunidad mágica; prometemos debida diligencia codificada.