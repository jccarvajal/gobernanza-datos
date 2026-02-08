# Capítulo 03. Arquitectura Decisional

> *"La estrategia es lo que quieres hacer. La arquitectura es lo que puedes hacer. Si tu plan estratégico requiere una visión 360 del cliente, pero tu base de datos tiene al cliente fragmentado en cinco tablas incomunicadas, tu estrategia no es un plan; es una alucinación."*

## 3.1. Ceguera Ontológica

En filosofía, la ontología estudia "lo que existe". En sistemas, el modelo de datos define la ontología de la organización.
Si una entidad, un concepto o una relación no tiene una representación formal en el esquema (ya sea en una tabla SQL, un documento JSON o un contrato de API), para efectos operativos de la empresa, **ese concepto no existe**.

Imagina un banco cuya estrategia es "Cuidar la salud financiera de la familia".

* Si su sistema *Core* solo tiene la entidad `Cuenta_Corriente` y `Cliente_Individual`, pero no tiene la entidad `Grupo_Familiar`...
* El banco es **ontológicamente ciego** a la familia.
* No puede medirla, no puede bonificarla y no puede protegerla.

La estrategia puede estar escrita en Powerpoint, pero si no baja al esquema de la base de datos (DDL) o a la definición de la interfaz, nunca será ejecutable. El sistema solo puede gestionar lo que puede nombrar.

---

## 3.2. El Determinismo del Esquema (Fricción y Costo)

A menudo se dice que el software es "blando" (*soft*-ware) y adaptable. En la práctica empresarial, la arquitectura de datos es **viscosa**.

Existe una asimetría fundamental de velocidad:

* **La Estrategia es Líquida:** Se puede cambiar en una reunión de directorio un lunes por la mañana.
* **El Esquema es Sólido:** Cambiar la estructura central de un Data Warehouse o un ERP puede tomar meses de ingeniería y migración.

Esta diferencia de velocidad crea el **Determinismo del Esquema**.
Cuando la Estrategia choca contra la Arquitectura, la Arquitectura suele ganar por desgaste. El costo y el tiempo de adaptar los sistemas es tan alto que la organización termina adaptando su estrategia a las limitaciones de sus herramientas, y no al revés.
La gobernanza efectiva consiste en reducir esta fricción, anticipando el modelo de datos que la estrategia futura necesitará, no solo el que necesita hoy.

---

## 3.3. La Ley de Conway y el Organigrama Fosilizado

La Ley de Conway establece que *"las organizaciones diseñan sistemas que son copias de sus estructuras de comunicación"*.
Si tienes equipos separados de Ventas y Marketing, tendrás bases de datos separadas de Ventas y Marketing.

Pero en el mundo de los datos, observamos un efecto de retroalimentación crítica: **El Modelo de Datos fosiliza la estructura organizacional.**
Si tus datos están fragmentados en silos técnicos, tus equipos humanos operarán en silos, aunque el CEO ordene "colaboración".

* Si el dato de "Inventario" está separado del dato de "Ventas", el equipo de Logística y el de Comercial no *pueden* colaborar en tiempo real, porque no ven la misma realidad.

Para cambiar la organización, a menudo es necesario cambiar primero las interfaces de datos (API/Contratos) que conectan a los equipos. Cambiar el flujo de datos obliga a cambiar el flujo de comunicación humana.

---

## 3.4. Arquitectura es Destino (En Decisiones Irreversibles)

No todas las decisiones técnicas importan igual.
Elegir entre la herramienta de BI "A" o "B" es reversible.
Pero las decisiones arquitectónicas estructurales fijan el rango de maniobra posible del negocio por años.

**Ejemplo: Teorema CAP (Consistency, Availability, Partition Tolerance)**

En sistemas distribuidos, debes elegir matemáticamente entre:

1.  **Consistencia Fuerte:** Todos ven el mismo dato al mismo tiempo (ej. Banco).
2.  **Disponibilidad Alta:** El sistema siempre responde, aunque el dato sea viejo (ej. Red Social).

Esta no es una decisión de "ingeniería"; es una decisión de negocio disfrazada.
Si el arquitecto elige "Disponibilidad" para una plataforma de pagos, ha decidido —sin consultar— que es aceptable que el saldo del cliente sea incorrecto temporalmente.
El arquitecto, al definir la infraestructura, está legislando sobre la experiencia del cliente y los riesgos que la empresa puede asumir.

> **Regla de Gobernanza:** Estas decisiones de compromiso (*trade-offs*) deben ser explícitas, documentadas y firmadas por el negocio, nunca implícitas en el código o en la compra de una tecnología "de moda".

---

## 3.5. Conclusión del Bloque 1: El Fin de la Teoría

Hasta aquí hemos hablado de conceptos: el dato como material peligroso (Cap. 1), el sistema de decisión GRC (Cap. 2) y la arquitectura como límite estratégico (Cap. 3).
Este es el fin del **Bloque 1 (Fundamentos)**.

A partir de ahora, dejamos la mesa de diseño y bajamos a la sala de máquinas.
En el **Bloque 2**, abordaremos la **Ingeniería de la Verdad**.

Ya no hablaremos de "qué" hacer, sino de "cómo" sobrevivir operativamente:

* Cómo evitar el secuestro por proveedores (**Cap. 4**).
* Cómo limpiar datos sin detener el negocio (**Cap. 5**).
* Cómo construir una verdad única en un mundo caótico (**Cap. 6**).

La teoría ha terminado. Empieza la construcción.