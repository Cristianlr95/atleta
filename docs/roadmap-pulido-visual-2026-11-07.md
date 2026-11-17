# Roadmap de pulido visual y experiencia — Atleta

Fecha: 7 de noviembre de 2026; seguimiento actualizado el 16/11/2026. Estado: H0 comprobado localmente; Perfil y Plantel aprobados y cerrados en su parte visual por el usuario el 16/11/2026; H5 visual aprobado. Backend, validación real en beta, dispositivos físicos y auditoría general pendientes.

## Publicación en main solicitada — 16/11/2026

Frontend publicado en `atleta-app/main@1e1ddd8cc1bd11c036d3099ba048c4f9795d5cbd`, integrando main previo con la revisión visual aprobada. [Registro de integración](../atleta-app/docs/main-integration-2026-11-16.md): build/lint, 271 unitarias, 73 E2E y audit runtime correctos; tres smoke omitidos por falta de credenciales A/B. La referencia del backend se conserva en `e6b3f1adaf0156eb06d9123e5c3235b2d3177ecc`. Este commit actualiza el roadmap y la referencia del frontend, e incorpora `.gitmodules` para resolver ambos repositorios al clonar.

La publicación de Git no acredita despliegue o validación funcional en beta. Los pendientes backend/beta permanecen abiertos. Los checkouts originales con cambios locales se preservaron mediante worktrees de integración.

## Evidencia y alcance

La observación inicial del 7/11 registró la beta abierta en Chrome con una cuenta existente; no acredita acceso ni revisión de la versión aprobada hoy. Actualmente no hay cuenta de prueba confirmada para la validación pendiente. En escritorio se revisaron Inicio, Partidos y Perfil; a 390 × 844 se revisaron Partidos, Ranking y Perfil. Se observaron principalmente estados sin partidos, equipo ni datos de ranking. La beta puede diferir del código local: verificar la versión antes de implementar. Las capturas se observaron durante la sesión, pero no quedaron guardadas como archivos; repetirlas y conservarlas antes de cerrar cada etapa. No se han verificado dispositivos físicos, contraste medido, teclado, lectores de pantalla ni estados con datos. Esta lista no pretende representar todos los problemas de la aplicación.

## Hallazgos observados

- **H1 — Legibilidad y jerarquía (alta):** etiquetas, iconos y textos secundarios son pequeños en Inicio, Perfil y navegación; el gráfico del perfil tiene rótulos particularmente difíciles de leer en teléfono. Medir tamaños y contraste antes de seleccionar valores.
- **H2 — Iconografía (alta):** los iconos multicolor de navegación y pestañas se ven diminutos y poco distinguibles. Mantener sus etiquetas y revisar también el estado activo.
- **H3 — Perfil (alta):** OVR y nivel general muestran el mismo valor; el gráfico y la lista repiten valores por rol. Hay oportunidad de simplificar la lectura conservando una alternativa textual accesible y la explicación del OVR. En teléfono la información queda distribuida en un recorrido largo.
- **H4 — Partidos vacío (media):** la descripción de la pestaña, «Mi agenda» y el mensaje vacío repiten la ausencia de partidos; la acción de crear está alejada del mensaje en escritorio. Hay una acción principal clara.
- **H5 — Ranking vacío (media):** en teléfono la tarjeta es mucho más estrecha que la pantalla y se muestran varios filtros antes de un mensaje vacío sin siguiente paso. Confirmar qué acciones son posibles antes de proponer una.
- **H6 — Navegación escritorio (media):** la barra inferior ocupa todo el ancho de la ventana mientras el contenido está limitado a una columna central. Revisar alineación y comportamiento al desplazarse sin perder acceso a navegación.
- **H7 — Inicio (media):** «Sin partido agendado» invita a crear o aceptar una invitación, pero la acción visible dice «Ver partidos»; comprobar si el destino permite ambas tareas y ajustar el texto según el resultado.

## Orden de trabajo y criterios de cierre

- [x] **0. Línea base (H0), cuatro pantallas del encargo.** Completada antes de modificar H3, en el commit frontend `6f0d44b`, base `6fcd35b` (H5 aprobado, descendiente de develop). Inicio `/home`, Partidos `/matches`, Ranking `/leaderboard` y Perfil `/player/profile`: datos, carga, vacío y HTTP 500 en 390/1440 px; 32 registros, 31 capturas nuevas y una reutilizada con procedencia identificada. Ruta, entorno, commit, viewport y estado registrados en el [inventario local](../atleta-app/docs/h0-h3-2026-11-16/linea-base.md). Angular normal y API interceptada; los 32 estados se reprodujeron. **Límites:** beta sin cuenta confirmada, dispositivo físico y lector real no disponibles. Las rutas restantes continúan en H6 y la validación integral en la etapa 7.
- [ ] **1. Fundamentos compartidos (H1, H2, H6).** Revisar tipografía, contraste, espaciado, iconos y navegación compartida. Reutilizar el sistema existente y etiquetas visibles. **Cierre:** navegación reconocible y alineada a 320, 390, 768 y 1440 px; sin desbordamiento horizontal ni contenido tapado; contraste medido, foco visible y controles utilizables con teclado y al 200 % de zoom. Comprobar tamaños táctiles y documentar excepciones.
- [ ] **2. Inicio (H7).** Ordenar identidad, próxima acción, progreso y actividad; verificar los destinos reales y simplificar mensajes repetidos. **Cierre:** es evidente qué hacer con y sin partido; enlaces y contadores conservan su comportamiento, capturas comparadas en ambos tamaños.
- [x] **3. Partidos e invitaciones (H4).** El estado vacío dice «Sin partidos todavía.» y sitúa «Crear primer partido» debajo del mensaje. En escritorio se centra el bloque y en móvil se alinea a la izquierda. El botón mantiene un área táctil de al menos 44 px y foco visible. **Validación focalizada:** se reportaron aprobadas las pruebas dirigidas de H4. La auditoría integral sigue pendiente.
- [x] **4. Perfil (H3) y Plantel: parte visual lista, aprobada por el usuario el 16/11/2026.** Fuente aprobada y probada `9bb209f31a34f754615010ad9a8a2e2e12ed297a`, rama `codex/profile-sections-navigation-20261116`. Perfil con OVR único y explicación, hexágono visible con datos y estadísticas debajo, sin desgloses visibles repetidos y con alternativa textual accesible; vacío/error y reintento conservados. Plantel con OVR medio y cobertura, hexágono agregado, listado y ficha de jugador en modal sin salir de la sección; permisos de gestión conservados. **Última verificación local:** 265 unitarias, 14 E2E a 390/1440 px y build/lint correctos con API simulada. [Evidencia final](../atleta-app/docs/profile-visible-radar-2026-11-16/verificacion.md). **No cierra:** datos backend ni beta; ver pendientes separados debajo. La integración publicada se registra arriba; no se declara despliegue validado.
- [x] **5. Ranking (H5), alcance visual.** Finalizado y aprobado por el usuario el 16/11/2026. Conserva el ancho móvil del PR #23, diferencia vacíos, permite limpiar búsquedas y reintentar errores; añade la propuesta de goles/MVP/últimos cinco resultados con datos de ejemplo. La tabla se desliza dentro de su contenedor con puesto/jugador fijos y barra oscura/cian. Revisión visual `f6e2a64`, rama frontend `codex/h5-ranking-review-20261116`; informe `atleta-app/docs/h5-ranking-2026-11-16.md`. **Comprobado:** build/lint, 15 unitarias de Ranking, 7 E2E completos y recorrido final con Chrome visible; evidencia móvil/escritorio en el informe. **Pendiente separado:** estadísticas reales e integración con beta, registradas como `BE-RANK-01` a `BE-RANK-05` en `atleta-server/docs/backlog-ranking-h5.md`, rama `codex/h5-ranking-backlog-20261116`. Sin validación de beta ni dispositivo físico; este cierre no acredita API real, integración de ramas ni despliegue.
- [ ] **6. Flujos restantes.** Aplicar la misma revisión a acceso, onboarding, creación/detalle/cierre de partido, MVP, creación/administración de equipos y social; el diseño del plantel ya está aprobado en la etapa 4. Registrar problemas concretos, prioridad y criterios antes de resolverlos. **Cierre:** recorridos críticos completos y verificados con datos de prueba; mantener autorización, validaciones y reglas de partido existentes.
- [ ] **7. Validación final.** Revisar cambios y ejecutar lint, build y pruebas relevantes; recorrer las rutas afectadas en escritorio y móvil, con teclado y herramientas de accesibilidad. Comparar capturas antes/después y probar en dispositivo físico si está disponible. **Cierre:** evidencia enlazada por etapa, fallos corregidos o pendientes explícitos y memoria actualizada. No desplegar sin autorización.

## Pendientes separados del cierre visual de Perfil y Plantel

### Backend — abierto

- [ ] **BE-PLANTEL-01:** goles/asistencias por integrante en DTO agregado y alcance definido (trayectoria o equipo). Hasta disponer de API, «Sin datos».
- [ ] **BE-PLANTEL-02:** PJ exclusivos del equipo, si ese es el alcance requerido. La UI actual muestra PJ totales de trayectoria.
- [ ] **BE-PLANTEL-03:** contrato compatible, partidos/participaciones válidos, autorización y distinción entre cero, ausencia y fallo.
- [ ] **BE-PLANTEL-04:** contrastar integrantes activos y promedio con datos reales. El OVR agregado actual es de presentación; un valor oficial persistido/histórico requiere decisión e implementación backend, solo si se necesita.

[Detalle backend](../atleta-app/docs/team-list-2026-11-16/backend-pendientes.md). Estos pendientes no se marcaron implementados con la aprobación visual. H5 conserva su backlog independiente BE-RANK-01..05.

### Beta — pendiente, sin cuenta de prueba confirmada

- [ ] Confirmar URL/entorno y SHA frontend/backend desplegados; obtener cuenta de prueba por canal privado y verificar correspondencia con la revisión aprobada.
- [ ] Probar perfiles con datos y nuevos; planteles con varios integrantes, vacíos y con valores ausentes/cero. Contrastar medias/cobertura y el alcance real de PJ/goles/asistencias.
- [ ] Validar carga, vacío, HTTP 500 y recuperación controlada; navegación, modal, foco y permisos de creador/jugador a 390/1440 px. Documentar escenarios no reproducibles y su motivo.
- [ ] Conservar capturas y metadatos de ruta, entorno, viewport, estado y revisión. Teléfono físico, lector de pantalla y auditoría integral siguen pendientes, separados de la aprobación visual.

[Checklist y estado vigente del frontend](../atleta-app/docs/roadmap-frontend.md). Este cierre es documental y local: no publica, integra ni despliega cambios.

## Referencias de implementación a confirmar

- Inicio: `atleta-app/src/app/features/dashboard/pages/home/`.
- Partidos: `atleta-app/src/app/features/matches/pages/matches-hub/`.
- Ranking: `atleta-app/src/app/features/ratings/pages/leaderboard/`.
- Perfil: `atleta-app/src/app/features/user/pages/player-profile/`.
- Navegación compartida: `atleta-app/src/app/shared/ui/metallic-bottom-nav/`.

Cada casilla cierra únicamente el alcance y la evidencia expresamente indicados. Las aprobaciones visuales no acreditan backend completo, validación de beta, integración o despliegue; los pendientes conservan sus casillas abiertas.
