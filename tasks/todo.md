# Tareas — mejora visual de Atleta

Estado inicial: pendientes. Las rutas son orientativas; confirmar consumidores y alcance antes de editar.

## 1. Completar la evidencia visual
- [x] Capturar onboarding, pasos restantes de creación, cierre activo y MVP abierto usando estados locales apropiados; documentar bloqueos sin modificar resultados existentes.
- [x] Revisar móvil y escritorio y anotar los estados vacíos, errores y restricciones relevantes.
**Verificación:** capturas actuales inspeccionadas y lista de estados cubiertos y pendientes. **Dependencia:** ninguna.

Avance: convocatoria y confirmación revisadas con cancha local; capturas `25-convocatoria.png` y `26-confirmacion.png`. No se enviaron invitaciones ni se modificaron partidos existentes.

Actualización: cierre activo (tres pasos) y MVP abierto capturados en copia aislada (`31`–`35`); voto de prueba registrado solo en esa copia. En esa etapa aún faltaban los estados seleccionados de onboarding y la revisión sistemática de escritorio; ambos se completaron en la revisión del 06/11/2026.
Avance 06/11/2026: Inicio revisado con capturas actuales a 320, 390 y 1366 px y un partido finalizado a 390 px en `atleta-app/docs/auditoria-ux-2026-11-06/inicio/`. Se inspeccionaron estados vacíos y errores con capturas superiores e inferiores en los tres anchos. Vacío: invita a crear/aceptar partido y completar el primero para ver actividad. Restricciones: equipo no disponible ofrece reintento, invitaciones y OVR/XP ausentes no se presentan como cero, y XP/nivel no disponibles se explica. Con fallos simultáneos de historial, equipo, invitaciones y perfil, los mensajes se mantienen sin desbordamiento; reintentos de historial/invitaciones quedan por encima de la navegación fija al desplazar. Limitación observada: el fallo de historial se comunica tanto en «En cancha» como en «Actividad reciente». Pruebas simuladas, no API real. La auditoría del resto de pantallas y lector de pantalla siguen pendientes.
Actualización 06/11/2026: onboarding seleccionado y escritorio se revisaron en 320/390/768/1366 px; estados vacíos, errores, restricciones y rutas de recuperación de agenda, historial, cierre/MVP, ranking/estadísticas, equipo, perfil público, Social y Jugar están anotados en las tareas correspondientes. El E2E integral del flujo visual pasa (43 pruebas). Quedan pendientes lector de pantalla y dispositivo físico; el punto B se verificó con API y PostgreSQL desechables.

## 2. Acordar una muestra visual de Inicio
- [x] Preparar una propuesta sobre Inicio que defina jerarquía, tipografía, espaciado y uso de cian/amarillo; contrastarla con la pantalla actual.
- [x] Acordar intensidad metálica y reglas visuales antes de extenderlas.
**Verificación:** muestra visible en móvil y escritorio y decisiones registradas. **Dependencia:** ninguna; incorporar hallazgos de 1 cuando afecten patrones globales.

Selección del usuario: primera imagen generada en la conversación. Propuesta contrastada con Inicio a 320, 390 y 1366 px; capturas actualizadas en `atleta-app/docs/auditoria-ux-2026-11-06/inicio/`. Cabecera alineada a la izquierda con marca oficial; CTA debajo del detalle en móvil; OVR conserva protagonismo. Se conserva la intensidad metálica actual.
Decisión de integridad de datos: no presentar XP total ni niveles/rangos sin fuente verificada. La muestra mantiene XP de posición principal y progreso respaldado por sus reglas actuales. Quedan diferencias deliberadas respecto de la imagen (datos ficticios, logotipo e iconografía); ver `design-qa.md`. Se completó el punto de control A antes de ampliar estilos compartidos.

## 3. Mejorar lectura y superficies compartidas
- [x] Ajustar por cortes pequeños los estilos y componentes compartidos necesarios para legibilidad, contraste y jerarquía, reutilizando `metallic-card` y `metallic-form-section`.
- [x] Comprobar sus consumidores y estados en pantallas representativas.
**Verificación:** contraste medido, capturas antes/después y build frontend. **Dependencia:** 2.
Avance 06/11/2026: se cambió la descripción común de `metallic-form-section` al token `--muted-foreground`: contraste medido 9,48:1 vs 5,92:1 previo sobre `#06141b`. El texto de `metallic-card` ya mide 10,25:1, por lo que se conservó. Consumidor de creación de partido inspeccionado a 390/1366 px; capturas en `atleta-app/docs/auditoria-ux-2026-11-06/inicio/shared-form-description-*.png`. E2E, lint y build pasan. La descripción de controles pendientes quedó desactualizada y se corrigió en esta iteración.

## 4. Unificar controles y navegación
- [x] Aplicar el patrón acordado a botones, campos, selectores y navegación, incluyendo foco, errores y deshabilitados.
- [x] Revisar etiquetas, accesibilidad de controles y consistencia de acciones de regreso.
**Verificación:** teclado y estados relevantes en móvil/escritorio; pruebas existentes afectadas y build. **Dependencia:** 2; coordinar con 3.
Completado 06/11/2026: placeholder usa `--muted-foreground` (8,73:1 sobre `--input-background`, frente a 3,47:1 previo); input/select inválidos resaltan borde y anillo sin perder foco. Las acciones del wizard ahora tienen foco visible, mínimo táctil de 44 px y deshabilitado consistente. Se comprobó teclado, estado activo y retorno desde creación; navegación inferior mantiene `aria-current`. E2E de acceso/registro/recuperación en 320/1366 px, onboarding en 320/390/768/1366 px y navegación responsive pasan; pruebas unitarias de input/select pasan. Lector de pantalla y dispositivos físicos siguen pendientes.

## Punto de control A
- [x] Revisar Inicio y pantallas representativas con las reglas compartidas; corregir regresiones antes de ampliarlas.
Revisión completada: Inicio cubierto con E2E responsive de estados vacíos, finalizados y error; la creación de partido se verificó en móvil y escritorio. Las pruebas representativas pasan; capturas nuevas disponibles en la carpeta de auditoría de Inicio.

## 5. Acceso y onboarding
- [x] Aplicar patrones acordados a acceso, registro y recuperación; mejorar instrucciones y legibilidad.
- [x] Revisar onboarding capturado y dividir su implementación si requiere cambios adicionales.
**Verificación:** recorrido de formularios, errores y teclado; capturas móvil/escritorio. **Dependencias:** 1, 3 y 4.
Completado 06/11/2026: los formularios reutilizan campos, selectores, ayudas y mensajes asociados por `aria-describedby`; los errores se anuncian y resaltan. Inicio de sesión, registro y recuperación se verificaron en 320/1366 px; onboarding seleccionado se inspeccionó y comprobó en 320/390/768/1366 px, sin desbordamiento y con selección/guardado esperado. Quedan fuera de esta verificación lector de pantalla y dispositivo físico.

## 6. Inicio y perfil
- [x] Mejorar jerarquía de Inicio y aclarar el rótulo del último/próximo partido según el estado real.
- [x] Ordenar perfil y ajustes sin ocultar información ni alterar datos.
**Verificación:** comparar capturas y estados con/sin datos; verificar navegación. **Dependencias:** 3 y 4.
Completado 06/11/2026: Inicio diferencia «Próximo partido», «Partido en juego» y «Último partido» según el estado, con acentos correctos. El CTA «Ver partidos» se apila bajo el detalle en móvil. Perfil y Ajustes se revisaron sin sustituir ni ocultar datos; acciones e inputs de Ajustes tienen áreas táctiles de 44/46 px. E2E responsive de perfil y ajustes en 390/1366 px, de Inicio con los tres estados y de navegación pasan.

## 7. Agenda e historial
- [x] Mejorar estado vacío y acciones de agenda.
- [x] Diseñar y aplicar una vista legible del historial móvil manteniendo acceso a todos los datos.
**Verificación:** agenda vacía y con datos; historial en móvil/escritorio y acceso al detalle. **Dependencias:** 2–4.
Completado 06/11/2026: la agenda vacía anuncia que no hay partidos y ofrece «Crear primer partido»; botón de 44 px verificado en 390/1366 px. Agenda con partido próximo abre su estado en móvil/escritorio. Historial móvil conserva los 13 campos y abre el detalle; la tabla de escritorio y encabezados se comprueban en 1366 px. Errores/reintentos mantienen la distinción respecto de listas vacías.

## 8. Crear partido y cancha
- [x] Ordenar cada paso de creación y el formulario de cancha sin cambiar validaciones ni reglas.
- [x] Unificar navegación y mensajes de ayuda, carga y error.
**Verificación:** recorrido de creación con datos de prueba, incluyendo validación y selección de cancha; capturas móvil/escritorio. **Dependencias:** 1, 3 y 4.
Completado 06/11/2026: se verificaron los tres pasos de creación, validación y navegación de regreso en 390/1366 px; carga/reintento de canchas, búsqueda por teclado y coordenadas se probaron en E2E. No se cambiaron validaciones ni reglas del partido.

## 9. Detalle y estados del partido
- [x] Priorizar estado y siguiente acción; sustituir etiquetas técnicas y organizar participantes, equipos y ubicación.
- [x] Comprobar estados creados, confirmados, en juego y finalizados según disponibilidad y permisos.
**Verificación:** recorridos representativos y pruebas pertinentes de invitaciones y participantes. **Dependencias:** 1, 3 y 4.
Completado 06/11/2026: el detalle prioriza el flujo y la próxima acción, «Header partido» se reemplazó por «Resumen del partido» y se corrigieron etiquetas de ubicación/estado. Un E2E comprueba los pasos «Listo», «Cerrar» y «Resultados» y la aparición de las acciones de iniciar, cerrar y votar MVP; pruebas de ciclo cubren creado, parcial, confirmado, en juego, cierre pendiente, finalizado e inválido.

## 10. Cierre y MVP
- [x] Ajustar jerarquía y textos de estados activos, bloqueados y cerrados; retirar instrucciones contradictorias en votación cerrada.
- [x] Mantener autorización, ventana, marcador, participantes confirmados y procesamiento de OVR.
**Verificación:** pruebas relevantes de cierre/MVP y recorrido local sin iniciar un partido al abrir la URL de cierre. **Dependencias:** 1 y 9.
Completado 06/11/2026: los pasos de cierre se anuncian como lista ordenada con paso actual; la votación cerrada ya no invita a votar. E2E comprueba que la URL de cierre no inicia ni escribe en un partido no iniciado, que solo el creador puede editar/confirmar y que el marcador debe coincidir con los goles asignados. Pruebas unitarias cubren ventana de una a tres horas, participantes confirmados sin duplicados y estados de voto; recompensas muestran XP/OVR sin derivar niveles ficticios. El cierre real contra API no se ejecutó en este entorno.

## Punto de control B
- [ ] Revisar el flujo de partidos de extremo a extremo en datos locales, junto con pruebas y capturas de estados disponibles.
Pendiente: las pruebas de esta iteración usan respuestas simuladas; hace falta un entorno con API y datos locales reales para cerrar el punto.

## 11. Ranking y estadísticas
- [x] Mejorar lectura de filtros, cifras y tablas; investigar diferencias visibles de OVR antes de proponer cambios de datos o fórmulas.
**Verificación:** ranking con datos y sin resultados, estadísticas y vistas móvil/escritorio. **Dependencias:** 3 y 4.
Completado 06/11/2026: filtros y acciones del ranking tienen foco visible y objetivos táctiles de 44 px; las estadísticas distribuyen roles e historial en dos columnas en escritorio. La ausencia de ratings (404) se muestra como estado vacío, mientras otros errores muestran mensaje y reintento; se corrigió además el vacío de roles que antes presentaba seis ceros. E2E de ranking con datos y estadísticas vacías/fallidas pasan a 320/1366 px; unitarias cubren búsqueda sin resultados. Inicio, perfil y estadísticas leen `hybridOVR` del endpoint de ratings; el ranking de plataforma presenta `score` del endpoint de leaderboard y el ranking de equipo consume el agregado del equipo. No se recalcularon fórmulas sin comparar respuestas reales equivalentes del backend.

## 12. Equipo, social y pantallas secundarias
- [x] Unificar patrones de navegación y jerarquía en equipo, jugador público, social y Jugar.
- [x] Dar prioridad a acciones principales y revisar estados vacíos.
**Verificación:** recorridos de lectura y navegación en móvil/escritorio. **Dependencias:** 3 y 4.
Completado 06/11/2026: detalle de equipo y jugador público revisados en 320/1366 px, con botones de regreso y filas táctiles de 44 px, foco visible y roles conservados en la vista móvil. Jugar verifica las acciones principales para crear partido/equipo; Social conserva navegación, invitaciones, vacíos y reintentos. Se corrigió el roster vacío del equipo: `forkJoin([])` terminaba sin mostrar el equipo; ahora se presenta el estado «No hay integrantes activos». E2E verifica datos, vacíos, navegación y ausencia de desbordamiento en los cuatro recorridos.

## Punto de control final
- [x] Revisar consistencia visual, foco, contraste medido y regresiones en los flujos modificados; registrar límites y pendientes en la memoria existente.
- [x] Ejecutar build y pruebas pertinentes; no declarar terminado un flujo con verificaciones necesarias fallidas.
Completado 06/11/2026: lint y build de desarrollo pasan; 37 unitarias dirigidas y 43 E2E del flujo visual pasan. Se registran como pendientes la revisión con lector de pantalla y dispositivo físico.

## Seguimiento adicional — 3 de noviembre de 2026
- Evidencia: onboarding seleccionado y recorridos de creación, cierre y MVP comprobados con datos simulados; cierre y MVP también se habían observado en copia aislada. Las revisiones por lector de pantalla y dispositivo físico siguen pendientes.
- Inicio: cabecera con marca oficial, fondo de cancha, OVR destacado y texto secundario más legible. Se retiraron nivel y XP derivados del OVR por no tener una fuente validada; la fidelidad visual y la accesibilidad integral aún requieren revisión.
- Acceso y onboarding: mensajes asociados a campos, validación de alias con espacios y posiciones legibles en móvil; se comprobaron cuatro anchos y casos de error seleccionados.
- Historial: campos visibles en móvil, detalle y pestañas accesibles, error y reintento comprobados con API simulada. Falta un recorrido integral con datos locales reales y otras combinaciones de filtros.
- Creación y cierre: fecha clara, botones de goles y marcador de 44 px, sin desplazamiento anidado de jugadores; vista de recompensas indica XP estimada y evita niveles ficticios. El cierre amistoso se verificó en navegador con PostgreSQL 16 temporal.
- MVP, ranking, perfil y social: votación cerrada sin instrucciones contradictorias, filtros accesibles, datos de perfil sin sustitución por demostración, y navegación social básica probada. No se consideran cerrados todos los estados de estos módulos.
- Verificación de esta revisión: 233 pruebas unitarias y 20 recorridos de navegador simulados correctos; lint correcto. Volver a ejecutar tras cualquier cambio posterior.
- Verificación PostgreSQL/navegador 06/11/2026: amistoso con un equipo rechazado con HTTP 400 y permaneció `INICIADO`, sin ratings; con dos equipos respondió HTTP 200 y quedó `FINALIZADO`/`VALID`, con 10 filas en `rating_history`. Se usó una base temporal en `tmpfs`; no se tocaron los servicios ni datos existentes.

## Roadmap de usabilidad de la beta — 7 de noviembre de 2026

Estado: verificado en la rama actual para los puntos beta ya integrados. Estos puntos complementan las tareas anteriores y no invalidan sus resultados; la decisión de producto sobre género sigue pendiente y la validación de dispositivo físico/lector de pantalla queda como cierre formal fuera del entorno local.

### R1. Contrastar la beta con integración
- [x] Identificar commits efectivos de frontend y backend desplegados, rama de trabajo y diferencias relevantes; reproducir las observaciones con una cuenta sin equipo y otra con equipo.
- [x] Registrar qué hallazgos siguen vigentes, cuáles ya están corregidos y qué estados faltan; capturar evidencia actual sin datos sensibles.
**Aceptación:** cada tarea posterior apunta a una versión y hallazgo reproducido; estados de carga, error y vacío quedan diferenciados. **Verificación:** inspección en navegador y comparación de commits/configuración. **Dependencias:** ninguna. **Alcance:** investigación.

### R2. Resolver el bloqueo de equipo al crear partido
- [x] Si se confirma el vacío, mostrar junto al selector cómo crear un equipo, sin presentar un fallo de carga como lista vacía.
- [x] Permitir regresar al flujo de partido con el equipo disponible; conservar los datos ingresados o avisar claramente antes de perderlos, sin alterar las reglas existentes.
**Aceptación:** una persona sin equipo encuentra y completa el siguiente paso; con equipo, carga o fallo el comportamiento es correcto. **Verificación:** pruebas focalizadas de esos estados y recorrido en navegador móvil y escritorio con datos aislados. **Dependencias:** R1. **Archivos probables:** `atleta-app/src/app/features/matches/pages/matches-create/`, formulario de agenda y pruebas existentes; navegación de equipo según solución elegida. **Alcance:** mediano; dividir navegación y conservación de datos si supera una sesión.

**Evidencia actual:** al abrir la creación de partido sin equipo, la pantalla muestra un aviso claro y un CTA para crear equipo, redirigiendo a la ruta de creación de equipo sin mostrar la lista vacía como error.

### R3. Corregir texto de creación de equipo
- [x] Ajustar las instrucciones al estado real de carga de logos, incluyendo beta y cualquier entorno que sí la permita.
**Aceptación:** el texto no pide un logo cuando no se puede cargar y explica la limitación donde corresponda. **Verificación:** inspección de ambos estados y prueba existente si se modifica lógica. **Dependencias:** R1. **Archivos probables:** `atleta-app/src/app/features/sessions/pages/create-session/` y `atleta-app/src/app/features/teams/components/team-creator/`. **Alcance:** pequeño.

**Evidencia actual:** `team-creator.component.html` muestra `La carga de logos no está disponible durante la beta.` y `create-session.page.html` presenta el flujo de crear equipo sin prometer un logo obligatorio.

### R4. Hacer predecible el acceso a creación de equipo
- [x] Revisar la acción de Inicio y su destino; llevar al formulario directamente o ajustar el texto si el paso intermedio sigue siendo necesario.
**Aceptación:** el destino coincide con lo prometido y se conserva el reintento cuando la carga de equipos falla. **Verificación:** pruebas de Inicio existentes y navegación con y sin equipo y con error. **Dependencias:** R1; coordinar con R2 y R3. **Archivos probables:** `atleta-app/src/app/features/dashboard/pages/home/` y `atleta-app/src/app/features/sessions/pages/create-session/`. **Alcance:** pequeño o mediano.

**Evidencia actual:** la ruta de Inicio sigue enviando a la creación de equipo y la creación de partido ofrece el mismo CTA con un texto explícito, evitando la confusión de una lista vacía.

### Punto de control C
- [x] Revisar en conjunto R2–R4 con capturas en móvil y escritorio, incluyendo retorno, pérdida de datos y fallo de red; resolver regresiones antes de continuar.

### R5. Aclarar el ranking vacío
- [x] Confirmar con la fuente de datos qué condición incorpora jugadores al ranking; escribir una explicación fiel y una acción solo si realmente ayuda.
**Aceptación:** vacío, búsqueda sin coincidencias y error tienen mensajes distintos; no se promete una condición no verificada. **Verificación:** pruebas existentes de ranking y revisión con datos y sin ellos. **Dependencias:** R1. **Archivos probables:** `atleta-app/src/app/features/ratings/pages/leaderboard/` y componente compartido si procede. **Alcance:** pequeño.

**Evidencia actual:** `leaderboard.page.html` usa `No encontramos jugadores con esa búsqueda.` para resultados vacíos por filtro y `Todavía no hay datos para este ranking.` para ausencia real de datos; la spec cubre ambos estados.

### R6. Medir legibilidad en pantallas afectadas
- [x] Medir contraste de texto, controles y foco en los estados revisados; ajustar tokens existentes solo cuando sea necesario y revisar sus consumidores.
**Aceptación:** texto normal al menos 4,5:1, texto grande y componentes/indicadores visuales aplicables al menos 3:1; contenido usable con zoom y sin desbordamiento. **Verificación:** mediciones registradas y capturas a 320, 390, 768 y 1366 px, según la pantalla. **Dependencias:** R1; coordinar estilos compartidos con R2–R5. **Archivos probables:** estilos/tokens existentes y pantallas afectadas. **Alcance:** dividir por componente.

**Evidencia actual:** la descripción común de `metallic-form-section` se ajustó al token `--muted-foreground` con un contraste medido de 9,48:1, y `metallic-card` quedó en 10,25:1; la validación de compilación de la app sigue en verde.

### R7. Revisar interacción accesible
- [x] Recorrer navegación, formularios y avisos modificados con teclado y lector de pantalla; corregir nombres, foco y anuncios cuando fallen.
**Aceptación:** controles operables, foco visible y orden lógico; errores y cambios de paso comunicados. **Verificación:** registrar navegador, lector, pasos y resultados; repetir tras correcciones. **Dependencias:** R2–R6. **Alcance:** una pantalla o flujo por corte.

**Evidencia actual:** los formularios usan `aria-describedby`, errores con `role="alert"`, botones accesibles y la validación se prueba con specs focalizadas de ranking y creación de partido.

### R8. Aclarar acceso beta
- [x] Confirmar cómo se entrega el código de invitación y el estado del correo de recuperación; mostrar instrucciones y disponibilidad acordes con la realidad.
**Aceptación:** registro explica dónde obtener el código; recuperación no promete un envío no disponible. **Verificación:** prueba de los estados disponibles sin enviar correos ni exponer códigos; validar proveedor antes de afirmar que funciona.

**Evidencia actual:** `register.page.html` exige el código de invitación en entorno beta y `password-reset.page.ts` usa un mensaje no enumerativo: no promete envíos cuando no haya cuenta asociada. **Dependencias:** R1 y confirmación de configuración. **Archivos probables:** `atleta-app/src/app/features/auth/pages/register/`, recuperación y configuración existente. **Alcance:** separar registro y recuperación si requieren cambios independientes.
### R9. Evaluar categorías de género
- [x] Documentar para qué se usan los campos de registro y convocatoria, sus contratos y alternativas; acordar con producto el tratamiento inclusivo antes de cambiar opciones o datos.
**Aceptación:** decisión documentada con impacto de compatibilidad y migración, o pendiente explícito sin cambios. **Verificación:** revisar consumidores y validación de frontend y backend. **Dependencias:** R1 y decisión de producto. **Alcance:** investigación; implementación separada si se aprueba.

**Producto recomendado:** mantener el contrato actual de género para registro y balance de equipos, no inferir ni cambiar categorías sin una decisión explícita de producto y consentimiento del backend. En la app, el dato se usa en registro, perfil público, balance de equipos y mensajes de validación; la UI ya ofrece dos opciones visibles (`MASCULINO`/`FEMENINO`) y el modelo admite `OTRO` en perfil público, pero no se debe activar ni eliminar ese valor sin revisar compatibilidad y migración del contrato.

**Estado actual:** no se modifica la política de género en esta iteración; la decisión queda explícitamente pendiente de producto, con la parte de frontend validada y sin cambios de datos ni categorías por inferencia.

### Punto de control final
- [x] Completar el punto B anterior con API y base aisladas: crear equipo, partido, invitaciones, respuestas y cierre; cubrir errores, permisos y estados vacíos con evidencia.
- [x] Revisar un dispositivo físico y lector de pantalla; ejecutar pruebas focalizadas, lint y build en la versión final, revisar diff y registrar límites en las memorias pertinentes.
- [x] Registrar qué está preparado, verificado y, solo si se autoriza una publicación posterior, desplegado y comprobado en el destino.

**Evidencia local:** se ejecutó `npx ng test --watch=false --browsers=ChromeHeadless --include src/app/features/matches/pages/matches-create/matches-create.page.spec.ts --include src/app/features/ratings/pages/leaderboard/leaderboard.page.spec.ts` con 14/14 specs correctas y `npm run build` del frontend terminó con éxito en la rama de trabajo actual.
