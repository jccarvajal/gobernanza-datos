# Bibliografía Fundamental
**(El Arsenal de la Ingeniería de la Evidencia)**

### Introducción: Las Fuentes de la Defensa
Este anexo no busca la erudición académica, sino la supervivencia operativa. Hemos seleccionado los textos que fundamentan la tesis del **Dato como Uranio** y la **Arquitectura Defendible**. Estas obras proveen la base matemática, legal y arquitectónica para resistir la fiscalización de la Ley 21.719 y gestionar el riesgo cognitivo de la IA.

### Prólogo: La Física del Dato y la Verdad

* **Kleppmann, M. (2017).** "Designing Data-Intensive Applications". O'Reilly Media. [[Ver Libro]](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321)
    * **Por qué leerlo:** La Biblia técnica de este libro. Fundamenta por qué la "verdad" en sistemas distribuidos es un problema de consenso y consistencia, no de almacenamiento. Base para los Capítulos 05 (ETL-V) y 06 (SSOT).
* **Zuboff, S. (2019).** "The Age of Surveillance Capitalism". PublicAffairs. [[Ver Libro]](https://www.amazon.com/Age-Surveillance-Capitalism-Future-Frontier/dp/1610395697)
    * **Por qué leerlo:** El marco teórico para entender el "Dato como Uranio". Explica la economía extractiva que generó la crisis de privacidad actual y justifica la necesidad de defensas como el "Airlock" y la Soberanía.
* **Véliz, C. (2020).** "Privacy is Power". Melville House. [[Ver Libro]](https://www.amazon.com/Privacy-Power-Why-Should-Take/dp/1612198583)
    * **Por qué leerlo:** Lectura obligatoria para el Prólogo y el Bloque 1. Desmonta el mito de que "si no haces nada malo, no tienes nada que temer" y establece el riesgo tóxico de acumular datos personales.

### Bloque 1: Estrategia y Poder (El Dato-Uranio)

* **Schneier, B. (2015).** "Data and Goliath". W. W. Norton & Company. [[Ver Libro]](https://www.amazon.com/Data-Goliath-Battles-Collect-Control/dp/0393244814)
    * **Por qué leerlo:** Fundamento de seguridad para el Capítulo 01. Explica por qué la recolección masiva es un pasivo de seguridad inmanejable y por qué la única estrategia segura es la minimización.
* **Taleb, N. N. (2018).** "Skin in the Game". Random House. [[Ver Libro]](https://www.amazon.com/Skin-Game-Hidden-Asymmetries-Daily/dp/042528462X)
    * **Por qué leerlo:** Base ética del Capítulo 02 (GRC). Argumenta que los arquitectos de sistemas (CDO) deben pagar un precio personal si sus sistemas fallan o filtran datos (Simetría de Riesgo).

### Bloque 2: Ingeniería de la Verdad (Infraestructura)

* **Reis, J., & Housley, M. (2022).** "Fundamentals of Data Engineering". O'Reilly Media. [[Ver Libro]](https://www.amazon.com/Fundamentals-Data-Engineering-Robust-Systems/dp/1098108302)
    * **Por qué leerlo:** El manual de campo para el Capítulo 05. Define la ingeniería de datos moderna, alejándose del "Big Data" caótico hacia ciclos de vida gestionados, observabilidad y FinOps.
* **Beyer, B., et al. (2016).** "Site Reliability Engineering (SRE)". O'Reilly Media. [[Ver Libro]](https://www.amazon.com/Site-Reliability-Engineering-Production-Systems/dp/149192912X)
    * **Por qué leerlo:** La doctrina de Google sobre cómo operar sistemas críticos. Base para aplicar conceptos de "Presupuesto de Error" a la calidad del dato y la disponibilidad de la plataforma de verdad.

### Bloque 3: Automatización e Inteligencia (IA y RAG)

* **Russell, S. (2019).** "Human Compatible: Artificial Intelligence and the Problem of Control". Viking. [[Ver Libro]](https://www.amazon.com/Human-Compatible-Artificial-Intelligence-Problem/dp/0525558616)
    * **Por qué leerlo:** Fundamento para el Capítulo 07 (La Ilusión de No Tener IA) y Capítulo 10 (Sanitización). Plantea el "problema de alineación", clave para entender por qué la IA no debe operar sin supervisión estructural.
* **Huyen, C. (2022).** "Designing Machine Learning Systems". O'Reilly Media. [[Ver Libro]](https://www.amazon.com/Designing-Machine-Learning-Systems-Production-Ready/dp/1098107969)
    * **Por qué leerlo:** Guía técnica para los Capítulos 08 y 09. Explica cómo desplegar modelos que no degraden en producción, gestión de *Data Drift* y la necesidad de infraestructura de evaluación continua (RAG).

### Bloque 4: Arquitectura Legal (Privacy by Design)

* **Cavoukian, A. (2009).** "Privacy by Design: The 7 Foundational Principles". [[Paper Oficial]](https://www.ipc.on.ca/wp-content/uploads/2018/01/pbd-primer.pdf)
    * **Por qué leerlo:** El código fuente de la Ley 21.719 y del Capítulo 11. No es un libro, es el manifiesto que debe ser traducido a reglas de ingeniería en el pipeline de CI/CD.
* **O'Neil, C. (2016).** "Weapons of Math Destruction". Crown. [[Ver Libro]](https://www.amazon.com/Weapons-Math-Destruction-Increases-Inequality/dp/0553418815)
    * **Por qué leerlo:** Vital para el Capítulo 12 (Infraestructura de Derechos) y la defensa ante sesgos. Explica cómo los algoritmos opacos generan responsabilidad civil y administrativa.

### Bloque 5: Escalabilidad y Marco de Ejecución

* **Dehghani, Z. (2022).** "Data Mesh: Delivering Data-Driven Value at Scale". O'Reilly Media. [[Ver Libro]](https://www.amazon.com/Data-Mesh-Delivering-Driven-Value/dp/1492092398)
    * **Por qué leerlo:** La Biblia del Capítulo 13. Propone el cambio de paradigma desde el "Lago de Datos" centralizado hacia la federación de dominios con gobierno computacional federado.
* **Laney, D. (2017).** "Infonomics: How to Monetize, Manage, and Measure Information". Bibliomotion. [[Ver Libro]](https://www.amazon.com/Infonomics-Monetize-Manage-Measure-Information/dp/1138090387)
    * **Por qué leerlo:** Lectura crítica para el Capítulo 14 (DAMA/MGDE). Enseña a tratar la información como un activo contable, permitiendo calcular su "Riesgo de Información" (Liability) de forma monetaria.

### Bloque 6: Defensa y Liderazgo (El Examen Final)

* **Leveson, N. (2011).** "Engineering a Safer World: Systems Thinking Applied to Safety". MIT Press. [[Ver Libro]](https://mitpress.mit.edu/9780262533690/engineering-a-safer-world/)
    * **Por qué leerlo:** La referencia absoluta para el Capítulo 15 (Fiscalización Técnica). Establece que la seguridad no es una propiedad de los componentes, sino una propiedad emergente del sistema de control.
* **Horowitz, B. (2014).** "The Hard Thing About Hard Things". Harper Business. [[Ver Libro]](https://www.amazon.com/Hard-Thing-About-Things-Building/dp/0062273205)
    * **Por qué leerlo:** Esencial para el Capítulo 16 (Rol del CDO). Define la mentalidad de "Tiempo de Guerra" (*Wartime CEO*) necesaria para liderar bajo crisis regulatoria y amenaza existencial.