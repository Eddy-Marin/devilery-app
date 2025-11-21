# Acta de Constitución del Proyecto (Project Charter)

**Nombre del Proyecto:** ZoneDelivery (Nombre Clave)  
**Versión:** 1.0  
**Fecha:** 20 Noviembre 2025  
**Sponsor:** Eduardo Marin  
 

## 1. Propósito y Justificación del Proyecto (Business Case)

Actualmente, existen zonas geográficas desatendidas por las grandes plataformas de delivery (UberEats, Rappi, DiDi, etc.). Los residentes y comercios de estas áreas tienen la necesidad latente de realizar pedidos a domicilio de forma eficiente y segura, pero carecen de la infraestructura tecnológica.

Este proyecto busca desarrollar una solución tecnológica (App Android) que cubra este vacío de mercado (Blue Ocean Strategy), ofreciendo tarifas competitivas y un enfoque en la seguridad mediante validación de entrega por PIN.

## 2. Objetivos del Proyecto (SMART)

- **Desarrollo:** Completar el MVP de la aplicación Android (Cliente, Repartidor y Lógica de Negocio) listo para despliegue.
- **Alcance:** Implementar el sistema de "Token de Entrega" (PIN) con una efectividad del 100% para evitar fraudes o disputas.
- **Cobertura:** Implementar sistema de Geofencing para delimitar la operación exclusivamente a la zona objetivo.

## 3. Alcance del Proyecto (Scope)

### In Scope (Se incluye en el MVP)
- **App Android Nativa:** Único sistema operativo para lanzamiento (Android 8.0+).
- **Roles de Usuario:** Cliente, Repartidor, Comercio (Gestión simplificada).
- **Geofencing:** Restricción de pedidos solo dentro de las coordenadas permitidas.
- **Ciclo del Pedido:** Selección, Carrito, Confirmación, Rastreo, Entrega.
- **Seguridad:** Validación de entrega mediante PIN de 4 dígitos (Token).
- **Rastreo:** Visualización en tiempo real de la ubicación del repartidor.

### Out of Scope (No se incluye en Fase 1)
- App para iOS (iPhone).
- Pagos con Tarjeta/Pasarela Bancaria (Fase 1 será Pago contra Entrega o integración manual).
- Chat en tiempo real (se usarán llamadas telefónicas directas mediante intent de Android).
- Algoritmos complejos de optimización de rutas (asignación por radio simple).

## 4. Interesados (Stakeholders)

| Rol | Descripción | Interés Principal |
| :--- | :--- | :--- |
| **Product Owner** | Dueño del proyecto | Retorno de inversión, adopción del mercado. |
| **Project Manager** | Líder Técnico | Cumplimiento de cronograma y calidad de código. |
| **Cliente Final** | Usuario que pide | Facilidad de uso, seguridad, recibir su comida caliente. |
| **Repartidor (Rider)** | Socio logístico | Claridad en la ubicación, app ligera, pago justo. |
| **Comercio** | Restaurante/Tienda | Aumentar ventas sin comisiones abusivas. |

## 5. Riesgos Iniciales Identificados

- **Conectividad:** La zona objetivo puede tener señal intermitente (3G/H+).
    - *Mitigación:* Arquitectura "Optimistic UI" y manejo de errores offline.
- **Precisión GPS:** Errores en la ubicación de direcciones no estandarizadas en mapas.
    - *Mitigación:* Permitir ajuste manual del "pin" en el mapa por parte del usuario.