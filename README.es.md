<p align="center">
  <img src="docs/logo/openwa_logo.webp" alt="Logo de OpenWA" width="200"/>
</p>

<h1 align="center">OpenWA</h1>
<p align="center">
  <strong>Pasarela API de WhatsApp de Código Abierto (Open Source WhatsApp API Gateway)</strong>
</p>

<p align="center">
  <a href="#-características">Características</a> •
  <a href="#-inicio-rápido">Inicio Rápido</a> •
  <a href="#-documentación">Docs</a> •
  <a href="#-ejemplos-de-la-api">API</a> •
  <a href="#-contribuir">Contribuir</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.1.6-blue.svg" alt="Versión"/>
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="Licencia"/>
  <img src="https://img.shields.io/badge/node-22_LTS-brightgreen.svg" alt="Node"/>
  <img src="https://img.shields.io/badge/NestJS-11.x-red.svg" alt="NestJS"/>
  <img src="https://img.shields.io/badge/docker-ready-blue.svg" alt="Docker"/>
  <img src="https://img.shields.io/badge/TypeScript-5.x-3178C6.svg" alt="TypeScript"/>
</p>

<p align="center">
  [Read in English](README.md)
</p>

---

## ✨ ¿Por qué OpenWA?

**OpenWA** es una pasarela API de WhatsApp gratuita y de código abierto diseñada para desarrolladores que necesitan control total sobre su infraestructura de mensajería, sin dependencias de proveedores externos ni cobros ocultos.

Construido sobre una **arquitectura modular (pluggable)**, OpenWA te permite intercambiar motores de bases de datos (SQLite/PostgreSQL), sistemas de almacenamiento de archivos (Local/S3) y capas de caché (Memoria/Redis) sin cambiar una sola línea de código de tu aplicación.

|                               |                                                              |
| ----------------------------- | ------------------------------------------------------------ |
| 🔓 **100% Código Abierto**    | Sin tarifas de licencia, sin funciones bloqueadas, acceso total al código fuente. |
| 🏗️ **Arquitectura Modular**   | Intercambia adaptadores de base de datos, almacenamiento y caché mediante configuración. |
| 🖥️ **Panel de Control Completo** | Interfaz moderna en React para gestionar sesiones, webhooks y claves API. |
| 🔹 **Listo para Multi-Sesión** | Ejecuta múltiples sesiones de WhatsApp de forma concurrente en una sola instancia. |
| 🐳 **Nativo en Docker**       | Listo para producción con configuración cero.                |
| 🔗 **Integración con n8n**    | Nodos comunitarios para automatización de flujos de trabajo. |

---

## 🎯 Características

### Características Principales

| Característica | Estado | Descripción |
| ------------- | ------ | ----------- |
| API REST      | ✅     | API completa de WhatsApp mediante endpoints HTTP |
| Multi-Sesión  | ✅     | Gestiona múltiples cuentas de WhatsApp |
| Webhooks      | ✅     | Eventos en tiempo real con firmas de seguridad HMAC |
| Panel Web     | ✅     | Interfaz visual de administración y monitoreo |
| Autenticación | ✅     | Acceso seguro mediante Claves API |
| Docs Swagger  | ✅     | Documentación interactiva de la API |

### Mensajería

| Característica | Estado | Descripción |
| ----------------- | ------ | ----------- |
| Mensajes de Texto | ✅     | Envío y recepción de mensajes de texto simple |
| Mensajes Multimedia | ✅   | Imágenes, videos, documentos y notas de audio |
| Reacciones        | ✅     | Reacciona a los mensajes utilizando emojis |
| Envíos Masivos    | ✅     | Envío de mensajes a múltiples destinatarios |
| Estado de Mensaje | ✅     | Rastreo de confirmaciones de entrega y lectura |

### Avanzado

| Característica | Estado | Descripción |
| ------------------- | ------ | ----------- |
| API de Grupos       | ✅     | Crea, gestiona y envía mensajes a grupos |
| Canales/Boletines   | ✅     | Soporte completo para Canales de WhatsApp |
| Gestión de Etiquetas| ✅     | Organiza tus chats mediante etiquetas (WhatsApp Business) |
| Soporte de Proxy    | ✅     | Configuración de proxies individuales por sesión |
| Límite de Peticiones| ✅     | Límites de velocidad de peticiones configurables |
| Lista Blanca CIDR   | ✅     | Control de acceso a la API basado en direcciones IP |
| Registros de Auditoría| ✅   | Historial de todas las operaciones realizadas en la API |

### Infraestructura

| Característica | Estado | Descripción |
| ---------------- | ------ | ----------- |
| SQLite           | ✅     | Base de datos local integrada sin configuración previa |
| PostgreSQL       | ✅     | Base de datos robusta de nivel de producción |
| Caché de Redis   | ✅     | Caché de alto rendimiento opcional |
| Almacenamiento S3/MinIO | ✅ | Almacenamiento en la nube escalable para archivos multimedia |
| Docker           | ✅     | Despliegue rápido con un solo comando |
| Controles de Salud| ✅     | Sondas de salud integradas y listas para Kubernetes |
| Migración de Datos| ✅     | Exporta e importa datos fácilmente entre backends |

---

## 🚀 Inicio Rápido

### Opción A: Docker (Recomendado)

```bash
# Clonar el repositorio e iniciar
git clone https://github.com/rmyndharis/OpenWA.git
cd OpenWA
docker compose -f docker-compose.dev.yml up -d

# Direcciones de Acceso
# Panel de Control: http://localhost:2886
# API REST: http://localhost:2785/api
# Documentación Swagger: http://localhost:2785/api/docs
```

### Opción B: Desarrollo Local

```bash
# Clonar el repositorio
git clone https://github.com/rmyndharis/OpenWA.git
cd OpenWA

# Instalar dependencias (incluye la instalación del panel web de forma automática)
npm install

# Iniciar API + Panel Web (la configuración inicial se autogenera en la primera ejecución)
npm run dev

# Direcciones de Acceso
# Panel de Control: http://localhost:2886
# API REST: http://localhost:2785/api
# Documentación Swagger: http://localhost:2785/api/docs
```

---

## 🏭 Despliegue en Producción

Para entornos productivos, utiliza el archivo principal `docker-compose.yml` con soporte de perfiles para habilitar los servicios opcionales:

```bash
# Producción básica (SQLite, almacenamiento local)
docker compose up -d

# Con base de datos PostgreSQL externa
docker compose --profile postgres up -d

# Stack completo (PostgreSQL, Redis, Panel Web, Proxy Inverso Traefik)
docker compose --profile full up -d
```

| Perfil | Servicios Incluidos |
| ---------------- | --------------------- |
| `postgres`       | Base de datos PostgreSQL |
| `redis`          | Caché de Redis |
| `minio`          | Almacenamiento compatible con S3 (MinIO) |
| `with-dashboard` | Panel de administración web |
| `with-proxy`     | Proxy inverso Traefik |
| `full`           | Todos los servicios mencionados anteriormente |

> **Diferencias entre Desarrollo y Producción**
>
> - Desarrollo (`docker-compose.dev.yml`): SQLite, almacenamiento local, incluye tanto la API como el Panel Web.
> - Producción (`docker-compose.yml`): Base de datos configurable, perfiles flexibles para habilitar componentes de forma modular.

## 🔌 Puertos Utilizados

| Servicio | Puerto | Descripción |
| --------- | --------------- | ------------------------ |
| API | `2785` | Endpoints de la API REST |
| Panel Web | `2886` | Interfaz gráfica de administración |
| Swagger | `2785/api/docs` | Documentación interactiva de la API |

---

## 📡 Ejemplos de la API

### Crear una Sesión

```bash
curl -X POST http://localhost:2785/api/sessions \
  -H "Content-Type: application/json" \
  -H "X-API-Key: TU_CLAVE_API" \
  -d '{"name": "mi-bot"}'
```

### Iniciar Sesión y Obtener Código QR

```bash
# Iniciar el proceso de la sesión
curl -X POST http://localhost:2785/api/sessions/{sessionId}/start \
  -H "X-API-Key: TU_CLAVE_API"

# Obtener el código QR (escanéalo con la app de WhatsApp)
curl http://localhost:2785/api/sessions/{sessionId}/qr \
  -H "X-API-Key: TU_CLAVE_API"
```

### Enviar un Mensaje de Texto

```bash
curl -X POST http://localhost:2785/api/sessions/{sessionId}/messages/send-text \
  -H "Content-Type: application/json" \
  -H "X-API-Key: TU_CLAVE_API" \
  -d '{
    "chatId": "5211234567890@c.us",
    "text": "¡Hola desde OpenWA en español!"
  }'
```

### Configurar un Webhook

```bash
curl -X POST http://localhost:2785/api/sessions/{sessionId}/webhooks \
  -H "Content-Type: application/json" \
  -H "X-API-Key: TU_CLAVE_API" \
  -d '{
    "url": "https://mi-servidor.com/webhook",
    "events": ["message.received", "session.status"],
    "secret": "mi-secreto-hmac"
  }'
```

---

## 🛠 Tecnologías Utilizadas

| Capa | Tecnología |
| ------------- | ----------------------- |
| **Entorno de Ejecución** | Node.js 22 LTS |
| **Framework** | NestJS 11.x |
| **Lenguaje** | TypeScript 5.x |
| **Motor de WhatsApp** | whatsapp-web.js |
| **Bases de Datos** | SQLite / PostgreSQL |
| **Caché** | Redis (opcional) |
| **Almacenamiento** | Local / S3 / MinIO |
| **ORM** | TypeORM |
| **Contenedores** | Docker + Docker Compose |

---

## 📁 Estructura del Proyecto

```
openwa/
├── src/
│   ├── main.ts                 # Punto de entrada de la aplicación
│   ├── app.module.ts           # Módulo raíz
│   ├── config/                 # Configuraciones del sistema
│   ├── common/                 # Utilidades compartidas
│   │   ├── cache/              # Caching mediante Redis
│   │   └── storage/            # Almacenamiento de archivos (Local/S3)
│   ├── core/                   # Núcleo del sistema
│   │   ├── hooks/              # Hooks del sistema de plugins
│   │   └── plugins/            # Gestión de plugins
│   ├── engine/                 # Abstracción del motor de WhatsApp
│   └── modules/
│       ├── session/            # Gestión de sesiones
│       ├── message/            # Envío y recepción de mensajes
│       ├── webhook/            # Configuración de webhooks
│       ├── group/              # API para gestión de grupos
│       ├── contact/            # API para contactos
│       ├── auth/               # Autenticación mediante Claves API
│       ├── infra/              # Panel de control de infraestructura
│       └── health/             # Endpoints para controles de salud
├── dashboard/                  # Panel de control web desarrollado en React
├── docs/                       # Documentación adicional del proyecto
├── docker-compose.yml
├── Dockerfile
└── package.json
```

---

## 📚 Documentación

Encuentra guías y documentación detallada en la carpeta `docs/`:

| Documento | Descripción |
| ------------------------------------------------------- | ---------------------------- |
| [Descripción del Proyecto](./docs/01-project-overview.md) | Introducción y objetivos |
| [Especificación de Requisitos](./docs/02-requirements-specification.md) | Requisitos de características |
| [Arquitectura del Sistema](./docs/03-system-architecture.md) | Diseño de la arquitectura de la solución |
| [Diseño de Seguridad](./docs/04-security-design.md) | Medidas e implementación de seguridad |
| [Diseño de Base de Datos](./docs/05-database-design.md) | Modelo de datos y migraciones |
| [Especificación de la API](./docs/06-api-specification.md) | Referencia detallada de los endpoints de la API |
| [Guía de Desarrollo](./docs/08-development-guidelines.md) | Estándares de codificación |
| [Guía de Migración](./docs/14-migration-guide.md) | Migración entre bases de datos y almacenamiento |

---

## 🤝 Contribuir

¡Agradecemos enormemente las contribuciones de la comunidad! Para comenzar:

1. Realiza un **Fork** del repositorio.
2. Crea tu propia rama de características (`git checkout -b feature/mi-caracteristica`).
3. Confirma tus cambios (`git commit -m 'Añadir nueva característica'`).
4. Sube la rama a tu repositorio (`git push origin feature/mi-caracteristica`).
5. Abre una **Pull Request** detallada.

Consulta las [Pautas de Desarrollo (en inglés)](./docs/08-development-guidelines.md) para más detalles sobre nuestros estándares y mejores prácticas de código.

---

## 📄 Licencia

Este proyecto está bajo la **Licencia MIT** – Es completamente de uso libre tanto para fines personales como comerciales.

Revisa el archivo de [LICENCIA](./LICENSE) para más detalles.

---

<div align="center">

**OpenWA** – Pasarela API de WhatsApp de Código Abierto y Gratuita

[📖 Documentación (en inglés)](./docs/README.md) · [🔌 API Docs](http://localhost:2785/api/docs) · [🐛 Reportar Bug](https://github.com/rmyndharis/OpenWA/issues) · [💡 Solicitar Característica](https://github.com/rmyndharis/OpenWA/issues)

<br/>

<sub>Creado con ❤️ por <a href="https://github.com/rmyndharis">Yudhi Armyndharis</a> y la Comunidad de OpenWA</sub>

</div>
