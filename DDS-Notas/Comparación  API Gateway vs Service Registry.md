
| **Criterio**                | **API Gateway**                                                                                              | **Service Registry**                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Propósito principal**     | Actuar como punto único de entrada para gestionar solicitudes de clientes, con funcionalidades avanzadas.    | Registrar y localizar dinámicamente instancias de servicios para comunicación directa entre ellos.           |
| **Nivel de abstracción**    | Alto: opera en la capa de aplicación (capa 7, HTTP/HTTPS).                                                   | Medio: facilita descubrimiento de servicios, operando en capas de infraestructura.                           |
| **Funciones principales**   | - Autenticación/autorización.  <br>- Enrutamiento avanzado.  <br>- Transformación de solicitudes/respuestas. | - Registrar y desregistrar servicios dinámicamente.  <br>- Resolver ubicaciones de servicios en tiempo real. |
| **Componente centralizado** | Sí, gestiona todo el tráfico de entrada a los servicios.                                                     | No, distribuye datos de ubicación y se integra con balanceadores o aplicaciones.                             |
| **Soporte para escalado**   | Puede gestionar múltiples servicios pero introduce overhead adicional.                                       | Es crucial para escalar servicios dinámicos en arquitecturas de microservicios.                              |
| **Complejidad**             | Más alto, requiere configurar políticas, autenticación, y enrutamiento.                                      | Relativamente bajo, pero requiere integración con balanceadores de carga y clientes.                         |
| **Protocolo soportado**     | Generalmente HTTP/HTTPS.                                                                                     | Puede operar con múltiples protocolos (HTTP, TCP, gRPC, etc.).                                               |
| **Casos ideales**           | Cuando se necesita gestionar APIs públicas o exponer servicios a clientes externos.                          | Para descubrimiento de servicios en arquitecturas internas con escalado dinámico.                            |
| **Ejemplos comunes**        | AWS API Gateway, Kong, Apigee.                                                                               | Eureka, Consul, Zookeeper.                                                                                   |

### **Resumen**

- **API Gateway**: Se usa como punto de entrada único para gestionar y exponer APIs, ideal para clientes externos.
- **Service Registry**: Se usa dentro de arquitecturas de microservicios para descubrimiento dinámico y escalabilidad interna.

Ambos son complementarios: el **API Gateway** enruta tráfico hacia servicios registrados en un **Service Registry**.