# Roadmap de pulido visual y experiencia — Atleta

Fecha: 7 de noviembre de 2026. Estado: diagnóstico inicial y plan pendiente de ejecución.

## Evidencia y alcance

Se observó la beta abierta en Chrome con una cuenta existente. En escritorio se revisaron Inicio, Partidos y Perfil; a 390 × 844 se revisaron Partidos, Ranking y Perfil. Se observaron principalmente estados sin partidos, equipo ni datos de ranking. La beta puede diferir del código local: verificar la versión antes de implementar. Las capturas se observaron durante la sesión, pero no quedaron guardadas como archivos; repetirlas y conservarlas antes de cerrar cada etapa. No se han verificado dispositivos físicos, contraste medido, teclado, lectores de pantalla ni estados con datos. Esta lista no pretende representar todos los problemas de la aplicación.

## Hallazgos observados

- **H1 — Legibilidad y jerarquía (alta):** etiquetas, iconos y textos secundarios son pequeños en Inicio, Perfil y navegación; el gráfico del perfil tiene rótulos particularmente difíciles de leer en teléfono. Medir tamaños y contraste antes de seleccionar valores.
- **H2 — Iconografía (alta):** los iconos multicolor de navegación y pestañas se ven diminutos y poco distinguibles. Mantener sus etiquetas y revisar también el estado activo.
- **H3 — Perfil (alta):** OVR y nivel general muestran el mismo valor; el gráfico y la lista repiten valores por rol. Hay oportunidad de simplificar la lectura conservando una alternativa textual accesible y la explicación del OVR. En teléfono la información queda distribuida en un recorrido largo.
- **H4 — Partidos vacío (media):** la descripción de la pestaña, «Mi agenda» y el mensaje vacío repiten la ausencia de partidos; la acción de crear está alejada del mensaje en escritorio. Hay una acción principal clara.
- **H5 — Ranking vacío (media):** en teléfono la tarjeta es mucho más estrecha que la pantalla y se muestran varios filtros antes de un mensaje vacío sin siguiente paso. Confirmar qué acciones son posibles antes de proponer una.
- **H6 — Navegación escritorio (media):** la barra inferior ocupa todo el ancho de la ventana mientras el contenido está limitado a una columna central. Revisar alineación y comportamiento al desplazarse sin perder acceso a navegación.
- **H7 — Inicio (media):** «Sin partido agendado» invita a crear o aceptar una invitación, pero la acción visible dice «Ver partidos»; comprobar si el destino permite ambas tareas y ajustar el texto según el resultado.

## Orden de trabajo y criterios de cierre

- [ ] **0. Preparar línea base.** Confirmar versión local y estado Git; levantar un entorno seguro con datos representativos. Capturar Inicio, Partidos, Ranking y Perfil en escritorio y teléfono; incluir estados vacíos, con datos, carga y error. Inventariar rutas restantes (acceso, registro, creación y detalle de partido, cierre, invitaciones, equipos y ajustes) y registrar sus hallazgos sin alterar datos reales. **Cierre:** cada pantalla y estado tiene captura identificada o bloqueo explícito.
- [ ] **1. Fundamentos compartidos (H1, H2, H6).** Revisar tipografía, contraste, espaciado, iconos y navegación compartida. Reutilizar el sistema existente y etiquetas visibles. **Cierre:** navegación reconocible y alineada a 320, 390, 768 y 1440 px; sin desbordamiento horizontal ni contenido tapado; contraste medido, foco visible y controles utilizables con teclado y al 200 % de zoom. Comprobar tamaños táctiles y documentar excepciones.
- [ ] **2. Inicio (H7).** Ordenar identidad, próxima acción, progreso y actividad; verificar los destinos reales y simplificar mensajes repetidos. **Cierre:** es evidente qué hacer con y sin partido; enlaces y contadores conservan su comportamiento, capturas comparadas en ambos tamaños.
- [ ] **3. Partidos e invitaciones (H4).** Hacer el estado vacío breve y acercar la acción principal; revisar agenda, historial, tarjetas con datos e invitaciones. **Cierre:** próximos e historial son distinguibles, creación y respuesta siguen funcionando y los estados de carga/error se entienden.
- [ ] **4. Perfil (H3).** Priorizar identidad, posiciones y OVR; reducir repeticiones visuales sin eliminar datos ni explicación; hacer legible el gráfico y su alternativa textual. Revisar trofeos y equipos. **Cierre:** datos coherentes, legibles y accesibles en ambos tamaños; ajustes y enlaces siguen funcionando.
- [ ] **5. Ranking (H5).** Aprovechar el ancho disponible y jerarquizar filtros y resultados; explicar el estado vacío según sus causas reales. **Cierre:** filtros y búsqueda funcionan con resultados y sin ellos, y se entiende cómo volver a un conjunto de resultados.
- [ ] **6. Flujos restantes.** Aplicar la misma revisión a acceso, onboarding, creación/detalle/cierre de partido, MVP, equipos y social. Registrar problemas concretos, prioridad y criterios antes de resolverlos. **Cierre:** recorridos críticos completos y verificados con datos de prueba; mantener autorización, validaciones y reglas de partido existentes.
- [ ] **7. Validación final.** Revisar cambios y ejecutar lint, build y pruebas relevantes; recorrer las rutas afectadas en escritorio y móvil, con teclado y herramientas de accesibilidad. Comparar capturas antes/después y probar en dispositivo físico si está disponible. **Cierre:** evidencia enlazada por etapa, fallos corregidos o pendientes explícitos y memoria actualizada. No desplegar sin autorización.

## Referencias de implementación a confirmar

- Inicio: `atleta-app/src/app/features/dashboard/pages/home/`.
- Partidos: `atleta-app/src/app/features/matches/pages/matches-hub/`.
- Ranking: `atleta-app/src/app/features/ratings/pages/leaderboard/`.
- Perfil: `atleta-app/src/app/features/user/pages/player-profile/`.
- Navegación compartida: `atleta-app/src/app/shared/ui/metallic-bottom-nav/`.

Ninguna casilla implica que el cambio esté implementado o verificado. La revisión debe ampliarse antes de estimar el trabajo completo.
