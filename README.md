# prueba-arquitecta-microservicios
Arquitectura de Referencia – Migración de Monolito Java a Microservicios  Este repositorio contiene los entregables de la prueba de Arquitectura de Softwar
- **Diagrama de arquitectura de alto nivel** en formato PlantUML (`arquitectura_ecommerce_microservicios.puml`).
- **Documentación de decisiones de arquitectura** (`decision_arquitectura.docx`).
- **Diagramas de secuencia** para el flujo *Crear orden* en enfoques de **Coreografía** y **Orquestación**.

---

## Instrucciones de uso

### 1. Requisitos previos
- [PlantUML](https://plantuml.com/) instalado localmente, o utilizar un [renderizador online](https://www.planttext.com/).
- Editor recomendado: VS Code o IntelliJ con plugin de PlantUML.
- Para los documentos `.docx`, usar MS Word, LibreOffice o Google Docs.

### 2. Renderizar los diagramas PlantUML
Ejemplo en terminal:
```bash
# Generar imagen PNG del diagrama de arquitectura
plantuml arquitectura_ecommerce_microservicios.puml

# Generar imagen PNG del diagrama de secuencia (coreografía)
plantuml seq_coreografia_orden.puml

# Generar imagen PNG del diagrama de secuencia (orquestación)
plantuml seq_orquestacion_orden.puml
```
Esto producirá archivos `.png` en la misma carpeta.

### 3. Estructura de carpetas
```
.
├── arquitectura_ecommerce_microservicios.puml   # Diagrama de arquitectura de alto nivel
├── decision_arquitectura.docx                   # Documento de decisiones y justificación
├── seq_coreografia_orden.puml                   # Diagrama de secuencia – Coreografía
├── seq_orquestacion_orden.puml                  # Diagrama de secuencia – Orquestación
└── README.md                                    # Instrucciones y contexto
```

---

## Decisiones clave de arquitectura

1. **Servicios iniciales (Bounded Contexts):**
   - *Catalog Service* (productos, inventario).
   - *User Service* (cuentas, perfiles).
   - *Order Service* (ciclo de vida de órdenes).

2. **Comunicación entre servicios:**
   - **REST síncrono** para consultas rápidas (validación de usuario/stock).
   - **Eventos asíncronos (Kafka/RabbitMQ)** para procesos de larga duración (reserva de stock, pagos).
   - Uso de **SAGA (coreografía)** para orquestar creación de órdenes.

3. **Gestión de datos:**
   - **Base de datos por servicio**.
   - Consistencia eventual manejada con eventos de dominio, patrón Outbox y CQRS.

4. **Componentes transversales:**
   - API Gateway / Ingress + WAF.
   - Auth Server (OIDC/OAuth2, ej. Keycloak).
   - Service Discovery + Config Server.
   - Observabilidad (logs, métricas, trazas).
   - CI/CD y despliegue en Kubernetes.

5. **Estrategia de modernización:**
   - *Strangler Fig Pattern*: el API Gateway enruta tráfico hacia el monolito o hacia microservicios.
   - Migración incremental: primero catálogo, luego órdenes.

---

## Diagramas incluidos
- `arquitectura_ecommerce_microservicios.puml` → Vista de alto nivel de microservicios, bases de datos y componentes transversales.
- `seq_coreografia_orden.puml` → Flujo *Crear orden* mediante eventos (coreografía).
- `seq_orquestacion_orden.puml` → Flujo *Crear orden* mediante workflow central (orquestación).

---

## Cómo contribuir
1. Clonar el repositorio https://github.com/angelicadr/prueba-arquitecta-microservicios/
2. Modificar o extender diagramas `.puml` según nuevas necesidades.
3. Regenerar imágenes con `plantuml`.
4. Actualizar `decision_arquitectura.docx` si se toman nuevas decisiones.

---

## Autor
**Angélica Duarte** – Arquitecta de Software y Líder Técnica.
**Angélica Duarte** – Arquitecta de Software y Líder Técnico.

