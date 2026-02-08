# Capítulo 10. Sanitización Cognitiva

> *"No existe el 'algoritmo racista' o la 'IA malvada'. Solo existen datasets de entrenamiento que reflejan las fallas históricas de la sociedad, y gobernanzas que no supieron filtrarlas. Si alimentas a la máquina con los prejuicios de tus decisiones pasadas, no estás innovando; estás automatizando tu propia obsolescencia moral y legal."*

## 10.1. El Sesgo como Falla Técnica (y de Omisión)

En la **Gobernanza de Datos Defensiva**, el sesgo (*Bias*) no es un problema de opinión o ideología; es un problema de **Calidad de Datos**. Si tu modelo de crédito recomienda rechazar a mujeres solventes porque entrenaste con datos históricos de una época machista, tu modelo tiene un defecto de ingeniería medible.

Pero hay un riesgo mayor: **El Sesgo por Omisión**.
A menudo, los datos históricos son correctos en lo que muestran, pero ciegos en lo que ignoran (ej. poblaciones rurales no digitalizadas).

> **Advertencia de Alcance:** El sesgo por omisión **no es totalmente eliminable** mediante limpieza de datos, porque el dato necesario nunca existió. La Gobernanza no promete un modelo "neutro" (imposible), sino un modelo donde las zonas ciegas están identificadas, documentadas y gestionadas como riesgo residual.
>
> *Nota Legal:* Documentar estas zonas ciegas no elimina la responsabilidad ante un daño, pero acredita la **debida diligencia** y la buena fe procesal de la organización, diferenciando el error técnico de la negligencia dolosa.

---

## 10.2. Los Datos Radioactivos: PII y PHI

Más allá del sesgo, existe una categoría de datos que actúa como veneno estructural: la Información Personal Identificable (PII) y la Información de Salud (PHI).

Aquí debemos hacer una distinción arquitectónica crítica entre **Entrenamiento** y **Recuperación**:

1.  **En Entrenamiento (Fine-Tuning):** Si incluyes PII en el corpus de entrenamiento, el dato se disuelve en los pesos matemáticos de la red neuronal.
    * **Estatus:** **Irreversible.** No puedes hacer un `DELETE FROM Model WHERE rut='123'`. El modelo se convierte legalmente en "fruto del árbol envenenado" y, en muchos casos, la única remediación legal posible es la destrucción total del modelo (pérdida de inversión).
2.  **En Recuperación (RAG):** Si el PII entra como contexto en una consulta puntual.
    * **Estatus:** **Reversible técnicamente, pero crítico operativamente.** Puedes borrar el log y el vector, pero si la IA ya entregó el dato sensible al usuario, el incidente de privacidad ya se consumó y debe reportarse.

---

## 10.3. Ingeniería de Equidad (Fairness Engineering)

¿Cómo definimos matemáticamente que una decisión es "justa"?
La Gobernanza debe definir las métricas de equidad (ej. Paridad Estadística, Igualdad de Oportunidades) antes de escribir una sola línea de código.

El rol del GRC no es "definir la justicia universal", sino establecer los **Umbrales de Tolerancia Regulatoria**.

* Si optimizas para "Paridad Demográfica", necesariamente pierdes precisión predictiva.
* Si optimizas para "Precisión Pura", puedes amplificar la discriminación histórica.

> **Decisión de Directorio:** La elección de la métrica de equidad determina qué tipo de riesgo legal la organización está dispuesta a asumir. No es una decisión técnica para el Data Scientist; es la configuración del **Apetito de Riesgo** corporativo. Esta decisión debe quedar registrada en un acta o política formal, no en un comentario de código.

---

## 10.4. La Cámara de Descontaminación (The Airlock)

Para operativizar la sanitización, introducimos un patrón arquitectónico obligatorio entre el "Lago de Datos" y la "Plataforma de IA": **The Airlock** (La Esclusa).

Es un servicio intermedio donde el dato es sometido a limpieza automatizada y obligatoria:

1.  **Detección de PII:** Escáneres (ej. Presidio, Macie) que bloquean o enmascaran RUTs, emails y nombres.
2.  **Filtrado de Toxicidad:** Eliminación de lenguaje peligroso o discriminatorio.

> **Cadena de Custodia:** La esclusa no es una "opción" de arquitectura; es un control de plataforma. Saltarse el Airlock no garantiza que el modelo falle, pero **rompe la cadena de custodia**. En caso de litigio, un modelo alimentado con datos que no pasaron por la esclusa carece de la evidencia de debida diligencia necesaria para una defensa robusta. La esclusa es el seguro de responsabilidad civil del algoritmo.

---

## 10.5. Conclusión: El Espejo Limpio

La Inteligencia Artificial es un espejo de alta definición. Si te paras frente a él con la cara sucia, el espejo reflejará la suciedad con fidelidad implacable.

La función de este capítulo no ha sido prometer una IA perfecta, sino una IA **auditable y defendible**.

* En el Capítulo 9, controlamos la memoria (Vectores).
* En el Capítulo 10, controlamos la toxicidad (Sanitización).

La IA industrializa el sesgo y lo hace visible. Esto no es una condena; es una oportunidad. Por primera vez, tenemos los logs para medir, corregir y gobernar nuestros propios prejuicios corporativos, transformando una debilidad oculta en un riesgo gestionado.

Ahora que hemos limpiado el dato y la cognición, debemos enfrentar la estructura más rígida de todas: la Ley.
En el **Bloque 4 (Arquitectura Legal)**, traduciremos los códigos legales en código de software, comenzando con el **Capítulo 11: Privacy by Design**.