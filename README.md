# Atleta

## Descripcion
Atleta es una plataforma full-stack para futbol amateur. El proyecto combina una aplicacion frontend mobile-first con un backend REST que permite registrar jugadores, gestionar perfiles deportivos, crear equipos, organizar partidos, confirmar convocatorias, cerrar resultados y calcular rendimiento mediante ratings, OVR y leaderboard.

## Problema que resuelve
La organizacion del futbol amateur suele depender de chats, planillas y acuerdos manuales. Eso genera perdida de historial, dificultad para confirmar asistencia, poca trazabilidad de resultados y ausencia de metricas deportivas comparables. Atleta centraliza estos flujos en una experiencia digital orientada a jugadores y organizadores.

## Funcionalidades principales
- Registro, login y sesion de usuarios.
- Onboarding de jugador con alias y posiciones.
- Perfil competitivo con OVR, roles, posiciones y equipos.
- Creacion y gestion de equipos.
- Creacion de partidos con modalidad, categoria, cancha, invitados y colores.
- Confirmacion de asistencia, asignacion de equipos y balanceo.
- Cierre de partido, marcador, goles, XP y votacion MVP.
- Ratings por rol, historial y leaderboard.
- Notificaciones, invitaciones y funcionalidades sociales parciales.

## Stack tecnico
- Frontend: Angular 20, Ionic 8, Capacitor 8, TypeScript, RxJS, Angular Signals.
- Backend: Java 21, Spring Boot, Spring Security, Spring Data JPA, OAuth2, JWT.
- Base de datos: PostgreSQL con migraciones Flyway.
- Testing: JUnit 5, Testcontainers, jqwik, H2, Karma/Jasmine y Playwright.
- Documentacion: OpenAPI/Swagger y documentos Markdown por dominio.
- Despliegue: Docker, Docker Compose y Nginx para SPA.

## Arquitectura / Estructura
El proyecto esta separado en dos aplicaciones principales:

```text
Atleta/
  atleta-app/       # Frontend Ionic/Angular
  atleta-server/    # Backend Spring Boot
```

### Frontend
[`atleta-app`](atleta-app/) implementa la experiencia de usuario mobile-first. Usa arquitectura feature-first con `core`, `shared` y dominios como `auth`, `matches`, `ratings`, `teams`, `fields`, `sessions`, `social` y `user`.

### Backend
[`atleta-server`](atleta-server/) implementa la API REST y la logica de negocio. Usa un monolito modular por capas con controllers, services, repositories, entities, DTOs, migraciones Flyway y documentacion OpenAPI.

## Instalacion y ejecucion local
Requisitos generales:

- Java 21
- Node.js 20 o superior
- npm
- Docker Desktop o PostgreSQL local

### 1. Levantar backend

```bash
cd atleta-server
cp .env.example .env
docker compose up --build
```

La API queda disponible en:

```text
http://localhost:8080
```

Swagger UI:

```text
http://localhost:8080/swagger-ui.html
```

### 2. Levantar frontend

En otra terminal:

```bash
cd atleta-app
npm ci
cp .env.example .env.development
npm start
```

En Windows PowerShell:

```powershell
cd atleta-app
npm ci
Copy-Item .env.example .env.development
npm start
```

El frontend espera por defecto el backend en:

```text
http://localhost:8080/api/v1
```

## Documentacion relacionada
- [README del frontend](atleta-app/README.md)
- [README del backend](atleta-server/README.md)
- [Documentacion de API](atleta-server/api/README.md)
- [Documentacion tecnica backend](atleta-server/docs/README.md)
- [Arquitectura frontend](atleta-app/docs/architecture.md)
- [Funcionalidades frontend](atleta-app/docs/funcionalidades.md)
- [Arquitectura backend](atleta-server/docs/architecture.md)
- [Funcionalidades backend](atleta-server/docs/funcionalidades.md)

## Estado del proyecto
Proyecto en desarrollo avanzado. Los flujos principales de autenticacion, perfil, equipos, partidos, cierre, MVP, ratings y leaderboard estan implementados entre frontend y backend. Todavia existen funcionalidades parciales y deuda tecnica documentada antes de considerarlo listo para produccion.

## Funcionalidades implementadas
- Backend con autenticacion local, Google OAuth, JWT, perfiles, equipos, partidos, ratings, social, canchas y leaderboard.
- Frontend con login, registro, onboarding, perfil competitivo, equipos, partidos, cierre, MVP, rankings y componentes visuales propios.
- Migraciones versionadas con Flyway.
- Configuracion por ambiente para frontend y backend.
- Docker para backend y frontend.

## Funcionalidades en desarrollo o parciales
- Social hub en frontend: existe codigo, pero no esta conectado como ruta principal activa.
- Google auth en frontend: hay CTA, pero no flujo completo implementado.
- Push remoto y badge server-side: infraestructura parcial.
- Automatizaciones temporales de partidos: dependen de lecturas, falta scheduler dedicado.
- Autorizacion fina por identidad y dominio: requiere hardening.

## Proximas mejoras
- Consolidar historial de partidos.
- Separar responsabilidades de servicios grandes en backend.
- Rehabilitar o retirar el modulo social.
- Versionar formulas de rating y XP.
- Agregar jobs programados para inicio, expiracion y recordatorios.
- Ampliar pruebas E2E e integracion.
- Endurecer seguridad de sesion, CORS, secretos y exposicion de Swagger/Actuator.

## Valor profesional del proyecto
Atleta demuestra capacidad para construir un producto full-stack con dominio real, reglas de negocio complejas y comunicacion frontend-backend. El proyecto evidencia experiencia en Angular/Ionic, Spring Boot, seguridad JWT/OAuth, modelado relacional, migraciones, arquitectura modular, testing, documentacion tecnica y preparacion para despliegue.

## Mejoras visuales sugeridas
- Capturas de onboarding, perfil competitivo, creacion de partido, detalle de partido y leaderboard.
- GIF del flujo crear partido -> confirmar jugadores -> cerrar partido -> actualizar OVR.
- Diagrama de arquitectura frontend/backend/base de datos.
- Diagrama de dominio para atleta, perfil, equipo, partido, rating y notificaciones.
- Enlace a una demo desplegada cuando exista un ambiente estable.
