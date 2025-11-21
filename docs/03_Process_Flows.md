# Diagramas de Flujo y Procesos

Este documento define la lógica visual del sistema. Se utiliza sintaxis Mermaid.js compatible con la mayoría de visores de Markdown modernos (GitLab, GitHub, Obsidian).

## 1. Ciclo de Vida del Pedido (Happy Path)

Estados por los que pasa un pedido desde la intención de compra hasta la entrega.

```mermaid
stateDiagram-v2
    [*] --> Creado: Cliente envía pedido
    Creado --> Aceptado: Comercio confirma disponibilidad
    Aceptado --> Preparacion: Cocinando / Empacando
    Preparacion --> Listo: Comercio marca listo para recoger
    Listo --> EnCamino: Repartidor recoge paquete
    note right of EnCamino
      El sistema activa el rastreo GPS
      y muestra el PIN al Cliente
    end note
    EnCamino --> Entregado: Validación PIN Correcta
    Entregado --> [*]
```

## 2. Flujo Crítico: Seguridad de Entrega (PIN)

Detalle de la interacción Cliente-Repartidor-Servidor para cerrar la transacción.

```mermaid
sequenceDiagram
    participant C as Cliente (App)
    participant S as Servidor (Backend)
    participant R as Repartidor (App)

    Note over S: Cambio de estado a "En Camino"
    S->>S: Genera PIN seguro (ej. 9921)
    S->>C: Push Notification: "Tu código es 9921"
    Note over C: Cliente ve pantalla de rastreo con el PIN
    
    R->>R: Llega al domicilio
    R->>C: Entrega pedido físico
    C->>R: Dice verbalmente "9921"
    
    R->>S: Envía input "9921" a API
    
    alt PIN Correcto
        S->>S: DB: Update status = DELIVERED
        S-->>R: Respuesta 200 OK (Pantalla Éxito)
        S-->>C: Push: "Pedido Entregado"
    else PIN Incorrecto
        S-->>R: Respuesta 400 Error
        Note over R: App muestra "Código incorrecto"
        R->>C: Solicita código nuevamente
    end
```

## 3. Flujo de Validación Geográfica (Geofencing)

Lógica para determinar si se puede prestar el servicio.

```mermaid
flowchart TD
    A[Inicio App] --> B{"¿Permiso GPS?"}
    B -->|No| C[Solicitar Permisos Android]
    B -->|Sí| D[Obtener Lat/Long actual]
    D --> E{"¿Está dentro del Polígono?"}
    E -->|No| F["Mostrar Pantalla 'Fuera de Zona'"]
    F --> F1[Opción: Notificarme cuando lleguen]
    E -->|Sí| G[Cargar Home con Comercios]
```
