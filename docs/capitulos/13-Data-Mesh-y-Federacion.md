# Capítulo 13. La Federación de Datos (Data Mesh)

> *"El intento de centralizar todos los datos de una empresa moderna en un solo equipo de 'Ingenieros de Datos' es una batalla perdida contra la física. El cuello de botella no es la tecnología; es el conocimiento de dominio. No puedes pedirle a un ingeniero que entienda profundamente la contabilidad de coberturas, la logística de última milla y la segmentación de marketing al mismo tiempo. O distribuimos la responsabilidad, o colapsamos el centro."*

## 13.1. La Muerte del Lago Central (y del Equipo Omnisciente)

El modelo tradicional de *Data Lake* Centralizado se basaba en una premisa arrogante: "Tráiganme todos sus datos, y mi equipo central los limpiará y entenderá".
Esto falló porque separó a **los que saben qué significan los datos** (Negocio/Dominios) de **los que tocan los datos** (Ingenieros Centrales).

El resultado es el "Teléfono Descompuesto":

1.  Finanzas envía datos complejos.
2.  Ingeniería Central (que no sabe de finanzas) los "limpia" mal o aplica reglas genéricas.
3.  El reporte final es técnicamente correcto (compila) pero semánticamente inútil o peligroso.

En la **Gobernanza de Datos Defensiva**, declaramos la quiebra del modelo centralizado para la capa de consumo semántico. Pasamos de un Monolito a una **Federación**.

---

## 13.2. Auftragstaktik: Misión, no Microgestión

Adoptamos el principio militar prusiano de *Auftragstaktik* (Mando por Misión).

* **Modelo Antiguo (Microgestión):** El Centro dice "Mueve la columna A a la columna B".
* **Modelo Data Mesh (Misión):** El Centro dice "Necesito saber la rentabilidad por cliente con esta definición estándar. Cómo lo calcules en tu sistema es tu problema, siempre que cumplas el contrato de interfaz y los estándares de seguridad".

**El Cambio de Poder:**
El "Data Owner" de un dominio (ej. Gerente de Logística) deja de ser un usuario pasivo que pide reportes a TI. Se convierte en un **Productor de Productos de Datos**.

* Tiene presupuesto autónomo.
* Tiene ingenieros embebidos en su equipo.
* **Tiene la responsabilidad funcional por la calidad de lo que publica.**

> **Advertencia de Responsabilidad:** La federación no es "hagan lo que quieran". Es "hagan lo necesario, pero respondan por ello". Si el dato de Logística rompe el reporte del CEO, la culpa ya no es de TI Central; es del Gerente de Logística.
> *Nota:* Hablamos de **responsabilidad institucional delegada** (impacto en evaluación de desempeño, bono, KPIs), no de responsabilidad penal individual, salvo casos de dolo o negligencia grave manifiesta.

---

## 13.3. Gobernanza Federada: La Constitución

Si cada dominio hace lo que quiere, no tenemos una empresa; tenemos un archipiélago de silos incompatibles.
Para evitar la anarquía, la Gobernanza se divide en dos capas estrictas:

1.  **Lo Federal (Centralizado e Innegociable):**
    * Estándares de Seguridad e Identidad (IAM).
    * Definiciones de "Hechos Constitucionales" (Qué es un Cliente, Qué es un Dólar, Qué es una Venta).
    * Políticas de Privacidad, Retención y Borrado (GDPR/Ley 21.719).
    * La Infraestructura de la Verdad (Plataforma Técnica Común).

2.  **Lo Local (Descentralizado y Autónomo):**
    * Cómo modelar los procesos internos del dominio.
    * Qué herramientas de análisis específico usar (dentro del catálogo aprobado).
    * La frecuencia de actualización (siempre que cumpla el SLA del contrato).

> **Principio de Soberanía:** El Centro gobierna los estándares y la plataforma (el "cómo" se conecta y protege). Los Dominios gobiernan el contenido y la lógica de negocio (el "qué" significa).

---

## 13.4. Polimorfismo y la SSOT (Resolviendo la Tensión)

En el Capítulo 6 establecimos la **Fuente Única de Verdad (SSOT)**. ¿Cómo convive esto con la Federación?
Mediante el **Polimorfismo Controlado**.

* **Nivel Constitucional (SSOT Global):** Existe una sola definición de "Cliente" (ID, Nombre Legal, Estado Tributario). Esto es central y rígido. Nadie puede inventar un cliente nuevo ni alterar su ID.
* **Nivel de Dominio (Contexto):**
    * Para Logística, el Cliente es una "Dirección de Entrega y Horario".
    * Para Marketing, el Cliente es un "Perfil de Comportamiento y Preferencias".
    * Para Cobranza, el Cliente es un "Score de Riesgo y Deuda".

La Gobernanza permite estas múltiples "vistas" (polimorfismo), siempre que todas apunten al mismo **ID Maestro Constitucional**.
La SSOT no significa "una sola tabla gigante con 500 columnas"; significa "una sola identidad referencial" a través de múltiples contextos federados.

---

## 13.5. Conclusión: Escalar la Verdad

Data Mesh no es una excusa para que TI se lave las manos. Es una estrategia de madurez organizacional.
Solo funciona si los Dominios aceptan que **los datos son un producto**, no un subproducto exhausto de sus operaciones diarias.

Un Data Mesh bien gobernado permite a la empresa crecer exponencialmente sin que el equipo de datos central se convierta en el cuello de botella.
Pero cuidado: la federación de datos sin estándares de ejecución es anarquía. Para que el Data Mesh sea legalmente defendible y no se convierta en un pantano distribuido, debe operar sobre el riel estricto que definiremos a continuación en el **Capítulo 14 (Gobernanza Ejecutable)**.