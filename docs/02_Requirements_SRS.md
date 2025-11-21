# Especificación de Requerimientos de Software (SRS)

**Proyecto:** ZoneDelivery  
**Documento:** Especificación Funcional y No Funcional

## 1. Requerimientos Funcionales (RF)

Los requerimientos se priorizan utilizando la escala MoSCoW (Must have, Should have, Could have, Won't have). Para este MVP, nos enfocamos en los "Must have".

### Módulo 1: Autenticación y Perfil

- **RF-001 (Registro):** El sistema debe permitir el registro de usuarios clasificándolos por rol (Cliente, Repartidor) mediante correo electrónico.
- **RF-002 (Login):** El sistema debe permitir el inicio de sesión validando credenciales y manteniendo la sesión activa (Persistencia).

### Módulo 2: Gestión de Pedidos (Cliente)

- **RF-003 (Catálogo):** El cliente debe poder visualizar una lista de comercios disponibles dentro de su geocerca.
- **RF-004 (Carrito):** El sistema debe permitir agregar ítems, sumar costos y confirmar la intención de pedido.
- **RF-005 (Visualización de PIN):** Una vez el pedido esté en estado "En Camino", el sistema generará y mostrará un PIN aleatorio de 4 dígitos al cliente.
    - *Restricción:* Este PIN NO debe ser visible para el repartidor en su app.

### Módulo 3: Logística y Rastreo (Repartidor)

- **RF-006 (Asignación):** El sistema debe notificar a los repartidores disponibles dentro de un radio X km del comercio.
- **RF-007 (Geolocalización):** El dispositivo del repartidor debe enviar su ubicación (latitud/longitud) en intervalos regulares (ej. cada 10s) cuando tenga un pedido activo.
- **RF-008 (Validación de Entrega):** La interfaz del repartidor debe tener un campo numérico obligatorio para ingresar el PIN proporcionado por el cliente para finalizar la tarea.

### Módulo 4: Lógica de Negocio (Backend)

- **RF-009 (Match de PIN):** El servidor debe comparar el PIN ingresado por el repartidor con el generado en la base de datos.
    - *Si coincide:* Transacción exitosa, pedido cerrado.
    - *No coincide:* Error, pedido permanece abierto.
- **RF-010 (Geofence):** El sistema debe validar las coordenadas del usuario antes de permitir crear un pedido. Si está fuera del polígono, se bloquea la acción.

## 2. Requerimientos No Funcionales (RNF)

### RNF-01: Compatibilidad Técnica
- **Sistema Operativo:** Android 8.0 (Oreo, API Level 26) o superior.
- **Arquitectura:** Cliente-Servidor.

### RNF-02: Rendimiento y Latencia
- **Tiempo de Respuesta GPS:** La actualización de la posición del repartidor en el mapa del cliente no debe tener un retraso mayor a 10 segundos en redes 4G.
- **Tiempo de Carga:** La pantalla inicial debe cargar en menos de 3 segundos.

### RNF-03: Seguridad
- **Datos Sensibles:** Las contraseñas deben almacenarse con Hashing (ej. bcrypt o equivalente de Firebase Auth).
- **Integridad del PIN:** El PIN se genera en el servidor (Backend), nunca en el cliente, para evitar manipulación local.

### RNF-04: Usabilidad
- **Diseño:** Interfaz intuitiva que requiera máximo 3 clics para recomprar un pedido anterior.
- **Feedback:** El sistema siempre debe informar el estado de la petición (Cargando, Éxito, Error).