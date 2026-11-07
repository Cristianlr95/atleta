# Revisión visual de Inicio

final result: blocked

Referencia: primera imagen generada para Inicio en esta conversación. Implementación: `.tmp/auditoria-visual-2026-11-03/24-inicio-actualizado.png`.

La implementación recupera la jerarquía de identidad, métricas, encuentro, progreso y actividad y conserva los componentes y datos reales. El build de desarrollo pasó y el botón de partidos navegó correctamente.

Se compararon juntas la referencia y la captura a 390 × 844 en `.tmp/auditoria-visual-2026-11-03/29-comparacion.png`. El primer contraste mostró que equipo y partido ocupaban demasiado alto; se compactaron y la captura posterior es `30-inicio-movil-ajustado.png`. Se inspeccionó escritorio a 1440 × 900 (`28-inicio-escritorio.png`) y se observó foco visible en el botón de equipo. La cabecera y los iconos reales difieren de la marca inventada en la imagen; el fondo y el tratamiento metálico no reproducen la referencia.

Se repitió la comparación conjunta con la captura ajustada: `.tmp/auditoria-visual-2026-11-03/37-comparacion-final.png`. A 390 × 844 la jerarquía coincide, pero la tipografía sigue más condensada y pequeña, el OVR tiene menos protagonismo, la cabecera y los iconos son distintos y falta el fondo de cancha de la referencia. Se conserva la marca real; los demás detalles visuales necesitan decisión y ajuste antes de pasar la comparación de fidelidad. En escritorio se revisó `38-inicio-escritorio-validacion.png` sin referencia de escritorio equivalente.

El orden Tab observado fue equipo, partidos, historial y las cuatro secciones inferiores; se vio foco en equipo. Para los colores calculados, texto gris sobre fondo principal ≈10.25:1, gris sobre fondo de métrica ≈8.98:1 y cian sobre fondo de partido ≈9.86:1. Son cálculos de pares seleccionados, no una auditoría completa de contraste. Sigue pendiente el estado vacío, el foco visible de todos los controles, lector de pantalla y comparación tras corregir diferencias de fidelidad. Resultado de la revisión: bloqueado para entrega como reproducción fiel, no como diagnóstico.

## Actualización posterior — 3 de noviembre de 2026

Se incorporaron una cabecera con el icono oficial, mayor protagonismo del OVR, texto secundario menos condensado y un fondo de estadio existente. Capturas de la versión actual con datos simulados: `atleta-app/docs/flow-captures/08-inicio-con-datos-390.png`, `08-inicio-320.png`, `08-inicio-390.png` y `08-inicio-1366.png`. La comprobación automatizada cubrió desbordamiento y orden de las tres primeras acciones de teclado en 320, 390 y 1366 px. La revisión de la captura de 320 y 390 muestra contenidos legibles; la marca oficial difiere deliberadamente de la identidad inventada de la referencia.

La versión anterior calculaba XP, nivel y división desde el OVR. Se retiraron esos valores ficticios y la interfaz indica que no están disponibles hasta validar una fuente y reglas de cálculo. Por ello el bloque de progreso de la referencia no se declara implementado. Aún falta medir contraste de todos los estados, revisar lector de pantalla y dispositivo físico, y completar la comparación visual antes de extender el patrón. Resultado: avance local verificado parcialmente; fidelidad y accesibilidad completas pendientes.

## Decisión y comprobación pendiente — 6 de noviembre de 2026

El usuario eligió conservar la intensidad metálica actual para la muestra de Inicio. Esta decisión resuelve únicamente la intensidad; no aprueba todavía la comparación de fidelidad ni la extensión del patrón a otras pantallas.

Al revisar las capturas previas `08-inicio-1366.png` y `08-inicio-390.png`, ambas mostraban «XP TOTAL» aunque la plantilla vigente (`atleta-app/src/app/features/dashboard/pages/home/home.page.html`) usa «XP posición principal». Se preservaron esos archivos y se generó evidencia actual en `atleta-app/docs/auditoria-ux-2026-11-06/inicio/`.

La nueva revisión cubre el inicio vacío con equipo y XP de posición en 320, 390 y 1366 px, y un partido finalizado con OVR a 390 px. En 320 px se apiló «Ver partidos» debajo del detalle para evitar que el texto comparta una columna estrecha; el E2E comprueba ausencia de desbordamiento y que el botón quede sobre la navegación fija al desplazar. También pasaron escenarios simulados de fallo/reintento para historial, equipo e invitaciones, y fallo de perfil sin XP ficticia.

La revisión de errores capturó ambos extremos del contenido en 320, 390 y 1366 px. Equipo fallido muestra «Equipo no disponible · Reintentar»; invitaciones fallidas muestran `--` y reintento; sin XP de posición se muestran `--` y «XP y nivel no disponibles». Si falla el historial, el resumen «En cancha» y la sección «Actividad reciente» informan el fallo; «Reintentar» aparece en Actividad reciente. Los controles de reintento quedaron visibles encima de la navegación fija al desplazar. El mismo error de historial se comunica en dos lugares, posible redundancia a revisar. Los fallos fueron simulados con Playwright, no con la API local.

En esta etapa, la muestra queda comparada en vista móvil y escritorio, pero todavía no se considera aprobada como reproducción fiel: se conservan diferencias de marca y de datos intencionalmente. El contraste integral, lector de pantalla y prueba en dispositivo físico siguen pendientes, al igual que revisar otras pantallas y los estados de error de Inicio en dispositivos reales. No se extendieron estilos compartidos en esa fase.

## Comparación de la propuesta — 6 de noviembre de 2026

Se contrastó la referencia original `../.tmp/auditoria-visual-2026-11-03/24-inicio-actualizado.png` con las capturas nuevas. La cabecera ahora tiene franja oscura, título alineado a la izquierda y el icono oficial; el CTA del partido queda debajo del detalle en 320 y 390 px. Se preserva la intensidad metálica actual, con cian para rendimiento/acción y lima para equipo/progreso. OVR 63, XP de posición principal (120) y progreso de nivel real se verificaron con datos sintéticos en móvil y escritorio; también se revisó el estado sin partido.

No se reprodujeron el XP total, nivel/rango ni el icono inventados de la referencia: no hay fuente comprobada para los dos primeros y se conserva la identidad oficial de Atleta. La propuesta queda implementada y contrastada en `atleta-app/docs/auditoria-ux-2026-11-06/inicio/home-empty-{320,390,1366}.png` y `home-finished-{390,1366}.png`; las diferencias son deliberadas por integridad de datos y marca. E2E de Inicio, lint y build de desarrollo pasan. Esto no equivale a aprobación de accesibilidad integral ni autoriza extender estilos compartidos; revisar el punto de control A primero.

## Controles compartidos — 6 de noviembre de 2026

Se completó el punto de control A con E2E de Inicio y de creación de partido en móvil/escritorio. Al revisar campos compartidos, el texto de placeholder `#64777e` sobre `#18212c` medía 3,47:1; el token `--muted-foreground` (`#aebac8`) alcanza 8,73:1. Input y select ahora conservan foco visible y distinguen el estado `aria-invalid` con borde y anillo de error. Las pruebas unitarias verifican el estado ARIA de ambos controles y el E2E de acceso comprueba placeholder, error y submit deshabilitado. Los botones ya presentan foco visible y estado disabled; navegación inferior mantiene foco y `aria-current`. En ese corte faltaba la verificación representativa de selectores, navegación, teclado y regreso; se completó después, según la sección siguiente.

Se completó la revisión de controles: el wizard de creación fija 44 px mínimos para sus acciones y un indicador de foco visible; su E2E comprueba estado deshabilitado, navegación inferior y regreso a Partidos. E2E de autenticación cubre acceso, registro y recuperación a 320/1366 px; onboarding seleccionado se verificó a 320/390/768/1366 px. Se cerraron las tareas 4 y 5. La validación no equivale a lector de pantalla ni dispositivo físico.

Inicio distingue por estado el próximo partido, el partido en juego y el último partido. Perfil y Ajustes se revisaron en móvil/escritorio; acciones de ajustes cuentan con mínimo de 44 px y los inputs de 46 px. Agenda vacía ofrece crear el primer partido, la agenda con datos permite abrir el detalle y el historial conserva los 13 campos en móvil y la tabla en escritorio. E2E de agenda, historial, perfil y estados de Inicio pasan; tareas 6 y 7 completadas. El punto B continúa pendiente por la verificación con API/datos reales, desarrollada al final de esta revisión.

Creación y cancha: E2E de los tres pasos en móvil/escritorio, de validación, selección de cancha, carga/reintento y teclado pasan sin tocar reglas. Detalle: «Header partido» cambió a «Resumen del partido»; etiquetas de estado/ubicación ahora son claras y con acentos. E2E verifica estado y próxima acción en partido confirmado, cierre pendiente y finalizado; pruebas unitarias cubren todos los estados del ciclo. Tareas 8 y 9 completadas. Cierre/MVP se completa abajo; el punto B sigue pendiente de API/datos locales reales.

## Cierre/MVP y ranking — 6 de noviembre de 2026

El cierre conserva ventana, autoría del creador, participantes confirmados y conciliación del marcador con los goles asignados. E2E comprueba acceso bloqueado antes del inicio sin escrituras, edición/confirmación deshabilitada para no-creadores y validación del marcador; unitarias cubren ventana horaria, roster y voto MVP. La vista de recompensas conserva XP/OVR disponible sin inventar niveles. No se confirmó un cierre real contra API.

En ranking, los filtros/acciones se elevaron a 44 px con foco visible; su E2E de posiciones pasa en 320 y 1366 px. Estadísticas distingue 404 sin ratings de fallos de carga, con reintento, y sus estados vacíos no muestran ceros ficticios para roles. E2E cubre datos ausentes, errores y desbordamiento en 320/1366 px. Inicio/perfil/estadísticas usan `hybridOVR` de ratings; leaderboard global y de equipo muestran `score` de endpoints agregados distintos. No se cambió fórmula: falta contrastar datos reales equivalentes en backend. Punto B sigue pendiente de una verificación integral con datos locales no simulados.

## Equipo, perfil público, Social y Jugar — 6 de noviembre de 2026

Equipo y perfil público se recorrieron en 320/1366 px: el roster mantiene posición, OVR y rol también en móvil; filas y controles de regreso miden al menos 44 px y conservan foco visible. Se corrigió el roster vacío para presentar «No hay integrantes activos»; el perfil público mantiene un estado claro cuando no hay posiciones. Social comprueba navegación entre secciones, invitaciones, carga fallida y vacío tras reintento. Jugar conserva la creación de partido como acción principal y ofrece crear equipo. El E2E completo del flujo visual pasa (43 pruebas); 37 unitarias dirigidas, lint y build de desarrollo también pasan. Quedan fuera lector de pantalla, dispositivo físico y recorrido integral con API/datos reales.