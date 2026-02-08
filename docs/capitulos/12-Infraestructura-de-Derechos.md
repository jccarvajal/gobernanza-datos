# Capítulo 12. La Infraestructura de Derechos (ARCO)

> *"Los derechos digitales (Acceso, Rectificación, Cancelación, Oposición) no son favores que la empresa concede al cliente. Son instrucciones de comando que el cliente ejecuta sobre la infraestructura de la empresa. Si tu arquitectura no tiene una API para recibir esas instrucciones, tu empresa está operando una monarquía digital en una era democrática."*

## 12.1. Vista 360º Inversa (Derecho de Acceso)

Históricamente, la "Vista 360º" era una herramienta de vigilancia del marketing hacia el cliente.
El Derecho de Acceso invierte el telescopio: es la **Vista 360º del Cliente hacia la Empresa**.

Cuando un usuario solicita "ver sus datos", no basta con exportar los datos maestros (Nombre, RUT). La ley y la doctrina moderna exigen entregar también las **inferencias y decisiones**:

* "¿Me clasificaron como 'Alto Riesgo'?"
* "¿Por qué el algoritmo rechazó mi crédito?"

> **Exigencia de Arquitectura:** El sistema debe ser capaz de reconstruir no solo el dato primario, sino el "gemelo digital" completo del usuario, incluyendo los perfiles derivados y la lógica de las decisiones automatizadas (*Meaningful Information about Logic Involved*). Un CSV con datos crudos ya no es cumplimiento; es ofuscación.
>
> *Límite Legal:* Esta transparencia tiene un techo: no debe revelar el **Secreto Comercial** (el código fuente exacto del algoritmo) ni vulnerar la privacidad de terceros. Se entrega la lógica de la decisión, no la propiedad intelectual del motor.

---

## 12.2. El Artefacto de Borrado (Crypto-shredding)

En entornos modernos de Big Data y Backups inmutables (WORM), ir a buscar y sobreescribir físicamente un registro específico (`DELETE * FROM table`) es técnicamente complejo y a veces imposible sin romper la integridad del backup.

La técnica estándar en estas arquitecturas es el **Crypto-shredding** (Triturado Criptográfico):

1.  Cada dato sensible se encripta con una llave única específica para ese usuario/dato.
2.  Cuando el usuario pide "Olvido", no borramos los petabytes de copias de seguridad.
3.  Borramos la **Llave de Encriptación** del usuario.

Sin la llave, los datos dispersos en los backups se convierten instantáneamente en ruido digital irrecuperable.

> **Residuo Digital:** Los bytes cifrados permanecen, pero son matemáticamente inaccesibles. Estos artefactos inertes deben ser tratados formalmente como un **Riesgo Residual Documentado**, aceptado por la organización como la mejor aproximación técnica posible al borrado físico en sistemas distribuidos.

---

## 12.3. Portabilidad: La API es el Derecho

La Portabilidad (llevarse los datos a otro proveedor) suele ser saboteada por las empresas mediante "fricción técnica": entregar PDFs escaneados o formatos propietarios inútiles.

La Gobernanza de Datos define que la Portabilidad debe ser **Mecánica y Estructurada** (JSON/XML vía API).
Sin embargo, esto crea un vector de ataque: si la API de portabilidad es insegura, se convierte en la herramienta perfecta para la exfiltración masiva de datos (*Scraping*).

> **Balance de Seguridad:** La seguridad de la plataforma prevalece sobre la velocidad de la entrega. Es aceptable introducir **fricción de seguridad intencional** (MFA, validación de identidad diferida, cuarentena de 24h) antes de liberar el paquete de portabilidad. El derecho es a recibir los datos, no a recibirlos en tiempo real sin verificación.

---

## 12.4. Notificación de Brechas: La Regla de las 72 Horas

La normativa internacional (GDPR) y local tiende a exigir la notificación de incidentes de seguridad en un plazo de 72 horas desde la "constatación".

El pánico suele llevar a dos errores:

1.  **Notificar Ruido:** Reportar cada escaneo de puertos (fatiga de alerta).
2.  **Ocultar por Vergüenza:** Esperar a tener "certeza total" (que llega semanas tarde).

**La Doctrina de la Mejor Evidencia:**

El objetivo en las primeras 72 horas no es la certeza forense total (imposible), sino la **mejor evidencia disponible**.
La arquitectura debe permitir al CISO y al DPO responder tres preguntas en t < 72h mediante instrumentación previa:

* ¿Qué datos *podrían* haber sido afectados? (Alcance).
* ¿Estaban encriptados? (Impacto).
* ¿Hay evidencia de exfiltración? (Tráfico de salida).

La decisión de notificar no es técnica ni legal en aislamiento; es una decisión de crisis que requiere datos técnicos rápidos para evaluar el riesgo reputacional y legal.

---

## 12.5. Conclusión: El Usuario como Operador

En la **Gobernanza de Datos Defensiva**, cambiamos el modelo mental del usuario.
Ya no es un "sujeto pasivo" que firmó un término y condición hace 5 años.
Metafóricamente, **cada ciudadano es el SysAdmin de su propia fila** en nuestra base de datos.

Esto no significa que tenga privilegios de administrador de infraestructura (*root*). Significa que tiene la capacidad de ejecutar **derechos predefinidos** (Ver, Corregir, Borrar, Mover) que el sistema debe obedecer automáticamente.
Si el usuario presiona el botón "Borrar", y la empresa responde "mande un fax y espere 30 días", el sistema no está roto; el sistema es ilegal por diseño.