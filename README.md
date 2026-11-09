# POC: Activación de Servicios con Arquitectura Orientada a Eventos

Prueba de Concepto (PoC) desarrollada para la cátedra de Programación Avanzada / Sistemas Distribuidos (UADER 2026). Implementa un sistema distribuido basado en microservicios asíncronos comunicados mediante **Apache Kafka**, persistencia en **MongoDB** y una interfaz web de control en tiempo real (`demo-ui`).

---

## 🏗️ Arquitectura del Sistema

El proyecto está estructurado como un monorepo que contiene los siguientes servicios:

* **`activation-api`**: API Gateway principal (NestJS). Recibe las solicitudes de contratación (`POST /activations`), las persiste y emite el evento inicial a Kafka.
* **`billing-service`**: Microservicio encargado de la creación y gestión de cuentas de cobro.
* **`provisioning-service`**: Microservicio encargado del aprovisionamiento técnico del servicio contratado.
* **`crm-analytics-service`** & **`notification-service`**: Microservicios accesorios para auditoría, analítica y envío de notificaciones (integrado con Mailhog).
* **`demo-ui`**: Interfaz web moderna (React + Vite + Tailwind CSS) conectada vía WebSockets para la gestión visual de activaciones.
* **Infraestructura Contenedorizada**:
  * **Apache Kafka + Zookeeper** (Mensajería orientada a eventos).
  * **Kafka-UI** (Monitoreo visual de tópicos y mensajes).
  * **MongoDB** (Base de datos NoSQL para los estados de las activaciones).
  * **Mailhog** (Servidor SMTP de pruebas para correos simulados).

---

## 🚀 Requisitos Previos

* [Docker](https://www.docker.com/) y [Docker Compose](https://docs.docker.com/compose/) instalados y en ejecución.

---

## ⚙️ Cómo Levantar el Proyecto

El entorno entero se despliega de forma unificada utilizando Docker Compose, sin necesidad de instalaciones manuales de dependencias en tu máquina local.

1. Cloná el repositorio y posicionate en la raíz del proyecto.
2. Ejecutá el siguiente comando para construir y levantar todos los contenedores en segundo plano:
   ```bash
   docker compose up -d --build
