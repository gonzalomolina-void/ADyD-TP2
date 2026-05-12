# Consultas para la Cátedra - TP2 (ADyD)

**Estudiante:** Alumno de la TUDW (FI - UNCOMA)
**Dominio Elegido:** 7 - Alquiler de vehículos (Vehitinder)

---

**Asunto: Consulta sobre el modelado conceptual del Dominio 7 (Vehitinder) - TP2**

Hola profes, ¿cómo va? Estuve analizando el escenario de **Vehitinder** y, aunque vengo del palo del desarrollo y por ahí uno tiende a pensar directo en las tablas de la DB, estoy tratando de abstraerme para el **Diagrama de Clases Conceptual** como pide la consigna. Me surgieron tres dudas puntuales que no quería dejar pasar para no arrastrar errores de base:

1.  **Sobre la jerarquía de Usuarios y Roles:** Estuve viendo que el enunciado habla de "Propietarios" e "Inquilinos". En mi primer borrador los puse como subclases de `Usuario`. Pero después me quedé pensando en lo que dice **Fowler** sobre no confundir *subtipos* con *roles*. Si un usuario hoy alquila un auto (Inquilino) pero mañana publica el suyo (Propietario), ¿sería correcto mantener la herencia o ustedes prefieren que lo modelemos con una asociación de roles para que el modelo sea más flexible? Me interesa saber qué criterio de "limpieza" arquitectónica prioriza la cátedra en estos casos de solapamiento.

2.  **Granularidad de la clase `Pago`:** En el material de la Unidad 4 citan a **Sommerville** sobre la identificación de objetos del sistema. Con el tema de los pagos, ¿es mejor tratar al `Pago` como una entidad independiente con su propio ciclo de vida (procesando, aprobado, etc.) o, al ser un modelo conceptual, lo deberíamos ver simplemente como un atributo de estado de la `Reserva`? Mi duda es si darle "entidad propia" no es estar yéndome mucho a la implementación, o si para ustedes es clave para reflejar la lógica del negocio.

3.  **Alcance del Diagrama de Actividades:** Para el proceso de "Calificación mutua", ¿el diagrama de actividades debería centrarse solo en el flujo lógico del sistema (el algoritmo que calcula el promedio) o es preferible que mostremos también las interacciones humanas y las decisiones del usuario, tipo un modelado de proceso de negocio (BPM)? Me da miedo que quede muy simple si solo pongo los pasos del software y quería saber hasta qué nivel de detalle de "negocio" esperan que lleguemos.

Desde ya gracias, la verdad que el tema de modelar antes de programar te cambia la perspectiva de cómo se estructuran las responsabilidades, ¡está muy bueno!
