# Análisis del Dominio 7: Alquiler de vehículos (Vehitinder)

En base a la descripción del "Dominio 7", se ha realizado el siguiente análisis para construir el diagrama conceptual de clases.

## 1. Identificación de Clases, Atributos y Métodos

Se han identificado las siguientes clases principales a partir del texto:

### `Usuario` (Clase Abstracta / Base)
Representa a cualquier persona registrada en el ecosistema.
*   **Atributos:**
    *   `nombre`: String
    *   `email`: String
    *   `contraseña`: String
*   **Métodos:**
    *   `iniciarSesion()`
    *   `enviarMensaje(receptor, texto)`
    *   `dejarCalificacion(transaccion, evaluado, puntaje, reseña)`

### `Propietario` (Hereda de `Usuario`)
Persona que ofrece sus vehículos para alquiler.
*   **Atributos:**
    *   `condicionesAlquiler`: String
    *   `preferenciasPersonales`: String
    *   `reputacion`: Float (calculado en base a calificaciones)
*   **Métodos:**
    *   `registrarVehiculo()`
    *   `evaluarSolicitud(solicitud)`
    *   `aprobarSolicitud(solicitud)`
    *   `rechazarSolicitud(solicitud)`

### `Inquilino` (Hereda de `Usuario`)
Persona que busca y solicita vehículos para alquilar.
*   **Atributos:**
    *   `historialConduccion`: String
    *   `preferenciasAlquiler`: String
    *   `reputacion`: Float (calculado en base a calificaciones)
*   **Métodos:**
    *   `buscarVehiculos(criterios)`
    *   `crearSolicitud(vehiculo, fechas, proposito)`
    *   `realizarPago(reserva)`

### `Vehiculo`
El automóvil ofrecido para alquiler.
*   **Atributos:**
    *   `patente`: String
    *   `fotos`: List<Image>
    *   `descripcion`: String
    *   `tarifaDiaria`: Float
    *   `disponibilidad`: Boolean (o Estado: Disponible, Reservado)
*   **Métodos:**
    *   `actualizarDisponibilidad()`
    *   `bloquearFechas(fechaInicio, fechaFin)`

### `SolicitudAlquiler`
El formulario que completa el inquilino para pedir un vehículo.
*   **Atributos:**
    *   `fechaInicio`: Date
    *   `fechaFin`: Date
    *   `proposito`: String
    *   `requisitosEspeciales`: String
    *   `estado`: Enum (Pendiente, Aprobada, Rechazada)
*   **Métodos:**
    *   `actualizarEstado(nuevoEstado)`

### `Reserva`
Se genera automáticamente cuando el Propietario aprueba una Solicitud.
*   **Atributos:**
    *   `fechaConfirmacion`: Date
    *   `estado`: Enum (PendientePago, Pagada, Finalizada)
*   **Métodos:**
    *   `procesarCobro()`

### `Pago`
Representa la transacción financiera.
*   **Atributos:**
    *   `monto`: Float
    *   `fechaPago`: Date
    *   `plataforma`: String (ej. MercadoPago)
    *   `estado`: Enum (Procesando, Exitoso, Fallido)
*   **Métodos:**
    *   `verificarPago()`

### `Mensaje`
Comunicación interna entre usuarios.
*   **Atributos:**
    *   `contenido`: String
    *   `fechaHora`: DateTime
*   **Métodos:**
    *   `leer()`

### `Calificacion`
Reseña dejada después de una transacción.
*   **Atributos:**
    *   `puntaje`: Integer
    *   `reseña`: String
    *   `fecha`: Date

---

## 2. Relaciones y Cardinalidad

*   **Generalización (Herencia):**
    *   `Propietario` *es un* `Usuario`.
    *   `Inquilino` *es un* `Usuario`.

*   **Asociaciones:**
    *   **Propietario - Vehículo:** Un Propietario registra/posee uno o muchos Vehículos.
        *   `Propietario (1) ----- (1..*) Vehiculo`
    *   **Inquilino - SolicitudAlquiler:** Un Inquilino crea cero o muchas Solicitudes.
        *   `Inquilino (1) ----- (0..*) SolicitudAlquiler`
    *   **Vehículo - SolicitudAlquiler:** Un Vehículo puede recibir cero o muchas Solicitudes.
        *   `Vehiculo (1) ----- (0..*) SolicitudAlquiler`
    *   **Propietario - SolicitudAlquiler:** Un Propietario evalúa cero o muchas Solicitudes (asociadas a sus vehículos).
        *   `Propietario (1) ----- (0..*) SolicitudAlquiler`
    *   **SolicitudAlquiler - Reserva:** Una Solicitud Aprobada genera exactamente una Reserva.
        *   `SolicitudAlquiler (1) ----- (0..1) Reserva`
    *   **Reserva - Vehículo:** Una reserva bloquea las fechas de un vehículo específico.
        *   `Reserva (0..*) ----- (1) Vehiculo`
    *   **Reserva - Pago:** Una Reserva requiere un Pago.
        *   `Reserva (1) ----- (1) Pago`
    *   **Usuario - Mensaje (Emisor):** Un Usuario envía cero o muchos Mensajes.
        *   `Usuario (1) ----- (0..*) Mensaje` (Rol: Emisor)
    *   **Usuario - Mensaje (Receptor):** Un Usuario recibe cero o muchos Mensajes.
        *   `Usuario (1) ----- (0..*) Mensaje` (Rol: Receptor)
    *   **Reserva - Calificacion:** Una transacción (Reserva completada) puede tener hasta dos Calificaciones (una del Propietario, una del Inquilino).
        *   `Reserva (1) ----- (0..2) Calificacion`
    *   **Usuario - Calificacion (Autor):** Un Usuario escribe Calificaciones.
        *   `Usuario (1) ----- (0..*) Calificacion` (Rol: Autor)
    *   **Usuario - Calificacion (Evaluado):** Un Usuario recibe Calificaciones.
        *   `Usuario (1) ----- (0..*) Calificacion` (Rol: Evaluado)